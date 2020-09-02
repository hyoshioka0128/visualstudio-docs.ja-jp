---
title: 出力ウィンドウの拡張 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Output window, about Output window
ms.assetid: b02fa88c-f92a-4ff6-ba5f-2eb4d48a643a
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2788903c60564d501770616fbe3ad2335e60a250
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68204429"
---
# <a name="extending-the-output-window"></a>出力ウィンドウの拡張
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[ **出力** ] ウィンドウは、一連の読み取り/書き込みテキストペインです。 Visual Studio には、 **Build**という組み込みのペインがあります。これらのウィンドウでは、プロジェクトはビルドに関するメッセージを伝達し、は **一般**に [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] IDE に関するメッセージを伝達します。 プロジェクトは、インターフェイスメソッドを使用して **ビルド** ウィンドウへの参照を自動的に取得 <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildableProjectCfg> します。また、Visual Studio は、サービスを使用して、 **[全般** ] ペインに直接アクセス <xref:Microsoft.VisualStudio.Shell.Interop.SVsGeneralOutputWindowPane> できます。 組み込みのペインに加えて、独自のカスタムペインを作成して管理することもできます。  
  
 **出力**ウィンドウは、インターフェイスとインターフェイスを使用して直接制御でき <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindow> <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindowPane> ます。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindow>サービスによって提供されるインターフェイスは、 <xref:Microsoft.VisualStudio.Shell.Interop.SVsOutputWindow> **出力**ウィンドウのペインを作成、取得、および破棄するためのメソッドを定義します。 この <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindow> インターフェイスは、ペインの表示、ペインの非表示、およびテキストの操作を行うためのメソッドを定義します。 **出力**ウィンドウを制御する別の方法として <xref:EnvDTE.OutputWindow> 、 <xref:EnvDTE.OutputWindowPane> Visual Studio オートメーションオブジェクトモデルのオブジェクトとオブジェクトを使用する方法があります。 これらのオブジェクトは、インターフェイスとインターフェイスのほぼすべての機能をカプセル化し <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindow> <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindowPane> ます。 さらに、 <xref:EnvDTE.OutputWindow> オブジェクトと <xref:EnvDTE.OutputWindowPane> オブジェクトにより、 **出力** ウィンドウペインの列挙やペインからのテキストの取得を簡単に行えるように、上位レベルの機能が追加されます。  
  
## <a name="creating-an-extension-that-uses-the-output-pane"></a>出力ウィンドウを使用する拡張機能の作成  
 出力ウィンドウのさまざまな側面を実行する拡張機能を作成できます。  
  
1. `TestOutput` **Testoutput**という名前のメニューコマンドを使用して、という名前の VSIX プロジェクトを作成します。 詳細については、「 [メニューコマンドを使用した拡張機能の作成](../extensibility/creating-an-extension-with-a-menu-command.md)」を参照してください。  
  
2. 次の参照を追加します。  
  
    1. EnvDTE  
  
    2. EnvDTE80  
  
3. TestOutput.cs で、次の using ステートメントを追加します。  
  
    ```f#  
    using EnvDTE;  
    using EnvDTE80;  
    ```  
  
4. TestOutput.cs で、ShowMessageBox メソッドを削除します。 次のメソッドスタブを追加します。  
  
    ```csharp  
    private void OutputCommandHandler(object sender, EventArgs e)  
    {  
    }  
    ```  
  
5. TestOutput コンストラクターで、コマンドハンドラーを OutputCommandHandler に変更します。 コマンドを追加する部分を次に示します。  
  
    ```csharp  
    OleMenuCommandService commandService = this.ServiceProvider.GetService(typeof(IMenuCommandService)) as OleMenuCommandService;  
    if (commandService != null)  
    {  
        CommandID menuCommandID = new CommandID(MenuGroup, CommandId);  
        EventHandler eventHandler = OutputCommandHandler;  
        MenuCommand menuItem = new MenuCommand(eventHandler, menuCommandID);  
        commandService.AddCommand(menuItem);  
    }  
    ```  
  
6. 以下のセクションでは、出力ペインを扱うさまざまな方法を示すさまざまな方法を紹介します。 これらのメソッドは、OutputCommandHandler () メソッドの本体に対して呼び出すことができます。 たとえば、次のコードでは、次のセクションで指定されている CreatePane () メソッドを追加しています。  
  
    ```csharp  
    private void OutputCommandHandler(object sender, EventArgs e)  
    {  
        CreatePane(new Guid(), "Created Pane", true, false);  
    }  
    ```  
  
## <a name="creating-an-output-window-with-ivsoutputwindow"></a>IVsOutputWindow を使用した出力ウィンドウの作成  
 この例では、インターフェイスを使用して、新しい **出力** ウィンドウウィンドウを作成する方法を示し <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindow> ます。  
  
```csharp  
void CreatePane(Guid paneGuid, string title,   
    bool visible, bool clearWithSolution)  
{  
    IVsOutputWindow output =   
        (IVsOutputWindow)GetService(typeof(SVsOutputWindow));  
    IVsOutputWindowPane pane;  
  
    // Create a new pane.  
    output.CreatePane(  
        ref paneGuid,   
        title,   
        Convert.ToInt32(visible),   
        Convert.ToInt32(clearWithSolution));  
  
    // Retrieve the new pane.  
    output.GetPane(ref paneGuid, out pane);  
  
     pane.OutputString("This is the Created Pane \n");  
}  
```  
  
 前のセクションで指定した拡張機能にこのメソッドを追加する場合、[ **testoutput の呼び出し** ] コマンドをクリックすると、 **出力** ウィンドウにヘッダーが表示されます。このヘッダーには、[ **出力元の表示:** ] という単語が表示されます。これは、ウィンドウ自体に **作成さ** れたウィンドウです。  
  
## <a name="creating-an-output-window-with-outputwindow"></a>OutputWindow を使用した出力ウィンドウの作成  
 この例では、オブジェクトを使用して **出力** ウィンドウペインを作成する方法を示し <xref:EnvDTE.OutputWindow> ます。  
  
```csharp  
void CreatePane(string title)  
{  
    DTE2 dte = (DTE2)GetService(typeof(DTE));  
    OutputWindowPanes panes =  
        dte.ToolWindows.OutputWindow.OutputWindowPanes;  
  
    try  
    {  
        // If the pane exists already, write to it.  
        panes.Item(title);  
    }  
    catch (ArgumentException)  
    {  
        // Create a new pane and write to it.  
        return panes.Add(title);  
    }  
}  
```  
  
 コレクションでは、[ <xref:EnvDTE.OutputWindowPanes> **出力** ] ウィンドウペインをタイトルで取得できますが、ペインタイトルは一意であるとは限りません。 タイトルが一意であることがわからない場合は、メソッドを使用し <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindow.GetPane%2A> て、正しいペインを GUID で取得します。  
  
 前のセクションで指定した拡張機能にこのメソッドを追加すると、[ **testoutput の呼び出し** ] コマンドをクリックしたときに、出力ウィンドウに "出力 **の表示: dtepane** " と "ペイン内の **追加された DTE ペイン** " というヘッダーが表示されます。  
  
## <a name="deleting-an-output-window"></a>出力ウィンドウの削除  
 この例では、 **出力** ウィンドウペインを削除する方法を示します。  
  
```csharp  
void DeletePane(Guid paneGuid)  
{  
    IVsOutputWindow output =  
    (IVsOutputWindow)ServiceProvider.GetService(typeof(SVsOutputWindow));  
  
    IVsOutputWindowPane pane;  
    output.GetPane(ref paneGuid, out pane);  
  
    if (pane == null)  
    {  
        CreatePane(paneGuid, "New Pane\n", true, true);  
    }  
     else  
    {  
        output.DeletePane(ref paneGuid);  
    }  
}  
```  
  
 前のセクションで指定した拡張機能にこのメソッドを追加する場合、[ **TestOutput の呼び出し** ] コマンドをクリックすると、出力ウィンドウに、[出力 **元の表示: 新規] ウィンドウ** と、ペイン内の [ **追加された** 項目] ウィンドウが表示されます。 [ **TestOutput の呼び出し** ] コマンドをもう一度クリックすると、ペインが削除されます。  
  
## <a name="getting-the-general-pane-of-the-output-window"></a>出力ウィンドウの [全般] ペインを取得する  
 この例では、**出力**ウィンドウの組み込みの **[全般**] ペインを取得する方法を示します。  
  
```csharp  
void GetGeneralPane()  
{  
    return (IVsOutputWindowPane)GetService(  
        typeof(SVsGeneralOutputWindowPane));  
}  
```  
  
 前のセクションで指定した拡張機能にこのメソッドを追加すると、[ **TestOutput を呼び出す**] コマンドをクリックしたときに、ウィンドウに [検索された項目の**全般] ウィンドウ**が表示**されます**。  
  
## <a name="getting-the-build-pane-of-the-output-window"></a>出力ウィンドウの [ビルド] ペインを取得する  
 この例では、[ビルド] ウィンドウを検索し、それに書き込む方法を示します。 ビルドウィンドウは既定でアクティブ化されていないため、アクティブ化します。  
  
```csharp  
void OutputTaskItemStringExExample(string buildMessage)  
{  
    EnvDTE80.DTE2 dte = (EnvDTE80.DTE2)ServiceProvider.GetService(typeof(EnvDTE.DTE));  
  
    EnvDTE.OutputWindowPanes panes =  
        dte.ToolWindows.OutputWindow.OutputWindowPanes;  
    foreach (EnvDTE.OutputWindowPane pane in panes)  
        {  
            if (pane.Name.Contains("Build"))  
            {  
                pane.OutputString(buildMessage + "\n");  
                pane.Activate();  
                return;  
             }  
        }  
}  
```
