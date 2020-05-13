---
title: ツール ウィンドウを追加する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- tutorials
- tool windows
ms.assetid: 8e16c381-03c8-404e-92ef-3614cdf3150a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 573f01043d8b1b0c2293a3ebf6e0c246a8727d6a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80740256"
---
# <a name="add-a-tool-window"></a>ツール ウィンドウを追加する

このチュートリアルでは、ツール ウィンドウを作成し、次の方法で Visual Studio に統合する方法について説明します。

- ツール ウィンドウにコントロールを追加します。

- ツール ウィンドウにツール バーを追加します。

- ツールバーにコマンドを追加します。

- コマンドを実装します。

- ツール ウィンドウの既定の位置を設定します。

## <a name="prerequisites"></a>必須コンポーネント

Visual Studio SDK は、Visual Studio のセットアップのオプション機能として含まれています。 詳細については、「 [Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-a-tool-window"></a>ツール ウィンドウを作成する

1. VSIX テンプレートを使用して**FirstToolWin**という名前のプロジェクトを作成し **、"FirstToolWindow"** という名前のカスタム ツール ウィンドウ項目テンプレートを追加します。

    > [!NOTE]
    > ツール ウィンドウを使用した拡張機能の作成の詳細については、「ツール[ウィンドウを使用した拡張機能の作成](../extensibility/creating-an-extension-with-a-tool-window.md)」を参照してください。

## <a name="add-a-control-to-the-tool-window"></a>ツール ウィンドウにコントロールを追加する

1. 既定のコントロールを削除します。 *最初のツールウィンドウコントロール.xamlを*開き、**クリックミーを削除します!** ボタンを選択します。

2. **ツールボックス**で、[**すべての WPF コントロール**] セクションを展開し、**メディア要素**コントロールを **[FirstToolWindowControl]** フォームにドラッグします。 コントロールを選択し、[**プロパティ]** ウィンドウで、この要素**mediaElement1**という名前を付けます。

## <a name="add-a-toolbar-to-the-tool-window"></a>ツール ウィンドウにツール バーを追加する
次の方法でツールバーを追加すると、そのグラデーションと色が IDE の他の部分と一致していることを保証します。

1. **ソリューション エクスプローラー**で、*最初にツール ウィンドウ パッケージを開きます*。 *.vsct*ファイルは、XML を使用してツール ウィンドウのグラフィカル ユーザー インターフェイス (GUI) 要素を定義します。

2. セクション`<Symbols>`で、`<GuidSymbol>``name`属性が . `guidFirstToolWindowPackageCmdSet` このノードの要素`<IDSymbol>`のリストに次の`<IDSymbol>`2 つの要素を追加して、ツールバーとツールバー グループを定義します。

    ```xml
    <IDSymbol name="ToolbarID" value="0x1000" />
    <IDSymbol name="ToolbarGroupID" value="0x1001" />
    ```

3. セクションのすぐ上`<Buttons>`に、次のような`<Menus>`セクションを作成します。

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

    メニューには、いくつかの異なる種類があります。 このメニューはツール ウィンドウのツールバーで、属性`type`で定義されています。 および`guid``id`設定は、ツールバーの完全修飾 ID を構成します。 通常、メニュー`<Parent>`のは包含するグループです。 ただし、ツールバーは独自の親として定義されます。 したがって、`<Menu>`と`<Parent>`要素に同じ識別子が使用されます。 属性`priority`は'0' だけです。

4. ツールバーは、多くの点でメニューに似ています。 たとえば、メニューにコマンドのグループがある場合と同様に、ツールバーにもグループを含めることもできます。 (メニューでは、コマンド グループは水平線で区切られます。 ツールバーでは、グループは視覚的な区分線で区切られるわけではありません。

    要素を`<Groups>`含むセクションを`<Group>`追加します。 これは、セクションで宣言した ID を`<Symbols>`持つグループを定義します。 セクションのすぐ`<Groups>`後にセクションを`<Menus>`追加します。

    ```xml
    <Groups>
        <Group guid="guidFirstToolWindowPackageCmdSet" id="ToolbarGroupID" priority="0x0000">
            <Parent guid="guidFirstToolWindowPackageCmdSet" id="ToolbarID" />
        </Group>
    </Groups>
    ```

    親の GUID と ID をツール バーの GUID と ID に設定すると、グループがツール バーに追加されます。

## <a name="add-a-command-to-the-toolbar"></a>ツールバーにコマンドを追加する

ボタンとして表示されるコマンドをツールバーに追加します。

1. `<Symbols>`セクションで、ツールバーとツールバー グループ宣言の直後に次の IDSymbol 要素を宣言します。

    ```xml
    <IDSymbol name="cmdidWindowsMedia" value="0x0100" />
    <IDSymbol name="cmdidWindowsMediaOpen" value="0x132" />
    ```

2. セクション内に Button`<Buttons>`要素を追加します。 この要素は、ツール ウィンドウのツール バーに **、検索**(虫眼鏡) アイコンとともに表示されます。

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

3. *FirstToolWindowCommand.cs*開き、既存のフィールドの直後に次の行をクラスに追加します。

    ```csharp
    public const string guidFirstToolWindowPackageCmdSet = "00000000-0000-0000-0000-0000";  // get the GUID from the .vsct file
    public const uint cmdidWindowsMedia = 0x100;
    public const int cmdidWindowsMediaOpen = 0x132;
    public const int ToolbarID = 0x1000;
    ```

    これにより、コマンドをコードで使用できるようになります。

## <a name="add-a-mediaplayer-property-to-firsttoolwindowcontrol"></a>コントロールにメディア プレーヤー プロパティを追加します。
ツール バー コントロールのイベント ハンドラーから、コードは、FirstToolWindowControl クラスの子であるメディア プレーヤー コントロールにアクセスできる必要があります。

**ソリューション エクスプローラー**で *、[FirstToolWindowControl.xaml]* を右クリックし、[**コードの表示**] をクリックして、次のコードを FirstToolWindowControl クラスに追加します。

```csharp
public System.Windows.Controls.MediaElement MediaPlayer
{
    get { return mediaElement1; }
}
```

## <a name="instantiate-the-tool-window-and-toolbar"></a>ツール ウィンドウとツール バーのインスタンスを作成する
[**ファイルを開く**] ダイアログを起動し、選択したメディア ファイルを再生するツール バーとメニュー コマンドを追加します。

1. *FirstToolWindow.cs*開き、次`using`のディレクティブを追加します。

    ```csharp
    using System.ComponentModel.Design;
    using System.Windows.Forms;
    using Microsoft.VisualStudio.Shell.Interop;
    ```

2. クラス内で、コントロールへのパブリック参照を追加します。

    ```csharp
    public FirstToolWindowControl control;
    ```

3. コンストラクターの最後に、このコントロール変数を新しく作成されたコントロールに設定します。

    ```csharp
    control = new FirstToolWindowControl();
    base.Content = control;
    ```

4. コンストラクター内のツール バーをインスタンス化します。

    ```csharp
    this.ToolBar = new CommandID(new Guid(FirstToolWindowCommand.guidFirstToolWindowPackageCmdSet),
        FirstToolWindowCommand.ToolbarID);
    this.ToolBarLocation = (int)VSTWT_LOCATION.VSTWT_TOP;
    ```

5. この時点で、FirstToolWindow コンストラクタは次のようになります。

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

6. メニュー コマンドをツールバーに追加します。 FirstToolWindowCommand.csクラスに、次の using ディレクティブを追加します。

    ```csharp
    using System.Windows.Forms;
    ```

7. クラスで、次のコードを追加します。 次のセクションでは、ButtonHandler コマンドが実装されます。

    ```csharp
    // Create the handles for the toolbar command.
    var mcs = this.ServiceProvider.GetService(typeof(IMenuCommandService)) as OleMenuCommandService;
    var toolbarbtnCmdID = new CommandID(new Guid(FirstToolWindowCommand.guidFirstToolWindowPackageCmdSet),
        FirstToolWindowCommand.cmdidWindowsMediaOpen);
    var menuItem = new MenuCommand(new EventHandler(
        ButtonHandler), toolbarbtnCmdID);
    mcs.AddCommand(menuItem);
    ```

### <a name="to-implement-a-menu-command-in-the-tool-window"></a>ツール ウィンドウにメニュー コマンドを実装するには

1. クラスで、**ファイルを開く**ダイアログを呼び出すボタンハンドラー メソッドを追加します。 ファイルが選択されると、メディア ファイルが再生されます。

2. クラスで、メソッドで作成される FirstToolWindow ウィンドウへのプライベート参照を追加します。

    ```csharp
    private FirstToolWindow window;
    ```

3. 上で定義したウィンドウを設定するように ShowToolWindow() メソッドを変更します (ButtonHandler コマンド ハンドラがウィンドウ コントロールにアクセスできるようにします)。 ここに完全な ShowToolWindow() メソッドがあります。

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

4. メソッドを追加します。 このコマンドは、再生するメディア ファイルを指定する OpenFileDialog を作成し、選択したファイルを再生します。

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

## <a name="set-the-default-position-for-the-tool-window"></a>ツール ウィンドウの既定の位置を設定する

次に、ツール ウィンドウの IDE で既定の場所を指定します。 ツール ウィンドウの構成情報は *、FirstToolWindowPackage.cs*ファイルに含まれています。

1. *FirstToolWindowPackage.cs*で、クラスの<xref:Microsoft.VisualStudio.Shell.ProvideToolWindowAttribute>属性を`FirstToolWindowPackage`見つけます。 既定の位置を指定するには、次の例に続くコンストラクターにさらにパラメーターを追加する必要があります。

    ```csharp
    [ProvideToolWindow(typeof(FirstToolWindow),
        Style = Microsoft.VisualStudio.Shell.VsDockStyle.Tabbed,
        Window = "3ae79031-e1bc-11d0-8f78-00a0c9110057")]
    ```

    最初の名前付き`Style`パラメータは、その`Tabbed`値は、ウィンドウが既存のウィンドウのタブになることを意味します。 ドッキング位置は、`Window`パラメーター n この場合は **、ソリューション エクスプローラー**の GUID で指定されます。

    > [!NOTE]
    > IDE のウィンドウの種類の詳細については、を参照してください<xref:EnvDTE.vsWindowType>。

## <a name="test-the-tool-window"></a>ツール ウィンドウをテストする

1. **F5 キー**を押して、Visual Studio の実験用ビルドの新しいインスタンスを開きます。

2. [**表示**] メニューの **[その他のウィンドウ]** をポイントし、[**最初のツール ウィンドウ**] をクリックします。

    メディア プレーヤー ツール ウィンドウは **、ソリューション エクスプローラー**と同じ位置に開きます。 以前と同じ位置に表示される場合は、ウィンドウレイアウトをリセットします (**ウィンドウ/ウィンドウレイアウトをリセット**)。

3. ツール ウィンドウのボタン (**検索**アイコンが表示されています) をクリックします。 サポートされているサウンド ファイルまたはビデオ ファイル (*たとえば、C:\windows\media\chimes.wav)* を選択し、[**開く**] を押します。

    チャイムの音が聞こえるはずです。

## <a name="see-also"></a>関連項目
- [コマンド、メニュー、およびツールバー](../extensibility/internals/commands-menus-and-toolbars.md)
