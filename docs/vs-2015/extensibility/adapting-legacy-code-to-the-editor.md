---
title: レガシコードをエディターに適合させる |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - adapters
ms.assetid: a208d38e-9bea-41c9-9fe2-38bd86a359cb
caps.latest.revision: 26
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 0bb90723a72c10dbf6cfda5edd4aa68f71f1c6b9
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68184915"
---
# <a name="adapting-legacy-code-to-the-editor"></a>レガシ コードをエディターに適合させる
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio エディターには、既存のコードコンポーネントからアクセスできる多くの機能が用意されています。 次の手順では、非 MEF コンポーネント (たとえば、VSPackage) を調整してエディター機能を使用する方法を示します。 また、アダプターを使用して、マネージコードとアンマネージコードの両方でエディターのサービスを取得する方法についても説明します。  
  
## <a name="editor-adapters"></a>エディターアダプター  
 エディターアダプター (shim) は、API 内のクラスとインターフェイスも公開するエディターオブジェクトのラッパーです <xref:Microsoft.VisualStudio.TextManager.Interop> 。 これらのアダプターを使用すると、エディター以外のサービス (Visual Studio シェルコマンド、エディターサービスなど) 間を移動できます。 (これは、エディターが現在 Visual Studio でホストされている方法です)。また、Visual Studio では、レガシエディターと言語サービスの拡張機能が正しく動作するようになります。  
  
## <a name="using-editor-adapters"></a>エディターアダプターの使用  
 には、 <xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService> 新しいエディターインターフェイスとレガシインターフェイスを切り替えるメソッドと、アダプターを作成するメソッドが用意されています。  
  
 MEF コンポーネントパーツでこのサービスを使用している場合は、次のようにサービスをインポートできます。  
  
```  
[Import(typeof(IVsEditorAdaptersFactoryService))]  
internal IVsEditorAdaptersFactoryService editorFactory;  
```  
  
 このサービスを MEF 以外のコンポーネントで使用する場合は、このトピックで後述する「MEF 以外のコンポーネントでの Visual Studio エディターサービスの使用」の手順に従ってください。  
  
## <a name="switching-between-the-new-editor-api-and-the-legacy-api"></a>新しいエディター API とレガシ API の切り替え  
 エディターオブジェクトとレガシインターフェイスを切り替えるには、次のメソッドを使用します。  
  
|メソッド|変換|  
|------------|----------------|  
|<xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService.GetBufferAdapter%2A>|<xref:Microsoft.VisualStudio.Text.ITextBuffer> を <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer> に変換します。|  
|<xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService.GetDataBuffer%2A>|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer> を <xref:Microsoft.VisualStudio.Text.ITextBuffer> に変換します。|  
|<xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService.GetDocumentBuffer%2A>|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer> を <xref:Microsoft.VisualStudio.Text.ITextBuffer> に変換します。|  
|<xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService.GetViewAdapter%2A>|<xref:Microsoft.VisualStudio.Text.Editor.ITextView> を <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> に変換します。|  
|<xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService.GetWpfTextView%2A>|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> を <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextView> に変換します。|  
  
## <a name="creating-adapters"></a>アダプターの作成  
 レガシインターフェイス用のアダプターを作成するには、次のメソッドを使用します。  
  
|メソッド|変換|  
|------------|----------------|  
|<xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService.CreateVsCodeWindowAdapter%2A>|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow> を作成します。|  
|<xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService.CreateVsTextBufferAdapter%2A>|指定し <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer> たのを作成し <xref:Microsoft.VisualStudio.Utilities.IContentType> ます。|  
|<xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService.CreateVsTextBufferAdapter%2A>|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer> を作成します。|  
|<xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService.CreateVsTextBufferCoordinatorAdapter%2A>|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBufferCoordinator> を作成します。|  
|<xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService.CreateVsTextViewAdapter%2A>|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> の <xref:Microsoft.VisualStudio.Text.Editor.ITextViewRoleSet> を作成します。|  
|<xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService.CreateVsTextViewAdapter%2A>|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> を作成します。|  
  
## <a name="creating-adapters-in-unmanaged-code"></a>アンマネージコードでのアダプターの作成  
 すべてのアダプタークラスは、ローカルの共同作成可能なクラスとして登録され、関数を使用してインスタンス化でき `VsLocalCreateInstance()` ます。  
  
 すべてのアダプターは、. の vsshlids .h ファイルで定義されている Guid を使用して作成されます。Visual Studio SDK インストールの \VisualStudioIntegration\Common\Inc\ フォルダー。 VsTextBufferAdapter のインスタンスを作成するには、次のコードを使用します。  
  
```  
IVsTextBuffer *pBuf = NULL;  
VsLocalCreateInstance(CLSID_VsTextBuffer, NULL, CLSCTX_INPROC_SERVER, IID_IVsTextBuffer, (void**)&pBuf);  
```  
  
## <a name="creating-adapters-in-managed-code"></a>マネージコードでのアダプターの作成  
 マネージコードでは、アンマネージコードについて説明したのと同じ方法でアダプターを同時に作成できます。 また、アダプターを作成して操作できる MEF サービスを使用することもできます。 アダプターを取得するこの方法では、クロス作成時よりもきめ細かく制御できます。  
  
#### <a name="to-create-an-adapter-for-ivstextview"></a>IVsTextView 用のアダプターを作成するには  
  
1. Microsoft.VisualStudio.Editor.dll への参照を追加します。 `CopyLocal` が `false` に設定されていることを確認します。  
  
2. 次のように、をインスタンス化し <xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService> ます。  
  
    ```  
    using Microsoft.VisualStudio.Editor;  
    ...  
    IVsEditorAdaptersFactoryService adapterFactoryService = ComponentModel.GetService<IVsEditorAdaptersFactoryService>();  
    ```  
  
3. `CreateX()` メソッドを呼び出します。  
  
    ```  
    adapterFactoryService.CreateTextViewAdapter(textView);  
    ```  
  
## <a name="using-the-visual-studio-editor-directly-from-unmanaged-code"></a>アンマネージコードから直接 Visual Studio エディターを使用する  
 VSEditor 名前空間と VisualStudio 名前空間は、COM 呼び出し可能インターフェイスを IVx * インターフェイスとして公開しています。 たとえば、VisualStudio インターフェイスは、COM バージョンのインターフェイスです。 VSEditor インターフェイスは、インターフェイスの COM バージョンです。 <xref:Microsoft.VisualStudio.Text.ITextBuffer> では、バッファー `IVxTextBuffer` スナップショットにアクセスし、バッファーを変更し、バッファーのテキスト変更イベントをリッスンし、追跡ポイントとスパンを作成することができます。 次の手順は、からにアクセスする方法を示して `IVxTextBuffer` `IVsTextBuffer` います。  
  
#### <a name="to-get-an-ivxtextbuffer"></a>IVxTextBuffer を取得するには  
  
1. IVx * インターフェイスの定義は、.. の VSEditor ファイルにあります。Visual Studio SDK インストールの \VisualStudioIntegration\Common\Inc\ フォルダー。  
  
2. 次のコードでは、メソッドを使用してテキストバッファーをインスタンス化し `IVsUserData->GetData()` ます。 次のコードで `pData` は、はオブジェクトへのポインターです `IVsUserData` 。  
  
    ```  
    #include <textmgr.h>  
    #include <VSEditor.h>  
    #include <vsshlids.h>  
  
    CComPtr<IVsTextBuffer> pVsTextBuffer;  
    CComPtr<IVsUserData> pData;  
    CComPtr<IVxTextBuffer> pVxBuffer;  
    ...  
    if (SUCCEEDED(pVsTextBuffer->QueryInterface(IID_IVsUserData, &pData))  
    {  
        CComVariant vt;  
        if (SUCCEEDED(pData->GetData(GUID_VxTextBuffer, &vt)) &&  
        (vt.Type == VT_UNKNOWN) && (vt.punkVal != NULL))  
        {  
            vt.punkVal->QueryInterface(IID_IVxTextBuffer, (void**)&pVxBuffer);  
        }  
    }  
    ```  
  
## <a name="using-visual-studio-editor-services-in-a-non-mef-component"></a>MEF 以外のコンポーネントでの Visual Studio エディターサービスの使用  
 MEF を使用せず、Visual Studio エディターのサービスを使用する既存のマネージコードコンポーネントがある場合は、ComponentModelHost VSPackage を含むアセンブリへの参照を追加し、その SComponentModel サービスを取得する必要があります。  
  
#### <a name="to-consume-visual-studio-editor-components-from-a-non-mef-component"></a>MEF 以外のコンポーネントから Visual Studio エディターコンポーネントを使用するには  
  
1. で Microsoft.VisualStudio.ComponentModelHost.dll アセンブリへの参照を追加します。Visual Studio のインストールの \Common7\IDE\ フォルダー。 `CopyLocal` が `false` に設定されていることを確認します。  
  
2. 次のように `IComponentModel` 、Visual Studio エディターサービスを使用するクラスにプライベートメンバーを追加します。  
  
    ```  
    using Microsoft.VisualStudio.ComponentModelHost;  
    ....  
    private IComponentModel componentModel;  
    ```  
  
3. コンポーネントの初期化メソッドでコンポーネントモデルをインスタンス化します。  
  
    ```  
    componentModel =  
     (IComponentModel)Package.GetGlobalService(typeof(SComponentModel));  
    ```  
  
4. その後、必要なサービスのメソッドを呼び出すことにより、いずれかの Visual Studio エディターサービスを取得でき `IComponentModel.GetService<T>()` ます。  
  
    ```  
    textBufferFactoryService =  
         componentModel.GetService<ITextBufferFactoryService>();     
    ```
