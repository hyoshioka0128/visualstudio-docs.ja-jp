---
title: ツール ウィンドウにショートカット メニューを追加する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- context menus, adding to tool windows
- menus, context menus
- shortcut menus, adding to tool windows
- tool windows, adding context menus
ms.assetid: 50234537-9e95-4b7e-9cb7-e5cf26d6e9d2
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 0f5b5b79721aa910c46e2580228d3f3a7836f70d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80740287"
---
# <a name="add-a-shortcut-menu-in-a-tool-window"></a>ツール ウィンドウにショートカット メニューを追加する
このチュートリアルでは、ツール ウィンドウにショートカット メニューを配置します。 ショートカット メニューは、ユーザーがボタン、テキスト ボックス、またはウィンドウの背景を右クリックしたときに表示されるメニューです。 ショートカット メニューのコマンドは、他のメニューやツールバーのコマンドと同じように動作します。 ショートカット メニューをサポートするには *、.vsct*ファイルで指定し、マウスの右クリックに応じて表示します。

ツール ウィンドウは、 から継承するカスタム ツール ウィンドウ クラスの WPF<xref:Microsoft.VisualStudio.Shell.ToolWindowPane>ユーザー コントロールで構成されます。

このチュートリアルでは *、.vsct*ファイルでメニュー項目を宣言し、ツール ウィンドウを定義するクラスでマネージ パッケージ フレームワークを使用してそれらを実装することによって、Visual Studio メニューとしてショートカット メニューを作成する方法を示します。 この方法では、Visual Studio のコマンド、UI 要素、およびオートメーション オブジェクト モデルへのアクセスが容易になります。

または、ショートカット メニューから Visual Studio の機能にアクセスできない場合は<xref:System.Windows.FrameworkElement.ContextMenu%2A>、ユーザー コントロールの XAML 要素のプロパティを使用できます。 詳細については、「[ショートカット メニュー](/dotnet/framework/wpf/controls/contextmenu)」を参照してください。

## <a name="prerequisites"></a>必須コンポーネント
Visual Studio 2015 以降では、ダウンロード センターから Visual Studio SDK をインストールしません。 これは、Visual Studio のセットアップのオプション機能として含まれています。 VS SDK は後でインストールすることもできます。 詳細については、「 [Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-the-tool-window-shortcut-menu-package"></a>ツール ウィンドウのショートカット メニュー パッケージを作成する

1. VSIX プロジェクトを作成`TWShortcutMenu`し、そのプロジェクトにショートカット**メニュー**という名前のツール ウィンドウ テンプレートを追加します。 ツール ウィンドウの作成の詳細については、「ツール ウィンドウ[を使用した拡張機能の作成](../extensibility/creating-an-extension-with-a-tool-window.md)」を参照してください。

## <a name="specifying-the-shortcut-menu"></a>ショートカット メニューの指定
このチュートリアルで示すようなショートカット メニューを使用すると、ツール ウィンドウの背景を塗りつぶすために使用する色の一覧から選択できます。

1. ショートカット*メニュー パッケージ.vsct*で、guidShortcutMenuPackageCmdSet という名前の GuidSymbol 要素を見つけ、ショートカット メニュー、ショートカット メニュー グループ、およびメニュー オプションを宣言します。 GuidSymbol 要素は次のようになります。

    ```xml
    <GuidSymbol name="guidShortcutMenuPackageCmdSet" value="{00000000-0000-0000-0000-0000}"> // your GUID here
        <IDSymbol name="ShortcutMenuCommandId" value="0x0100" />
        <IDSymbol name="ColorMenu" value="0x1000"/>
        <IDSymbol name="ColorGroup" value="0x1100"/>
        <IDSymbol name="cmdidRed" value="0x102"/>
        <IDSymbol name="cmdidYellow" value="0x103"/>
        <IDSymbol name="cmdidBlue" value="0x104"/>
    </GuidSymbol>
    ```

2. ボタン要素の直前に、メニュー要素を作成し、その中にショートカット メニューを定義します。

    ```vb
    <Menus>
      <Menu guid="guidShortcutMenuPackageCmdSet" id="ColorMenu" type="Context">
        <Strings>
          <ButtonText>Color change</ButtonText>
          <CommandName>ColorChange</CommandName>
        </Strings>
      </Menu>
    </Menus>
    ```

    ショートカット メニューは、メニューまたはツールバーの一部ではないため、親メニューを持っていません。

3. ショートカット メニュー項目を含むグループ要素を持つグループ要素を作成し、そのグループをショートカット メニューに関連付けます。

    ```xml
    <Groups>
        <Group guid="guidShortcutMenuPackageCmdSet" id="ColorGroup">
            <Parent guid="guidShortcutMenuPackageCmdSet" id="ColorMenu"/>
        </Group>
    </Groups>
    ```

4. Buttons 要素で、ショートカット メニューに表示される個々のコマンドを定義します。 Buttons 要素は次のようになります。

    ```xml
    <Buttons>
        <Button guid="guidShortcutMenuPackageCmdSet" id="ShortcutMenuCommandId" priority="0x0100" type="Button">
            <Parent guid="guidSHLMainMenu" id="IDG_VS_WNDO_OTRWNDWS1"/>
            <Icon guid="guidImages" id="bmpPic1" />
            <Strings>
                <ButtonText>ShortcutMenu</ButtonText>
            </Strings>
        </Button>

        <Button guid="guidShortcutMenuPackageCmdSet" id="cmdidRed" priority="1" type="Button">
            <Parent guid="guidShortcutMenuPackageCmdSet" id="ColorGroup" />
            <Strings>
                <ButtonText>Red</ButtonText>
            </Strings>
        </Button>

        <Button guid="guidShortcutMenuPackageCmdSet" id="cmdidYellow" priority="3" type="Button">
            <Parent guid="guidShortcutMenuPackageCmdSet" id="ColorGroup" />
            <Strings>
                <ButtonText>Yellow</ButtonText>
            </Strings>
        </Button>

        <Button guid="guidShortcutMenuPackageCmdSet" id="cmdidBlue" priority="5" type="Button">
            <Parent guid="guidShortcutMenuPackageCmdSet" id="ColorGroup" />
            <Strings>
                <ButtonText>Blue</ButtonText>
            </Strings>
        </Button>
    </Buttons>
    ```

5. *ShortcutMenuCommand.cs*で、コマンド セット GUID、ショートカット メニュー、およびメニュー項目の定義を追加します。

    ```csharp
    public const string guidShortcutMenuPackageCmdSet = "00000000-0000-0000-0000-00000000"; // your GUID will differ
    public const int ColorMenu = 0x1000;
    public const int cmdidRed = 0x102;
    public const int cmdidYellow = 0x103;
    public const int cmdidBlue = 0x104;
    ```

    これらは、*ショートカット メニュー パッケージ.vsct*ファイルのシンボル セクションで定義されているのと同じコマンド ID です。 コンテキスト グループは *.vsct*ファイルでのみ必要であるため、ここには含まれていません。

## <a name="implementing-the-shortcut-menu"></a>ショートカット メニューの実装
 このセクションでは、ショートカット メニューとそのコマンドを実装します。

1. *ShortcutMenu.cs*では、ツール ウィンドウはメニュー コマンド サービスを取得できますが、このウィンドウに含まれるコントロールは取得できません。 次の手順は、ユーザー コントロールでメニュー コマンド サービスを使用できるようにする方法を示しています。

2. *ShortcutMenu.cs*で、次の using ディレクティブを追加します。

    ```csharp
    using Microsoft.VisualStudio.Shell;
    using System.ComponentModel.Design;
    ```

3. メニュー コマンド サービスを取得し、コントロールを追加するツール ウィンドウの Initialize() メソッドをオーバーライドして、メニュー コマンド サービスをコンストラクターに渡します。

    ```csharp
    protected override void Initialize()
    {
        var commandService = (OleMenuCommandService)GetService(typeof(IMenuCommandService));
        Content = new ShortcutMenuControl(commandService);
    }
    ```

4. ショートカット メニュー ツール ウィンドウのコンストラクターで、コントロールを追加する行を削除します。 コンストラクタは次のようになります。

    ```csharp
    public ShortcutMenu() : base(null)
    {
        this.Caption = "ShortcutMenu";
        this.BitmapResourceID = 301;
        this.BitmapIndex = 1;
    }
    ```

5. *ShortcutMenuControl.xaml.cs*で、メニュー コマンド サービスのプライベート フィールドを追加し、メニュー コマンド サービスを受け取るようにコントロール コンストラクターを変更します。 次に、メニュー コマンド サービスを使用して、コンテキスト メニュー コマンドを追加します。 次のコードのように、ショートカット メニュー コントロールのコンストラクターが表示されます。 コマンド ハンドラーは後で定義されます。

    ```csharp
    public ShortcutMenuControl(OleMenuCommandService service)
    {
        this.InitializeComponent();
        commandService = service;

        if (null !=commandService)
        {
            // Create an alias for the command set guid.
            Guid guid = new Guid(ShortcutMenuCommand.guidShortcutMenuPackageCmdSet);

            // Create the command IDs.
            var red = new CommandID(guid, ShortcutMenuCommand.cmdidRed);
            var yellow = new CommandID(guid, ShortcutMenuCommand.cmdidYellow);
            var blue = new CommandID(guid, ShortcutMenuCommand.cmdidBlue);

            // Add a command for each command ID.
            commandService.AddCommand(new MenuCommand(ChangeColor, red));
            commandService.AddCommand(new MenuCommand(ChangeColor, yellow));
            commandService.AddCommand(new MenuCommand(ChangeColor, blue));
        }
    }
    ```

6. で *、* 最上位<xref:System.Windows.UIElement.MouseRightButtonDown><xref:System.Windows.Controls.UserControl>の要素にイベントを追加します。 XAML ファイルは次のようになります。

    ```vb
    <UserControl x:Class="TWShortcutMenu.ShortcutMenuControl"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
            Background="{DynamicResource VsBrush.Window}"
            Foreground="{DynamicResource VsBrush.WindowText}"
            mc:Ignorable="d"
            d:DesignHeight="300" d:DesignWidth="300"
            Name="MyToolWindow"
            MouseRightButtonDown="MyToolWindow_MouseRightButtonDown">
        <Grid>
            <StackPanel Orientation="Vertical">
                <TextBlock Margin="10" HorizontalAlignment="Center">ShortcutMenu</TextBlock>
            </StackPanel>
        </Grid>
    </UserControl>
    ```

7. *ShortcutMenuControl.xaml.cs*で、イベント ハンドラのスタブを追加します。

    ```csharp
    private void MyToolWindow_MouseRightButtonDown(object sender, MouseButtonEventArgs e)
    {
    . . .
    }
    ```

8. 同じファイルに次の using ディレクティブを追加します。

    ```csharp
    using Microsoft.VisualStudio.Shell;
    using System.ComponentModel.Design;
    using System;
    using System.Windows.Input;
    using System.Windows.Media;
    ```

9. 次のように`MyToolWindowMouseRightButtonDown`イベントを実装します。

    ```csharp
    private void MyToolWindow_MouseRightButtonDown(object sender, MouseButtonEventArgs e)
    {
        if (null != commandService)
        {
            CommandID menuID = new CommandID(
                new Guid(ShortcutMenuCommand.guidShortcutMenuPackageCmdSet),
                ShortcutMenuCommand.ColorMenu);
            Point p = this.PointToScreen(e.GetPosition(this));
            commandService.ShowContextMenu(menuID, (int)p.X, (int)p.Y);
        }
    }
    ```

    ショートカット メニュー<xref:System.ComponentModel.Design.CommandID>のオブジェクトが作成され、マウスクリックの位置が識別され、メソッドを使用してその場所でショートカット メニューが<xref:Microsoft.VisualStudio.Shell.OleMenuCommandService.ShowContextMenu%2A>開かれます。

10. コマンド ハンドラーを実装します。

    ```csharp
    private void ChangeColor(object sender, EventArgs e)
    {
        var mc = sender as MenuCommand;

        switch (mc.CommandID.ID)
        {
            case ShortcutMenuCommand.cmdidRed:
                MyToolWindow.Background = Brushes.Red;
                break;
            case ShortcutMenuCommand.cmdidYellow:
                MyToolWindow.Background = Brushes.Yellow;
                break;
            case ShortcutMenuCommand.cmdidBlue:
                MyToolWindow.Background = Brushes.Blue;
                break;
        }
    }
    ```

    この場合、1 つのメソッドが、すべてのメニュー項目のイベントを処理する場合<xref:System.ComponentModel.Design.CommandID>に、背景色を識別し、それに応じて設定します。 メニュー項目に関連のないコマンドが含まれている場合は、各コマンドに対して個別のイベント ハンドラーを作成します。

## <a name="test-the-tool-window-features"></a>ツール ウィンドウ機能をテストする

1. プロジェクトをビルドし、デバッグを開始します。 実験用インスタンスが表示されます。

2. 実験用のインスタンスで、[**表示/ その他のウィンドウ]** をクリックし、[**ショートカット メニュー**] をクリックします。 これを行うと、ツール ウィンドウが表示されます。

3. ツール ウィンドウの本文を右クリックします。 色の一覧を表示するショートカット メニューを表示する必要があります。

4. ショートカット メニューの色をクリックします。 ツール ウィンドウの背景色を選択した色に変更する必要があります。

## <a name="see-also"></a>関連項目
- [コマンド、メニュー、およびツールバー](../extensibility/internals/commands-menus-and-toolbars.md)
- [サービスの使用と提供](../extensibility/using-and-providing-services.md)
