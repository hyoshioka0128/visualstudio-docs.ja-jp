---
title: 'チュートリアル: プログラムによるグラフィックス情報のキャプチャ |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: a5adeff9-afaf-4047-b5ce-ef0aefe710eb
caps.latest.revision: 24
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 9de8e2a2ee69911f5505937494d2912c724326e9
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/10/2020
ms.locfileid: "75847809"
---
# <a name="walkthrough-capturing-graphics-information-programmatically"></a>チュートリアル: プログラムによるグラフィックス情報のキャプチャ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] のグラフィックス診断を使用すると、Direct3D アプリケーションからプログラムによってグラフィックス情報をキャプチャできます。  
  
 プログラムによるキャプチャは次のようなシナリオで役立ちます。  
  
- 存在するスワップチェーンをグラフィックス アプリケーションが使用しないとき (テクスチャにレンダリングするときなど)、プログラムによるキャプチャを開始します。  
  
- アプリケーションがまったくレンダリングしないとき (DirectCompute を使用して計算を実行するときなど)、プログラムによるキャプチャを開始します。  
  
- レンダリングの問題を予測して手動テストでキャプチャすることは難しいものの、実行時にアプリケーションの状態に関する情報を使用してプログラムで予測できるときは、 `CaptureCurrentFrame`を呼び出します。  
  
## <a name="CaptureDX11_2"></a> Windows 8.1 のプログラムによるキャプチャ  
 このチュートリアルのパートでは、Windows 8.1 で DirectX 11.2 API を使用するアプリケーションでのプログラムによるキャプチャについて説明します。ここでは、堅牢なキャプチャ方法を使用します。 Windows 8.0 で前のバージョンの DirectX を使用しているアプリでプログラムによるキャプチャを使用する方法については、このチュートリアルで後述する「 [Programmatic capture in Windows 8.0 and earlier](#CaptureDX11_1) 」をご覧ください。  
  
 このセクションでは、次のタスクを実行する方法を示します。  
  
- プログラムによるキャプチャを使用するためにアプリケーションを準備する  
  
- IDXGraphicsAnalysis インターフェイスを取得する  
  
- グラフィックス情報をキャプチャする  
  
> [!NOTE]
> プログラムによるキャプチャの以前の実装では、Remote Tools for [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] を利用してキャプチャ機能を提供していましたが、Windows 8.1 は Direct3D 11.2 によりキャプチャを直接サポートしています。 このため、Windows 8.1 でプログラムによるキャプチャを行うために Remote Tools をインストールする必要がなくなりました。  
  
### <a name="preparing-your-app-to-use-programmatic-capture"></a>プログラムによるキャプチャを使用するためにアプリケーションを準備する  
 アプリケーションでプログラムによるキャプチャを使用するには、必要なヘッダーをインクルードすることが必要です。 これらのヘッダーは、Windows 8.1 の SDK の一部です。  
  
##### <a name="to-include-programmatic-capture-headers"></a>プログラムによるキャプチャのヘッダーをインクルードするには  
  
- IDXGraphicsAnalysis インターフェイスを定義するソース ファイルに、次のヘッダーをインクルードします。  
  
    ```  
    #include <DXGItype.h>  
    #include <dxgi1_2.h>  
    #include <dxgi1_3.h>  
    #include <DXProgrammableCapture.h>  
    ```  
  
    > [!IMPORTANT]
    > Windows 8.1 アプリケーションでプログラムによるキャプチャを実行するには、ヘッダー ファイル vsgcapture.h をインクルードしないでください。このファイルは Windows 8.0 以前のプログラムによるキャプチャをサポートしています。 このヘッダーは DirectX 11.2 で使用することはできません。 D3d11_2 .h ヘッダーの後にこのファイルが含まれている場合、コンパイラは警告を発行します。 D3d11_2 の前に vsgcapture. h が含まれている場合、アプリは起動しません。  
  
    > [!NOTE]
    > コンピューターに June 2010 DirectX SDK がインストールされており、プロジェクトのインクルード パスに `%DXSDK_DIR%includex86`が含まれている場合は、それをインクルード パスの最後に移動します。 ライブラリ パスでも同様にします。  
  
#### <a name="windows-phone-81"></a>Windows Phone 8.1  
 Windows Phone 8.1 SDK には DXProgrammableCapture ヘッダーが含まれていないため、`BeginCapture()` および `EndCapture()` メソッドを使用できるように、自分で `IDXGraphicsAnalysis` インターフェイスを定義する必要があります。 前のセクションで説明されているとおり、他のヘッダーをインクルードします。  
  
###### <a name="to-define-the-idxgraphicsanalysis-interface"></a>IDXGraphicsAnalysis インターフェイスを定義するには  
  
- ヘッダー ファイルをインクルードしたのと同じファイルで、IDXGraphicsAnalysis インターフェイスを定義します。  
  
  ```  
  interface DECLSPEC_UUID("9f251514-9d4d-4902-9d60-18988ab7d4b5") DECLSPEC_NOVTABLE  
  IDXGraphicsAnalysis : public IUnknown  
  {  
      STDMETHOD_(void, BeginCapture)() PURE;  
      STDMETHOD_(void, EndCapture)() PURE;  
  };  
  ```  
  
  使いやすくするために、新しいヘッダー ファイルでこれらのステップを実行し、その後で、アプリケーションで必要な個所にヘッダー ファイルをインクルードすることができます。  
  
### <a name="getting-the-idxgraphicsanalysis-interface"></a>IDXGraphicsAnalysis インターフェイスを取得する  
 DirectX 11.2 からグラフィックス情報をキャプチャする前に、DXGI デバッグ インターフェイスを取得する必要があります。  
  
> [!IMPORTANT]
> プログラムによるキャプチャを使用する場合は、引き続き、グラフィックス診断 ([!INCLUDE[vsprvs](../includes/vsprvs-md.md)]の Alt + F5 キー) または[コマンドラインキャプチャツール](../debugger/command-line-capture-tool.md)でアプリを実行する必要があります。  
  
##### <a name="to-get-the-idxgraphicsanalysis-interface"></a>IDXGraphicsAnalysis インターフェイスを取得するには  
  
- 以下のコードを使用して、DXGI デバッグ インターフェイスに対して IDXGraphicsAnalysis インターフェイスをフックします。  
  
    ```  
    IDXGraphicsAnalysis* pGraphicsAnalysis;  
    HRESULT getAnalysis = DXGIGetDebugInterface1(0, __uuidof(pGraphicsAnalysis), reinterpret_cast<void**>(&pGraphicsAnalysis));  
    ```  
  
     使用する前に正しいインターフェイスを取得できるように、 `HRESULT` から返される `DXGIGetDebugInterface1` を必ずチェックします。  
  
    ```  
    if (FAILED(getAnalysis))  
    {  
        // Abort program or disable programmatic capture in your app.  
    }  
    ```  
  
    > [!NOTE]
    > `DXGIGetDebugInterface1` によって `E_NOINTERFACE` (`error: E_NOINTERFACE No such interface supported`) が返された場合は、アプリがグラフィックス診断の下で実行されていることを確認します ([!INCLUDE[vsprvs](../includes/vsprvs-md.md)]で Alt + F5 キーを押します)。  
  
### <a name="capturing-graphics-information"></a>グラフィックス情報をキャプチャする  
 これで、正しい `IDXGraphicsAnalysis` インターフェイスを取得できたので、 `BeginCapture` および `EndCapture` を使用してグラフィックス情報をキャプチャできます。  
  
##### <a name="to-capture-graphics-information"></a>グラフィックス情報をキャプチャするには  
  
- グラフィックス情報のキャプチャを開始するには、 `BeginCapture`を使用します。  
  
    ```  
    ...  
    pGraphicsAnalysis->BeginCapture();  
    ...  
    ```  
  
     `BeginCapture` が呼び出されるとキャプチャはすぐに始まり、次のフレームが開始するのを待ちません。 現在のフレームが表示されたとき、または `EndCapture`を呼び出したときにキャプチャは停止します。  
  
    ```  
    ...  
    pGraphicsAnalysis->EndCapture();  
    ...  
    ```  
  
## <a name="CaptureDX11_1"></a> Programmatic capture in Windows 8.0 and earlier  
 チュートリアルのこの部分では、DirectX 11.1 API を使用する Windows 8.0 (およびそれ以前) のアプリケーションにおけるプログラムによるキャプチャについて説明します。これは、従来のキャプチャ方法を使用します。 Windows 8.1 で DirectX 11.2 を使用するアプリでプログラムによるキャプチャを使用する方法については、このチュートリアルで前述の「 [Windows 8.1 のプログラムによるキャプチャ](#CaptureDX11_2) 」をご覧ください。  
  
 ここでは、次のタスクについて説明します。  
  
- プログラムによるキャプチャを使用するためにコンピューターを準備する  
  
- プログラムによるキャプチャを使用するためにアプリケーションを準備する  
  
- グラフィックス ログ ファイルの名前と場所を設定する  
  
- `CaptureCurrentFrame` API の使用  
  
### <a name="preparing-your-computer-to-use-programmatic-capture"></a>プログラムによるキャプチャを使用するためにコンピューターを準備する  
 プログラム キャプチャ API は、Remote Tools for [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] を使用してキャプチャ機能を提供します。 ローカル コンピューターでプログラムによるキャプチャを使用している場合でも、アプリケーションが実行されるコンピューターにリモート ツールをインストールしておく必要があります。 ローカル コンピューターでプログラムによるキャプチャを行う場合は、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] を実行させる必要はありません。  
  
 コンピューターで実行しているアプリケーションでリモート キャプチャ API を使用するには、まず Remote Tools for [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] を対象のコンピューターにインストールする必要があります。 リモート ツールのバージョンによって、サポートしているハードウェア プラットフォームも異なります。 リモート ツールのインストール方法については、Microsoft のダウンロード Web サイトの「 [リモート ツールのダウンロード](https://visualstudio.microsoft.com/downloads#remote-tools) 」ページをご覧ください。  
  
 または [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] で、32 ビット アプリケーション向けのリモート キャプチャを実行するのに必要なコンポーネントをインストールします。  
  
> [!NOTE]
> [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]も含めて大半の Windows デスクトップ アプリケーションは、 [!INCLUDE[win8](../includes/win8-md.md)] for ARM デバイスでサポートされていないため、ARM デバイスでグラフィックス診断をキャプチャするには、Remote Tools for [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] をプログラム キャプチャ API と一緒に使用する方法しかありません。  
  
### <a name="preparing-your-app-to-use-programmatic-capture"></a>プログラムによるキャプチャを使用するためにアプリケーションを準備する  
 グラフィックス診断ツールを使用するには、まず依存するグラフィックス情報をキャプチャする必要があります。 `CaptureCurrentFrame` API を使用して、プログラムによって情報をキャプチャできます。  
  
##### <a name="to-prepare-your-app-to-capture-graphics-information-programmatically"></a>グラフィックス情報をプログラムによってキャプチャするためにアプリケーションを準備するには  
  
1. `vsgcapture.h` ヘッダーがアプリケーションのソース コードにインクルードされていることを確認します。 このヘッダーは、プログラム キャプチャ API を呼び出すソース コード ファイルや、複数のソース コード ファイルから API を呼び出すためのコンパイル済みヘッダー ファイルの中で、決まった場所にのみインクルードできます。  
  
2. アプリケーション用のソース コードで、現行のフレームの残りをキャプチャしようとするたびに、 `g_pVsgDbg->CaptureCurrentFrame()`を呼び出します。 この方法では、パラメーターを使用しないため戻り値がありません。  
  
### <a name="configuring-the-name-and-location-of-the-graphics-log-file"></a>グラフィックス ログ ファイルの名前と場所を設定する  
 グラフィックス ログは、 `DONT_SAVE_VSGLOG_TO_TEMP` および `VSG_DEFAULT_RUN_FILENAME` マクロで定義されている場所に作成されます。  
  
##### <a name="to-configure-the-name-and-location-of-the-graphics-log-file"></a>グラフィックス ログ ファイルの名前と場所を構成するには  
  
- グラフィックス ログが一時ディレクトリに書き込まれないようにするために、 `#include <vsgcapture.h>` 行の前に次の行を追加します。  
  
  ```  
  #define DONT_SAVE_VSGLOG_TO_TEMP  
  ```  
  
   この値を定義すると、作業ディレクトリに対して相対的な場所へグラフィックス ログを書き込むことも、( `VSG_DEFAULT_RUN_FILENAME` の定義が絶対パスの場合は) 絶対パスへ書き込むこともできます。  
  
- グラフィックス ログを別の場所へ保存するか、または別のファイル名を指定するには、 `#include <vsgcapture.h>` 行の前に次の行を追加します。  
  
  ```  
  #define VSG_DEFAULT_RUN_FILENAME <filename>  
  ```  
  
   この手順を実行しない場合、ファイル名は default.vsglog になります。 `DONT_SAVE_VSGLOG_TO_TEMP`を定義しないと、ファイルの場所は一時ディレクトリに対して相対的なものになります。それ以外の場合は、作業ディレクトリに対して相対的な場所になるか、または絶対的なファイル名を指定した場合は別の場所になります。  
  
  [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)] アプリの場合、temp ディレクトリの場所は各ユーザーとアプリに固有であり、通常、C:\users\\*ユーザー名*\AppData\Local\Packages\\*パッケージファミリ名*、tempstate\\などの場所にあります。 デスクトップアプリの場合、temp ディレクトリの場所は各ユーザーに固有であり、通常は C:\Users\\*username*\\\AppData\Local\Temp などの場所にあります。  
  
> [!NOTE]
> 特定の場所に書き込むには、その場所に対する書き込み権限を持っている必要があります。持っていない場合はエラーが発生します。 [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)] のアプリケーションは、アプリケーションがデータを書き込める場所についてはデスクトップ アプリケーションよりも制約が多く、特定の場所に書き込むためには追加の構成が必要な場合があります。  
  
### <a name="capturing-the-graphics-information"></a>グラフィックス情報をキャプチャする  
 プログラムによるキャプチャのためのアプリケーションの準備が完了して、グラフィックス ログ ファイルの場所と名前を選択的に構成したら、アプリケーションをビルドして実行またはデバッグし、データをキャプチャします。プログラム キャプチャ API を使用する場合は、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] からグラフィックス診断を開始しないでください。 グラフィックス ログは、指定した場所に書き込まれます。 このバージョンのログを保持したい場合は、別の場所に移動します。それ以外の場合は、アプリケーションを再実行したときにログが上書きされます。  
  
> [!TIP]
> プログラムによるキャプチャを使用している間でも、アプリケーションにフォーカスを置いた状態で **[Print Screen]** を押すだけでグラフィックス情報を手動でキャプチャできます。 この方法を使用すると、プログラム キャプチャ API でキャプチャされていない追加のグラフィックス情報をキャプチャできます。  
  
## <a name="next-steps"></a>次のステップ  
 このチュートリアルでは、プログラムでグラフィックス情報をキャプチャする方法を示しました。 次の手順では、次のオプションを検討します。  
  
- グラフィックス診断ツールを使用してキャプチャされたグラフィックス情報を解析する方法について学習します。 「[概要](../debugger/overview-of-visual-studio-graphics-diagnostics.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [チュートリアル: グラフィックス情報のキャプチャ](../debugger/walkthrough-capturing-graphics-information.md)   
 [Capturing Graphics Information](../debugger/capturing-graphics-information.md)   
 [コマンド ライン キャプチャ ツール](../debugger/command-line-capture-tool.md)
