---
title: ツールウィンドウの追加 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- tutorials
- tool windows
ms.assetid: 8e16c381-03c8-404e-92ef-3614cdf3150a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 169f386128ccdd79aef6b90a6703f50323b9b6f3
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85904146"
---
# <a name="add-a-tool-window"></a>ツールウィンドウを追加する

このチュートリアルでは、次の方法でツールウィンドウを作成し、Visual Studio に統合する方法について説明します。

- ツールウィンドウにコントロールを追加します。

- ツールウィンドウにツールバーを追加します。

- ツールバーにコマンドを追加します。

- コマンドを実装します。

- ツールウィンドウの既定の位置を設定します。

## <a name="prerequisites"></a>前提条件

Visual Studio SDK は、Visual Studio セットアップでオプション機能として含まれています。 詳細については、「 [Visual STUDIO SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-a-tool-window"></a>ツールウィンドウを作成する

1. VSIX テンプレートを使用して **Firsttoolwin** という名前のプロジェクトを作成し、 **FirstToolWindow**という名前のカスタムツールウィンドウ項目テンプレートを追加します。

    > [!NOTE]
    > ツールウィンドウを使用した拡張機能の作成の詳細については、「 [ツールウィンドウを使用した拡張機能の作成](../extensibility/creating-an-extension-with-a-tool-window.md)」を参照してください。

## <a name="add-a-control-to-the-tool-window"></a>ツールウィンドウにコントロールを追加する

1. 既定のコントロールを削除します。 *Firsttoolwindowcontrol .xaml*を開き、 **[Click Me!]** を削除します。 ボタンを選択します。

2. **ツールボックス**で、[**すべての WPF コントロール**] セクションを展開し、[ **Media 要素**] コントロールを**firsttoolwindowcontrol**フォームにドラッグします。 コントロールを選択し、[ **プロパティ** ] ウィンドウで、この要素に **mediaElement1**という名前を指定します。

## <a name="add-a-toolbar-to-the-tool-window"></a>ツールウィンドウにツールバーを追加する
次のようにツールバーを追加すると、そのグラデーションと色が IDE の他の部分と一致することが保証されます。

1. **ソリューションエクスプローラー**で、 *Firsttoolwindowpackage. vsct*を開きます。 *Vsct*ファイルは、XML を使用して、ツールウィンドウのグラフィカルユーザーインターフェイス (GUI) 要素を定義します。

2. セクションで、 `<Symbols>` 属性がであるノードを見つけ `<GuidSymbol>` `name` `guidFirstToolWindowPackageCmdSet` ます。 `<IDSymbol>` `<IDSymbol>` ツールバーとツールバーグループを定義するには、このノードの要素のリストに次の2つの要素を追加します。

    ```xml
    <IDSymbol name="ToolbarID" value="0x1000" />
    <IDSymbol name="ToolbarGroupID" value="0x1001" />
    ```

3. セクションのすぐ上に、次のような `<Buttons>` セクションを作成し `<Menus>` ます。

    ```xml
    <Menus>
        <Menu guid="guidFirstToolWindowPackageCmdSet" id="ToolbarID" priority="0x0000" type="ToolWindowToolbar">
            <Parent guid="guidFirstToolWindowPackageCmdSet" id="ToolbarID" />
            <Strings>
                <ButtonText>Tool Window Toolbar</ButtonText>
                <CommandName>Tool Window Toolbar</CommandName>
            </Strings>
        </Menu>
    </Menus>
    ```

    メニューにはいくつかの種類があります。 このメニューはツールウィンドウのツールバーで、属性によって定義されてい `type` ます。 との設定により、 `guid` `id` ツールバーの完全修飾 ID が構成されます。 通常、 `<Parent>` メニューのは、親グループです。 ただし、ツールバーは独自の親として定義されます。 したがって、要素と要素には同じ識別子が使用され `<Menu>` `<Parent>` ます。 `priority`属性は ' 0 ' にすぎません。

4. ツールバーは、さまざまな方法でメニューに似ています。 たとえば、メニューにコマンドのグループが含まれているとしても、ツールバーにはグループが含まれる場合があります。 (メニューでは、コマンドグループは水平線で区切られます。 ツールバーでは、グループは視覚的な区切り線で区切られていません)。

    `<Groups>`要素を含むセクションを追加 `<Group>` します。 これにより、セクションで宣言した ID を持つグループが定義され `<Symbols>` ます。 セクションの直後にセクションを追加し `<Groups>` `<Menus>` ます。

    ```xml
    <Groups>
        <Group guid="guidFirstToolWindowPackageCmdSet" id="ToolbarGroupID" priority="0x0000">
            <Parent guid="guidFirstToolWindowPackageCmdSet" id="ToolbarID" />
        </Group>
    </Groups>
    ```

    親の GUID と ID をツールバーの GUID と ID に設定すると、そのグループがツールバーに追加されます。

## <a name="add-a-command-to-the-toolbar"></a>ツールバーにコマンドを追加する

ツールバーにコマンドを追加します。これはボタンとして表示されます。

1. セクションで `<Symbols>` 、ツールバーとツールバーのグループ宣言の直後に、次の IDSymbol 要素を宣言します。

    ```xml
    <IDSymbol name="cmdidWindowsMedia" value="0x0100" />
    <IDSymbol name="cmdidWindowsMediaOpen" value="0x132" />
    ```

2. セクション内に Button 要素を追加し `<Buttons>` ます。 この要素は、ツールウィンドウのツールバーに、 **検索** (虫眼鏡) アイコン付きで表示されます。

    ```xml
    <Button guid="guidFirstToolWindowPackageCmdSet" id="cmdidWindowsMediaOpen" priority="0x0101" type="Button">
        <Parent guid="guidFirstToolWindowPackageCmdSet" id="ToolbarGroupID"/>
        <Icon guid="guidImages" id="bmpPicSearch" />
        <Strings>
            <CommandName>cmdidWindowsMediaOpen</CommandName>
            <ButtonText>Load File</ButtonText>
        </Strings>
    </Button>
    ```

3. *FirstToolWindowCommand.cs*を開き、既存のフィールドの直後に、クラスに次の行を追加します。

    ```csharp
    public const string guidFirstToolWindowPackageCmdSet = "00000000-0000-0000-0000-0000";  // get the GUID from the .vsct file
    public const uint cmdidWindowsMedia = 0x100;
    public const int cmdidWindowsMediaOpen = 0x132;
    public const int ToolbarID = 0x1000;
    ```

    これにより、コードでコマンドを使用できるようになります。

## <a name="add-a-mediaplayer-property-to-firsttoolwindowcontrol"></a>MediaPlayer プロパティを FirstToolWindowControl に追加します。
ツールバーコントロールのイベントハンドラーから、コードは FirstToolWindowControl クラスの子である Media Player コントロールにアクセスできる必要があります。

**ソリューションエクスプローラー**で、[ *firsttoolwindowcontrol .xaml*] を右クリックし、[**コードの表示**] をクリックして、firsttoolwindowcontrol クラスに次のコードを追加します。

```csharp
public System.Windows.Controls.MediaElement MediaPlayer
{
    get { return mediaElement1; }
}
```

## <a name="instantiate-the-tool-window-and-toolbar"></a>ツールウィンドウとツールバーのインスタンス化
ツールバーとメニューコマンドを追加して、[ **ファイルを開く** ] ダイアログを起動し、選択したメディアファイルを再生します。

1. *FirstToolWindow.cs*を開き、次のディレクティブを追加し `using` ます。

    ```csharp
    using System.ComponentModel.Design;
    using System.Windows.Forms;
    using Microsoft.VisualStudio.Shell.Interop;
    ```

2. FirstToolWindow クラス内で、FirstToolWindowControl コントロールへのパブリック参照を追加します。

    ```csharp
    public FirstToolWindowControl control;
    ```

3. コンストラクターの最後で、このコントロール変数を新しく作成したコントロールに設定します。

    ```csharp
    control = new FirstToolWindowControl();
    base.Content = control;
    ```

4. コンストラクター内でツールバーをインスタンス化します。

    ```csharp
    this.ToolBar = new CommandID(new Guid(FirstToolWindowCommand.guidFirstToolWindowPackageCmdSet),
        FirstToolWindowCommand.ToolbarID);
    this.ToolBarLocation = (int)VSTWT_LOCATION.VSTWT_TOP;
    ```

5. この時点で、FirstToolWindow コンストラクターは次のようになります。

    ```csharp
    public FirstToolWindow() : base(null)
    {
        this.Caption = "FirstToolWindow";
        this.BitmapResourceID = 301;
        this.BitmapIndex = 1;
        control = new FirstToolWindowControl();
        base.Content = control;
        this.ToolBar = new CommandID(new Guid(FirstToolWindowCommand.guidFirstToolWindowPackageCmdSet),
            FirstToolWindowCommand.ToolbarID);
            this.ToolBarLocation = (int)VSTWT_LOCATION.VSTWT_TOP;
    }
    ```

6. メニューコマンドをツールバーに追加します。 FirstToolWindowCommand.cs クラスに、次の using ディレクティブを追加します。

    ```csharp
    using System.Windows.Forms;
    ```

7. FirstToolWindowCommand クラスで、ShowToolWindow () メソッドの末尾に次のコードを追加します。 ButtonHandler コマンドは、次のセクションで実装されます。

    ```csharp
    // Create the handles for the toolbar command.
    var mcs = this.ServiceProvider.GetService(typeof(IMenuCommandService)) as OleMenuCommandService;
    var toolbarbtnCmdID = new CommandID(new Guid(FirstToolWindowCommand.guidFirstToolWindowPackageCmdSet),
        FirstToolWindowCommand.cmdidWindowsMediaOpen);
    var menuItem = new MenuCommand(new EventHandler(
        ButtonHandler), toolbarbtnCmdID);
    mcs.AddCommand(menuItem);
    ```

### <a name="to-implement-a-menu-command-in-the-tool-window"></a>ツールウィンドウにメニューコマンドを実装するには

1. FirstToolWindowCommand クラスに、[ **ファイルを開く** ] ダイアログを呼び出す buttonhandler メソッドを追加します。 ファイルが選択されると、メディアファイルが再生されます。

2. FirstToolWindowCommand クラスで、FindToolWindow () メソッドで作成される FirstToolWindow ウィンドウへのプライベート参照を追加します。

    ```csharp
    private FirstToolWindow window;
    ```

3. ShowToolWindow () メソッドを変更して、上で定義したウィンドウを設定します。これにより、ButtonHandler コマンドハンドラーがウィンドウコントロールにアクセスできるようになります。 完全な ShowToolWindow () メソッドを次に示します。

    ```csharp
    private void ShowToolWindow(object sender, EventArgs e)
    {
        window = (FirstToolWindow) this.package.FindToolWindow(typeof(FirstToolWindow), 0, true);
        if ((null == window) || (null == window.Frame))
        {
            throw new NotSupportedException("Cannot create tool window");
        }

        IVsWindowFrame windowFrame = (IVsWindowFrame)window.Frame;
        Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure(windowFrame.Show());

        var mcs = this.ServiceProvider.GetService(typeof(IMenuCommandService)) as OleMenuCommandService;
        var toolbarbtnCmdID = new CommandID(new Guid(FirstToolWindowCommandguidFirstToolWindowPackageCmdSet),
            FirstToolWindowCommand.cmdidWindowsMediaOpen);
        var menuItem = new MenuCommand(new EventHandler(
            ButtonHandler), toolbarbtnCmdID);
        mcs.AddCommand(menuItem);
    }
    ```

4. ButtonHandler メソッドを追加します。 ユーザーが再生するメディアファイルを指定するための OpenFileDialog を作成してから、選択したファイルを再生します。

    ```csharp
    private void ButtonHandler(object sender, EventArgs arguments)
    {
        OpenFileDialog openFileDialog = new OpenFileDialog();
        DialogResult result = openFileDialog.ShowDialog();
        if (result == DialogResult.OK)
        {
            window.control.MediaPlayer.Source = new System.Uri(openFileDialog.FileName);
        }
    }
    ```

## <a name="set-the-default-position-for-the-tool-window"></a>ツールウィンドウの既定の位置を設定する

次に、ツールウィンドウの IDE で既定の場所を指定します。 ツールウィンドウの構成情報は、 *FirstToolWindowPackage.cs* ファイルにあります。

1. *FirstToolWindowPackage.cs*で、クラスの <xref:Microsoft.VisualStudio.Shell.ProvideToolWindowAttribute> 属性を見つけ `FirstToolWindowPackage` ます。これにより、FirstToolWindow 型がコンストラクターに渡されます。 既定の位置を指定するには、次の例のように、コンストラクターにさらにパラメーターを追加する必要があります。

    ```csharp
    [ProvideToolWindow(typeof(FirstToolWindow),
        Style = Microsoft.VisualStudio.Shell.VsDockStyle.Tabbed,
        Window = "3ae79031-e1bc-11d0-8f78-00a0c9110057")]
    ```

    最初の名前付きパラメーターはで、 `Style` その値はです。これは、ウィンドウが既存のウィンドウのタブになることを `Tabbed` 意味します。 ドッキング位置は、パラメーターによって指定され `Window` ます。 n このケースでは、 **ソリューションエクスプローラー**の GUID になります。

    > [!NOTE]
    > IDE でのウィンドウの種類の詳細については、「」を参照してください <xref:EnvDTE.vsWindowType> 。

## <a name="test-the-tool-window"></a>ツールウィンドウをテストする

1. **F5**キーを押して、Visual Studio の実験的なビルドの新しいインスタンスを開きます。

2. [ **表示** ] メニューの [ **その他のウィンドウ** ] をポイントし、[ **最初のツールウィンドウ**] をクリックします。

    メディアプレーヤーのツールウィンドウは、 **ソリューションエクスプローラー**と同じ位置で開きます。 それでも以前と同じ位置に表示されている場合は、ウィンドウのレイアウトをリセットします (ウィンドウまたはウィンドウの**レイアウトをリセット**します)。

3. ツールウィンドウで、ボタン ( **検索** アイコンが表示されています) をクリックします。 サポートされているサウンドファイルまたはビデオファイル (たとえば、 *C:\windows\media\chimes.wav*) を選択し、[ **開く**] を押します。

    チャイム音が聞こえます。

## <a name="see-also"></a>関連項目
- [コマンド、メニュー、およびツールバー](../extensibility/internals/commands-menus-and-toolbars.md)
