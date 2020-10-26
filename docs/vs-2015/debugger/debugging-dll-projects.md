---
title: DLL プロジェクトのデバッグ |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- debugging DLLs
- templates, debugging DLLs
- DLLs, debugging
- debugging [Visual Studio], DLLs
ms.assetid: 433cab30-d191-460b-96f7-90d2530ca243
caps.latest.revision: 41
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 4a4533c304f84d9dc59ec6b05328528870e49655
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65691395"
---
# <a name="debugging-dll-projects"></a>DLL プロジェクトのデバッグ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

DLL を作成するテンプレートは次のとおりです。  
  
- (C++、C#、および Visual Basic) クラス ライブラリ  
  
- (C++、C#、および Visual Basic): Windows フォーム コントロール ライブラリ  
  
   Windows コントロール ライブラリのデバッグは、クラス ライブラリ プロジェクトのデバッグとほぼ同じです。 多くの場合、Windows コントロールは別のプロジェクトから呼び出します。 呼び出し元のプロジェクトをデバッグする場合は、Windows コントロールのコードにステップ インし、ブレークポイントを設定し、ほかのデバッグ操作を実行できます。 詳細については、「 [Windows フォーム コントロール](https://msdn.microsoft.com/library/f050de8f-4ebd-4042-94b8-edf9a1dbd52a)」を参照してください。  
  
- (C# および Visual Basic): Web コントロール ライブラリ  
  
   詳細については、「[Web Control Library (Managed Code)](../debugger/web-control-library-managed-code.md)」を参照してください。  
  
- (C++): MFC ActiveX コントロールと MFC スマート デバイス ActiveX コントロール  
  
   ActiveX コントロールは、インターネット経由でクライアント コンピューターにダウンロードでき、Web ページで表示したり、アクティブにしたりできるコントロールです。  
  
   ActiveX コントロールは、スタンドアロンでは実行できず、HTML Web ページに埋め込む必要があるため、そのデバッグは他の種類のコントロールのデバッグと似ています。 詳細については、「 [How to: Debug an ActiveX Control](../debugger/how-to-debug-an-activex-control.md)」を参照してください。  
  
- (C++): MFC スマート デバイス DLL  
  
   詳細については、「 [MFC のデバッグ技術](../debugger/mfc-debugging-techniques.md)」を参照してください。  
  
  このセクションでは、次のトピックについても説明します。  
  
- [方法: DLL プロジェクトからデバッグする](../debugger/how-to-debug-from-a-dll-project.md)  
  
- [方法: 混合モードでデバッグする](../debugger/how-to-debug-in-mixed-mode.md)  
  
  このトピックは次の内容で構成されており、クラス ライブラリ デバッグの準備に関する考慮事項について説明しています。  
  
- [デバッグ バージョンのビルド](#vxtskdebuggingdllprojectsbuildingadebugversion)  
  
- [混合モードのデバッグ](#vxtskdebuggingdllprojectsmixedmodedebugging)  
  
- [既定の構成の変更](#vxtskdebuggingdllprojectschangingdefaultconfigurations)  
  
- [DLL のデバッグ方法](#vxtskdebuggingdllprojectswaystodebugthedll)  
  
- [呼び出し元のアプリケーション](#vxtskdebuggingdllprojectsthecallingapplication)  
  
- [Web ページ上のコントロール](#vxtskdebuggingdllprojectscontrolsonawebpage)  
  
- [[イミディエイト] ウィンドウ](#vxtskdebuggingdllprojectstheimmediatewindow)  
  
## <a name="building-a-debug-version"></a><a name="vxtskdebuggingdllprojectsbuildingadebugversion"></a> デバッグバージョンのビルド  
 デバッグをどの方法で始める場合でも、DLL のデバッグ バージョンを先にビルドして、アプリケーションが参照する場所にデバッグ バージョンを配置するようにします。 この手順を忘れると、アプリケーションが別のバージョンの DLL を参照して読み込む可能性があります。 その場合、ブレークポイントがヒットせず、プログラムの実行が継続されます。 デバッグ時には、デバッガーの **[モジュール]** ウィンドウを開いて、プログラムが読み込んだ DLL を確認できます。 **[モジュール]** ウィンドウには、デバッグしているプロセスに読み込まれた DLL や EXE が一覧表示されます。 詳細については、「 [方法: [モジュール] ウィンドウを使用する](../debugger/how-to-use-the-modules-window.md)」を参照してください。  
  
 C++ で記述されたコードにデバッガーをアタッチするには、コードが `DebuggableAttribute`を生成する必要があります。 [/ASSEMBLYDEBUG](https://msdn.microsoft.com/library/94443af3-470c-41d7-83a0-7434563d7982) リンカー オプションを使ってリンクすると、これを自動的にコードに追加できます。  
  
## <a name="mixed-mode-debugging"></a><a name="vxtskdebuggingdllprojectsmixedmodedebugging"></a> 混合モードのデバッグ  
 DLL を呼び出す呼び出し元のアプリケーションは、マネージド コードで記述されている場合と、ネイティブ コードで記述されている場合があります。 マネージド DLL とそれを呼び出すネイティブ コードの両方をデバッグする場合は、マネージド デバッガーとネイティブ デバッガーを共に有効にする必要があります。 これは、[ ** \<Project> プロパティページ**] ダイアログボックスまたはウィンドウで選択できます。 DLL プロジェクトからデバッグを開始するか、呼び出し元のアプリケーション プロジェクトからデバッグを開始するかによって、確認方法は異なります。 詳細については、「 [方法: 混合モードでデバッグ](../debugger/how-to-debug-in-mixed-mode.md)する」を参照してください。  
  
## <a name="changing-default-configurations"></a><a name="vxtskdebuggingdllprojectschangingdefaultconfigurations"></a> 既定の構成の変更  
 プロジェクト テンプレートを使用してコンソール アプリケーション プロジェクトを作成するときは、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] により、デバッグ構成とリリース構成に必要な設定が自動的に作成されます。 これらの設定は必要に応じて変更できます。 詳細については、「 [C++ デバッグ構成のプロジェクト設定](../debugger/project-settings-for-a-cpp-debug-configuration.md)」、「 [C# デバッグ構成の](../debugger/project-settings-for-csharp-debug-configurations.md)プロジェクト設定」、「 [Visual Basic デバッグ構成のプロジェクト](../debugger/project-settings-for-a-visual-basic-debug-configuration.md)設定」、および「 [方法: デバッグ構成とリリース構成を設定する](../debugger/how-to-set-debug-and-release-configurations.md)」を参照してください。  
  
## <a name="ways-to-debug-the-dll"></a><a name="vxtskdebuggingdllprojectswaystodebugthedll"></a> DLL をデバッグする方法  
 このセクションの各プロジェクトでは、DLL を作成します。 DLL は直接実行できず、アプリケーション (通常は EXE) から呼び出す必要があります。 詳細については、「 [Creating and Managing Visual C++ Projects](https://msdn.microsoft.com/library/11003cd8-9046-4630-a189-a32bf3b88047)」を参照してください。 呼び出し元のアプリケーションは、次の条件のいずれかに該当している場合があります。  
  
- クラス ライブラリを格納する同じ [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ソリューション内の、別のプロジェクトにビルドされたアプリケーション  
  
- テスト コンピューターや運用コンピューターに既に配置されている既存のアプリケーション  
  
- Web に配置され、URL からアクセスするアプリケーション  
  
- DLL を埋め込む Web ページを含む Web アプリケーション  
  
### <a name="debugging-the-calling-application"></a><a name="vxtskdebuggingdllprojectsthecallingapplication"></a> 呼び出し元アプリケーションのデバッグ  
 DLL をデバッグするには、まず呼び出し元のアプリケーション (通常、EXE または Web アプリケーション) をデバッグします。 これには、複数の方法があります。  
  
- 呼び出し元のアプリケーションに対するプロジェクトが存在する場合は、そのプロジェクトを開いて、 **[デバッグ]** メニューから実行を開始できます。 詳細については、「 [How to: Start Execution](https://msdn.microsoft.com/b0fe0ce5-900e-421f-a4c6-aa44ddae453c)」を参照してください。  
  
- 呼び出し元のアプリケーションが、テスト コンピューターや運用コンピューターに配置されている既存のプログラムであり、既に動作している場合は、それにアタッチできます。 DLL が Internet Explorer によってホストされるコントロール、または Web ページ上のコントロールである場合は、この方法を使用します。 詳細については、「 [方法: 実行中のプロセスにアタッチする](https://msdn.microsoft.com/636d0a52-4bfd-48d2-89ad-d7b9ca4dc4f4)」を参照してください。  
  
- DLL プロジェクトからデバッグできます。 詳細については、「 [方法: DLL プロジェクトからデバッグ](../debugger/how-to-debug-from-a-dll-project.md)する」を参照してください。  
  
- [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] **イミディエイト** ウィンドウを開いて、プログラムが読み込んだ DLL を確認できます。 この場合、 **イミディエイト** ウィンドウは、アプリケーションの役割をします。  
  
  呼び出し元のアプリケーションのデバッグを始める前に、通常はクラス ライブラリ内にブレークポイントを設定します。 詳細については、「 [Breakpoints and Tracepoints](https://msdn.microsoft.com/fe4eedc1-71aa-4928-962f-0912c334d583)」を参照してください。 ブレークポイントにヒットした場合は、コードのステップ実行により、1 行ずつアクションを確認して問題を特定できます。 詳細については、「 [Code Stepping Overview](https://msdn.microsoft.com/8791dac9-64d1-4bb9-b59e-8d59af1833f9)」を参照してください。  
  
### <a name="controls-on-a-web-page"></a><a name="vxtskdebuggingdllprojectscontrolsonawebpage"></a> Web ページ上のコントロール  
 Web ページ コントロールをデバッグするには、それを埋め込む [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] ページを作成します (このようなページがまだ存在しない場合)。 次に、Web ページ コードとコントロール コードにブレークポイントを設定します。 Web ページを [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]から起動します。  
  
 呼び出し元のアプリケーションのデバッグを始める前に、通常は DLL 内にブレークポイントを設定します。 ブレークポイントにヒットした場合は、コードのステップ実行により、1 行ずつアクションを確認して問題を特定できます。 詳細については、「 [Breakpoints and Tracepoints](https://msdn.microsoft.com/fe4eedc1-71aa-4928-962f-0912c334d583)」を参照してください。  
  
### <a name="the-immediate-window"></a><a name="vxtskdebuggingdllprojectstheimmediatewindow"></a> [イミディエイト] ウィンドウ  
 DLL の関数やメソッドは、呼び出し元のアプリケーションがなくても評価できます。 そのためには、 **[イミディエイト]** ウィンドウを使用して、デザイン時デバッグを行います。 この方法でデバッグするには、DLL プロジェクトが開いているときに次の手順を実行します。  
  
1. デバッガーの **[イミディエイト]** ウィンドウを開きます。  
  
2. `Test` クラスの `Class1`メソッドをテストする場合は、次の C# コードを [イミディエイト] ウィンドウで入力して、 `Class1` 型のオブジェクトをインスタンス化します。 このマネージド コードは、構文を適切に変更することで Visual Basic と C++ で動作します。  
  
    ```  
    Class1 obj = new Class1();  
    ```  
  
     C# では、すべての名前を完全修飾する必要があります。 また、メソッドや変数はいずれもデバッグ セッションの現在のスコープとコンテキストに含まれる必要があります。  
  
3. `Test` が 1 つの `int` パラメーターを受け取るものと想定し、 `Test` [イミディエイト] **ウィンドウを使用して** を評価します。  
  
    ```  
    ?obj.Test(10)  
    ```  
  
     結果が **[イミディエイト]** ウィンドウに出力されます。  
  
4. `Test` の中にブレークポイントを配置し、関数を再び評価してデバッグを継続できます。  
  
    ```  
    ?obj.Test(10);  
    ```  
  
     ブレークポイントにヒットすると、 `Test`をステップ実行できます。 `Test`の実行が終了すると、デバッガーはデザイン モードに戻ります。  
  
## <a name="see-also"></a>参照  
 [マネージコードのデバッグ](../debugger/debugging-managed-code.md)   
 [Visual C++ のプロジェクトの種類](../debugger/debugging-preparation-visual-cpp-project-types.md)   
 [C#、F #、および Visual Basic プロジェクトの種類](../debugger/debugging-preparation-csharp-f-hash-and-visual-basic-project-types.md)   
 [C++ デバッグ構成のプロジェクト設定](../debugger/project-settings-for-a-cpp-debug-configuration.md)   
 [C# デバッグ構成のプロジェクト設定](../debugger/project-settings-for-csharp-debug-configurations.md)   
 [Visual Basic デバッグ構成のプロジェクト設定](../debugger/project-settings-for-a-visual-basic-debug-configuration.md)   
 [デバッガーのセキュリティ](../debugger/debugger-security.md)
