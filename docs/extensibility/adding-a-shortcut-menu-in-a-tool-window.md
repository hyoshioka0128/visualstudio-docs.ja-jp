---
title: ツールウィンドウにショートカットメニューを追加する |Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
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
ms.openlocfilehash: aa8d6f5c47289e66a51653e39d31890f09e8ceb2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85904195"
---
# <a name="add-a-shortcut-menu-in-a-tool-window"></a>ツールウィンドウにショートカットメニューを追加する
このチュートリアルでは、ツールウィンドウにショートカットメニューを配置します。 ショートカットメニューは、ユーザーがボタン、テキストボックス、またはウィンドウの背景を右クリックしたときに表示されるメニューです。 ショートカットメニューのコマンドは、他のメニューまたはツールバーのコマンドと同じように動作します。 ショートカットメニューをサポートするには、このファイルを *vsct* ファイルで指定し、マウスの右クリックに応答して表示します。

ツールウィンドウは、から継承されるカスタムツールウィンドウクラスの WPF ユーザーコントロールで構成さ <xref:Microsoft.VisualStudio.Shell.ToolWindowPane> れます。

このチュートリアルでは、Visual Studio メニューとしてショートカットメニューを作成する方法について説明します。このためには、 *vsct* ファイルでメニュー項目を宣言し、次に、マネージパッケージフレームワークを使用して、ツールウィンドウを定義するクラスにそれらを実装します。 この方法を使用すると、Visual Studio のコマンド、UI 要素、およびオートメーションオブジェクトモデルに簡単にアクセスできます。

また、ショートカットメニューから Visual Studio の機能にアクセスできない場合は、 <xref:System.Windows.FrameworkElement.ContextMenu%2A> ユーザーコントロールで XAML 要素のプロパティを使用できます。 詳細については、「 [ContextMenu](/dotnet/framework/wpf/controls/contextmenu)」を参照してください。

## <a name="prerequisites"></a>前提条件
Visual Studio 2015 以降では、ダウンロードセンターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップでオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「 [Visual STUDIO SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-the-tool-window-shortcut-menu-package"></a>ツールウィンドウのショートカットメニューパッケージを作成する

1. という名前の VSIX プロジェクトを作成 `TWShortcutMenu` し、 **ShortcutMenu** という名前のツールウィンドウテンプレートを追加します。 ツールウィンドウの作成の詳細については、「 [ツールウィンドウで拡張機能を作成](../extensibility/creating-an-extension-with-a-tool-window.md)する」を参照してください。

## <a name="specifying-the-shortcut-menu"></a>ショートカットメニューの指定
このチュートリアルに示されているようなショートカットメニューを使用すると、ツールウィンドウの背景の塗りつぶしに使用する色の一覧からユーザーが選択できるようになります。

1. *ShortcutMenuPackage*で、guidShortcutMenuPackageCmdSet という名前の guidsymbol 要素を検索し、ショートカットメニュー、ショートカットメニューグループ、およびメニューオプションを宣言します。 GuidSymbol 要素は次のようになります。

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

2. Buttons 要素の直前に、メニュー要素を作成し、そこにショートカットメニューを定義します。

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

    ショートカットメニューは、メニューまたはツールバーの一部ではないため、親を持ちません。

3. ショートカットメニュー項目を含む Group 要素を持つ Groups 要素を作成し、そのグループをショートカットメニューに関連付けます。

    ```xml
    <Groups>
        <Group guid="guidShortcutMenuPackageCmdSet" id="ColorGroup">
            <Parent guid="guidShortcutMenuPackageCmdSet" id="ColorMenu"/>
        </Group>
    </Groups>
    ```

4. Buttons 要素で、ショートカットメニューに表示される個々のコマンドを定義します。 Buttons 要素は次のようになります。

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

5. *ShortcutMenuCommand.cs*で、コマンドセット GUID、ショートカットメニュー、およびメニュー項目の定義を追加します。

    ```csharp
    public const string guidShortcutMenuPackageCmdSet = "00000000-0000-0000-0000-00000000"; // your GUID will differ
    public const int ColorMenu = 0x1000;
    public const int cmdidRed = 0x102;
    public const int cmdidYellow = 0x103;
    public const int cmdidBlue = 0x104;
    ```

    これらのコマンド Id は、 *ShortcutMenuPackage* ファイルの Symbols セクションで定義されているものと同じです。 ここには、このコンテキストグループは含まれていません。このコンテキストグループは、 *vsct* ファイルでのみ必要です。

## <a name="implementing-the-shortcut-menu"></a>ショートカットメニューの実装
 このセクションでは、ショートカットメニューとそのコマンドを実装します。

1. *ShortcutMenu.cs*では、ツールウィンドウはメニューコマンドサービスを取得できますが、それに含まれるコントロールは取得できません。 次の手順は、メニューコマンドサービスをユーザーコントロールで使用できるようにする方法を示しています。

2. *ShortcutMenu.cs*で、次の using ディレクティブを追加します。

    ```csharp
    using Microsoft.VisualStudio.Shell;
    using System.ComponentModel.Design;
    ```

3. ツールウィンドウの Initialize () メソッドをオーバーライドしてメニューコマンドサービスを取得し、コントロールを追加して、メニューコマンドサービスをコンストラクターに渡します。

    ```csharp
    protected override void Initialize()
    {
        var commandService = (OleMenuCommandService)GetService(typeof(IMenuCommandService));
        Content = new ShortcutMenuControl(commandService);
    }
    ```

4. ShortcutMenu tool ウィンドウコンストラクターで、コントロールを追加する行を削除します。 コンストラクターは次のようになります。

    ```csharp
    public ShortcutMenu() : base(null)
    {
        this.Caption = "ShortcutMenu";
        this.BitmapResourceID = 301;
        this.BitmapIndex = 1;
    }
    ```

5. *ShortcutMenuControl.xaml.cs*で、メニューコマンドサービスのプライベートフィールドを追加し、メニューコマンドサービスを実行するようにコントロールコンストラクターを変更します。 次に、メニューコマンドサービスを使用して、ショートカットメニューのコマンドを追加します。 ShortcutMenuControl コンストラクターは次のコードのようになります。 コマンドハンドラーは、後で定義します。

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

6. *ShortcutMenuControl*で、 <xref:System.Windows.UIElement.MouseRightButtonDown> 最上位レベルの要素にイベントを追加します <xref:System.Windows.Controls.UserControl> 。 XAML ファイルは次のようになります。

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

7. *ShortcutMenuControl.xaml.cs*で、イベントハンドラーのスタブを追加します。

    ```csharp
    private void MyToolWindow_MouseRightButtonDown(object sender, MouseButtonEventArgs e)
    {
    . . .
    }
    ```

8. 次の using ディレクティブを同じファイルに追加します。

    ```csharp
    using Microsoft.VisualStudio.Shell;
    using System.ComponentModel.Design;
    using System;
    using System.Windows.Input;
    using System.Windows.Media;
    ```

9. 次のようにイベントを実装し `MyToolWindowMouseRightButtonDown` ます。

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

    これに <xref:System.ComponentModel.Design.CommandID> より、ショートカットメニューのオブジェクトが作成され、マウスクリックの位置が識別され、メソッドを使用してその場所のショートカットメニューが開き <xref:Microsoft.VisualStudio.Shell.OleMenuCommandService.ShowContextMenu%2A> ます。

10. コマンドハンドラーを実装します。

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

    この場合、を識別し、それに応じて背景色を設定することによって、すべてのメニュー項目のイベントを処理するメソッドが1つだけに <xref:System.ComponentModel.Design.CommandID> なります。 メニュー項目に関連付けられていないコマンドが含まれている場合は、コマンドごとに個別のイベントハンドラーを作成します。

## <a name="test-the-tool-window-features"></a>ツールウィンドウの機能をテストする

1. プロジェクトをビルドし、デバッグを開始します。 実験用インスタンスが表示されます。

2. 実験用インスタンスで、[ **表示]/[その他のウィンドウ**] をクリックし、[ **ShortcutMenu**] をクリックします。 この操作を行うと、ツールウィンドウが表示します。

3. ツールウィンドウの本文を右クリックします。 色の一覧を含むショートカットメニューが表示されます。

4. ショートカットメニューの色をクリックします。 ツールウィンドウの背景色は、選択した色に変更する必要があります。

## <a name="see-also"></a>関連項目
- [コマンド、メニュー、およびツールバー](../extensibility/internals/commands-menus-and-toolbars.md)
- [サービスの使用と提供](../extensibility/using-and-providing-services.md)
