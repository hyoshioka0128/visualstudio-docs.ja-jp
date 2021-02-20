---
title: 出力ウィンドウの拡張 |Microsoft Docs
description: Visual Studio SDK の [出力] ウィンドウを拡張し、独自のカスタムペインを作成および管理する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Output window, about Output window
ms.assetid: b02fa88c-f92a-4ff6-ba5f-2eb4d48a643a
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 91c59737d269af4eb91df402f38346cf41e3146e
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99961769"
---
# <a name="extend-the-output-window"></a>出力ウィンドウを拡張する
[ **出力** ] ウィンドウは、一連の読み取り/書き込みテキストペインです。 Visual Studio には、 **Build** という組み込みのペインがあります。これらのウィンドウでは、プロジェクトはビルドに関するメッセージを伝達し、は **一般** に [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] IDE に関するメッセージを伝達します。 プロジェクトは、インターフェイスメソッドを使用して **ビルド** ウィンドウへの参照を自動的に取得 <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildableProjectCfg> します。また、Visual Studio は、サービスを使用して、 **[全般** ] ペインに直接アクセス <xref:Microsoft.VisualStudio.Shell.Interop.SVsGeneralOutputWindowPane> できます。 組み込みのペインに加えて、独自のカスタムペインを作成して管理することもできます。

 **出力** ウィンドウは、インターフェイスとインターフェイスを使用して直接制御でき <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindow> <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindowPane> ます。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindow>サービスによって提供されるインターフェイスは、 <xref:Microsoft.VisualStudio.Shell.Interop.SVsOutputWindow> **出力** ウィンドウのペインを作成、取得、および破棄するためのメソッドを定義します。 この <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindowPane> インターフェイスは、ペインの表示、ペインの非表示、およびテキストの操作を行うためのメソッドを定義します。 **出力** ウィンドウを制御する別の方法として <xref:EnvDTE.OutputWindow> 、 <xref:EnvDTE.OutputWindowPane> Visual Studio オートメーションオブジェクトモデルのオブジェクトとオブジェクトを使用する方法があります。 これらのオブジェクトは、インターフェイスとインターフェイスのほぼすべての機能をカプセル化し <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindow> <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindowPane> ます。 さらに、 <xref:EnvDTE.OutputWindow> オブジェクトと <xref:EnvDTE.OutputWindowPane> オブジェクトにより、 **出力** ウィンドウペインの列挙やペインからのテキストの取得を簡単に行えるように、上位レベルの機能が追加されます。

## <a name="create-an-extension-that-uses-the-output-pane"></a>出力ウィンドウを使用する拡張機能を作成する
 出力ウィンドウのさまざまな側面を実行する拡張機能を作成できます。

1. `TestOutput` **Testoutput** という名前のメニューコマンドを使用して、という名前の VSIX プロジェクトを作成します。 詳細については、「 [メニューコマンドを使用して拡張機能を作成](../extensibility/creating-an-extension-with-a-menu-command.md)する」を参照してください。

2. 次の参照を追加します。

    1. EnvDTE

    2. EnvDTE80

3. *TestOutput.cs* で、次の using ステートメントを追加します。

    ```f#
    using EnvDTE;
    using EnvDTE80;
    ```

4. *TestOutput.cs* で、メソッドを削除し `ShowMessageBox` ます。 次のメソッドスタブを追加します。

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

6. 以下のセクションでは、出力ペインを扱うさまざまな方法を示すさまざまな方法を紹介します。 これらのメソッドは、メソッドの本体に呼び出すことができ `OutputCommandHandler()` ます。 たとえば、次のコードは、 `CreatePane()` 次のセクションで示されているメソッドを追加します。

    ```csharp
    private void OutputCommandHandler(object sender, EventArgs e)
    {
        CreatePane(new Guid(), "Created Pane", true, false);
    }
    ```

## <a name="create-an-output-window-with-ivsoutputwindow"></a>IVsOutputWindow を使用して出力ウィンドウを作成する
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

## <a name="create-an-output-window-with-outputwindow"></a>OutputWindow を使用して出力ウィンドウを作成する
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
        panes.Add(title);
    }
}
```

 コレクションでは、[ <xref:EnvDTE.OutputWindowPanes> **出力** ] ウィンドウペインをタイトルで取得できますが、ペインタイトルは一意であるとは限りません。 タイトルが一意であることがわからない場合は、メソッドを使用し <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindow.GetPane%2A> て、正しいペインを GUID で取得します。

 前のセクションで指定した拡張機能にこのメソッドを追加すると、[ **testoutput の呼び出し** ] コマンドをクリックしたときに、出力ウィンドウに "出力 **の表示: dtepane** " と "ペイン内の **追加された DTE ペイン** " というヘッダーが表示されます。

## <a name="delete-an-output-window"></a>出力ウィンドウを削除する
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

## <a name="get-the-general-pane-of-the-output-window"></a>出力ウィンドウの [全般] ペインを取得します。
 この例では、**出力** ウィンドウの組み込みの **[全般**] ペインを取得する方法を示します。

```csharp
IVsOutputWindowPane GetGeneralPane()
{
    return (IVsOutputWindowPane)GetService(
        typeof(SVsGeneralOutputWindowPane));
}
```

 前のセクションで指定した拡張機能にこのメソッドを追加すると、[ **TestOutput を呼び出す**] コマンドをクリックしたときに、ウィンドウに [検索された項目の **全般] ウィンドウ** が表示 **されます**。

## <a name="get-the-build-pane-of-the-output-window"></a>[出力] ウィンドウの [ビルド] ウィンドウを取得します。
 この例では、[ **ビルド** ] ウィンドウを検索し、それに書き込む方法を示します。 **ビルド** ウィンドウは既定でアクティブ化されていないため、アクティブ化します。

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
