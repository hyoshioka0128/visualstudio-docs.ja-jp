---
title: 出力ウィンドウを拡張する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Output window, about Output window
ms.assetid: b02fa88c-f92a-4ff6-ba5f-2eb4d48a643a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 800b443b079111d1d09fffdd900b246a020578f4
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80711643"
---
# <a name="extend-the-output-window"></a>出力ウィンドウを拡張する
**出力**ウィンドウは、読み取り/書き込みテキスト ペインのセットです。 Visual Studio には、ビルドに関するメッセージをプロジェクトが伝達する**ビルド**、および IDE に関する[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]メッセージを伝達する**全般**という組み込みのペインがあります。 プロジェクトは、インターフェイス メソッド**を使用**してビルド<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildableProjectCfg>ペインへの参照を自動的に取得し、Visual Studio はサービス<xref:Microsoft.VisualStudio.Shell.Interop.SVsGeneralOutputWindowPane>を通じて **[全般**] ウィンドウに直接アクセスできます。 組み込みのペインに加えて、独自のカスタム ペインを作成および管理できます。

 **出力**ウィンドウは、<xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindow>インターフェイスを<xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindowPane>通じて直接制御できます。 サービスによって提供されるインターフェイスは<xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindow>、**出力**ウィンドウ ペインを作成、取得、および破棄するためのメソッドを定義します。 <xref:Microsoft.VisualStudio.Shell.Interop.SVsOutputWindow> インターフェイス<xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindowPane>は、ペインの表示、ペインの非表示、およびテキストの操作を行うためのメソッドを定義します。 **出力**ウィンドウを制御する別の方法は、Visual <xref:EnvDTE.OutputWindow> Studio<xref:EnvDTE.OutputWindowPane>オートメーション オブジェクト モデルの オブジェクトと を使用することです。 これらのオブジェクトは、 インターフェイス<xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindow><xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindowPane>のほぼすべての機能をカプセル化します。 また、<xref:EnvDTE.OutputWindow>オブジェクトは<xref:EnvDTE.OutputWindowPane>、**出力**ウィンドウ ペインを列挙し、ペインからテキストを取得しやすくするために、いくつかの高レベルの機能を追加します。

## <a name="create-an-extension-that-uses-the-output-pane"></a>[出力] ウィンドウを使用する拡張機能を作成する
 出力ペインのさまざまな側面を使用する拡張機能を作成できます。

1. **TestOutput**という名前の`TestOutput`メニュー コマンドで名前を付けた VSIX プロジェクトを作成します。 詳細については、「[メニュー コマンドを使用して拡張機能を作成する](../extensibility/creating-an-extension-with-a-menu-command.md)」を参照してください。

2. 次の参照を追加します。

    1. EnvDTE

    2. EnvDTE80

3. *TestOutput.cs*で、次の using ステートメントを追加します。

    ```f#
    using EnvDTE;
    using EnvDTE80;
    ```

4. *[TestOutput.cs]* で`ShowMessageBox`メソッドを削除します。 次のメソッドスタブを追加します。

    ```csharp
    private void OutputCommandHandler(object sender, EventArgs e)
    {
    }
    ```

5. テスト出力コンストラクターで、コマンド ハンドラーを "出力コマンド ハンドラー" に変更します。 コマンドを追加する部分は次のとおりです。

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

6. 以下のセクションでは、出力ペインに対するさまざまな処理方法を示すさまざまな方法を示します。 これらのメソッドをメソッドの本体に`OutputCommandHandler()`呼び出すことができます。 たとえば、次のコードは、次`CreatePane()`のセクションで指定したメソッドを追加します。

    ```csharp
    private void OutputCommandHandler(object sender, EventArgs e)
    {
        CreatePane(new Guid(), "Created Pane", true, false);
    }
    ```

## <a name="create-an-output-window-with-ivsoutputwindow"></a>出力ウィンドウを使用して出力ウィンドウを作成する
 この例では、インターフェイスを使用して新しい **[出力**]<xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindow>ウィンドウ ペインを作成する方法を示します。

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

 前のセクションで指定した拡張機能にこのメソッドを追加する場合 **、TestOutput の呼び出し**コマンドをクリックすると、[出力を表示] というヘッダーが表示される [**出力**]**This is the Created Pane**ウィンドウが表示されます **。**

## <a name="create-an-output-window-with-outputwindow"></a>出力ウィンドウを使用して出力ウィンドウを作成する
 この例では、オブジェクトを使用して**出力**ウィンドウ ペインを<xref:EnvDTE.OutputWindow>作成する方法を示します。

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

 <xref:EnvDTE.OutputWindowPanes>このコレクションでは **、出力**ウィンドウのウィンドウ枠をタイトルで取得できますが、ペインタイトルが一意であるとは保証されません。 タイトルの一意性を疑う場合は、メソッド<xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindow.GetPane%2A>を使用して GUID によって正しいウィンドウを取得します。

 このメソッドを前のセクションで指定した拡張機能に追加すると **、TestOutput の呼び出し**コマンドをクリックすると、[**出力を表示**] というヘッダーが表示される [出力] ウィンドウが**Added DTE Pane**表示されます。

## <a name="delete-an-output-window"></a>出力ウィンドウの削除
 この例では、**出力**ウィンドウ ペインを削除する方法を示します。

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

 前のセクションで指定した拡張機能にこのメソッドを追加する場合 **、TestOutput の呼び出し**コマンドをクリックすると、[出力を表示] というヘッダーが表示される [出力]**Added Created Pane**ウィンドウ**が表示されます。** [TestOutput の**呼び出し**] コマンドを再度クリックすると、ペインが削除されます。

## <a name="get-the-general-pane-of-the-output-window"></a>[出力] ウィンドウの [全般] ウィンドウを取得する
 この例では、**出力**ウィンドウの組み込みの **[全般**] ウィンドウを取得する方法を示します。

```csharp
IVsOutputWindowPane GetGeneralPane()
{
    return (IVsOutputWindowPane)GetService(
        typeof(SVsGeneralOutputWindowPane));
}
```

 前のセクションで指定した拡張機能にこのメソッドを追加する場合 **、TestOutput の呼び出し**コマンドをクリックすると、**出力**ウィンドウがペインに **[見つかった全般] ウィンドウが**表示されます。

## <a name="get-the-build-pane-of-the-output-window"></a>[出力] ウィンドウの [ビルド] ウィンドウを取得する
 この例では、[**ビルド**] ウィンドウを見つけて書き込む方法を示します。 **[ビルド**] ウィンドウは既定ではアクティブ化されないので、アクティブ化も行います。

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
