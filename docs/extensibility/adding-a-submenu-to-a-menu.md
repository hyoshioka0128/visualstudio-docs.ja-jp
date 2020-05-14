---
title: メニューにサブメニューを追加する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- context menus
- submenus, cascading
- cascading submenus
- menus, creating cascading submenus
ms.assetid: 692600cb-d052-40e2-bdae-4354ae7c6c84
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 59c9364d03aab135f7c9b4bf91df21b949e78ee4
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80740271"
---
# <a name="add-a-submenu-to-a-menu"></a>メニューにサブメニューを追加する
このチュートリアルでは、「メニューを[Visual Studio メニュー バーに追加する](../extensibility/adding-a-menu-to-the-visual-studio-menu-bar.md)」のデモで **、TestMenu**メニューにサブメニューを追加する方法を示します。

 サブメニューは、別のメニューに表示されるセカンダリ メニューです。 サブメニューは、名前の後に続く矢印で識別できます。 名前をクリックすると、サブメニューとそのコマンドが表示されます。

 このチュートリアルでは、Visual Studio のメニュー バーのメニューにサブメニューを作成し、サブメニューに新しいコマンドを配置します。 このチュートリアルでは、新しいコマンドも実装します。

## <a name="prerequisites"></a>必須コンポーネント
 Visual Studio 2015 以降では、ダウンロード センターから Visual Studio SDK をインストールしません。 これは、Visual Studio のセットアップのオプション機能として含まれています。 VS SDK は後でインストールすることもできます。 詳細については、「 [Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="add-a-submenu-to-a-menu"></a>メニューにサブメニューを追加する

1. [「Visual Studio メニュー バーにメニューを追加する」の手順に](../extensibility/adding-a-menu-to-the-visual-studio-menu-bar.md)従って、プロジェクトとメニュー項目を作成します。 このチュートリアルの手順では、VSIX プロジェクトの名前が`TopLevelMenu`.

2. *を*開きます。 `<Symbols>`セクションで、サブメニューの`<IDSymbol>`要素、サブメニュー グループ用の要素、およびコマンド用の要素を "guidTopLevelMenuCmdSet" という名前の`<GuidSymbol>`ノードに追加します。 これは、最上位メニューの要素を`<IDSymbol>`含むノードと同じです。

    ```xml
    <IDSymbol name="SubMenu" value="0x1100"/>
    <IDSymbol name="SubMenuGroup" value="0x1150"/>
    <IDSymbol name="cmdidTestSubCommand" value="0x0105"/>
    ```

3. 新しく作成したサブメニューをセクション`<Menus>`に追加します。

    ```xml
    <Menu guid="guidTestCommandPackageCmdSet" id="SubMenu" priority="0x0100" type="Menu">
        <Parent guid="guidTestCommandPackageCmdSet" id="MyMenuGroup"/>
        <Strings>
            <ButtonText>Sub Menu</ButtonText>
            <CommandName>Sub Menu</CommandName>
        </Strings>
    </Menu>
    ```

     親の GUID と ID のペアは、メニューを[Visual Studio メニュー バーに追加で](../extensibility/adding-a-menu-to-the-visual-studio-menu-bar.md)生成されたメニュー グループを指定し、最上位のメニューの子です。

4. 手順 2 で定義したメニュー グループ`<Groups>`をセクションに追加し、サブメニューの子にします。

    ```xml
    <Group guid="guidTestCommandPackageCmdSet" id="SubMenuGroup" priority="0x0000">
        <Parent guid="guidTestCommandPackageCmdSet" id="SubMenu"/>
    </Group>
    ```

5. `<Buttons>`セクションに新`<Button>`しい要素を追加して、手順 2 で作成したコマンドをサブメニューの項目として定義します。

    ```xml
    <Button guid="guidTestCommandPackageCmdSet" id="cmdidTestSubCommand" priority="0x0000" type="Button">
        <Parent guid="guidTestCommandPackageCmdSet" id="SubMenuGroup" />
        <Icon guid="guidImages" id="bmpPic2" />
        <Strings>
           <CommandName>cmdidTestSubCommand</CommandName>
           <ButtonText>Test Sub Command</ButtonText>
        </Strings>
    </Button>
    ```

6. ソリューションをビルドし、デバッグを開始します。 実験用インスタンスが表示されます。

7. [**テスト メニュー] を**クリックして、**サブメニュー**という名前の新しいサブメニューを表示します。 サブメニューを開くには、[**サブメニュー]** をクリックし、新しいコマンドである**テスト サブ コマンド**を表示します。 **[サブ コマンドのテスト**] をクリックしても何も実行されません。

## <a name="add-a-command"></a>コマンドの追加

1. *TestCommand.cs*開き、既存のコマンド ID の後に次のコマンド ID を追加します。

    ```csharp
    public const int cmdidTestSubCmd = 0x0105;
    ```

2. サブコマンドを追加します。 コマンド コンストラクターを検索します。 `AddCommand`メソッドの呼び出しの直後に次の行を追加します。

    ```csharp
    CommandID subCommandID = new CommandID(CommandSet, cmdidTestSubCmd);
    MenuCommand subItem = new MenuCommand(new EventHandler(SubItemCallback), subCommandID);
    commandService.AddCommand(subItem);
    ```

    コマンド`SubItemCallback`ハンドラーは後で定義されます。 コンストラクタは次のようになります。

    ```csharp
    private TestCommand(Package package)
    {
        if (package == null)
        {
            throw new ArgumentNullException("package");
        }

        this.package = package;

        OleMenuCommandService commandService = this.ServiceProvider.GetService(typeof(IMenuCommandService)) as OleMenuCommandService;
        if (commandService != null)
        {
            var menuCommandID = new CommandID(CommandSet, CommandId);
            var menuItem = new MenuCommand(this.MenuItemCallback, menuCommandID);
            commandService.AddCommand(menuItem);

            CommandID subCommandID = new CommandID(CommandSet, cmdidTestSubCmd);
            MenuCommand subItem = new MenuCommand(new EventHandler(SubItemCallback), subCommandID);
            commandService.AddCommand(subItem);
        }
    }
    ```

3. `SubItemCallback()`を追加します。 これは、サブメニューの新しいコマンドがクリックされたときに呼び出されるメソッドです。

    ```csharp
    private void SubItemCallback(object sender, EventArgs e)
    {
        IVsUIShell uiShell = (IVsUIShell)this.ServiceProvider.GetServiceAsync(typeof(SVsUIShell));
        Guid clsid = Guid.Empty;
        int result;
        uiShell.ShowMessageBox(
            0,
            ref clsid,
            "TestCommand",
            string.Format(CultureInfo.CurrentCulture,
            "Inside TestCommand.SubItemCallback()",
            this.ToString()),
            string.Empty,
            0,
            OLEMSGBUTTON.OLEMSGBUTTON_OK,
            OLEMSGDEFBUTTON.OLEMSGDEFBUTTON_FIRST,
            OLEMSGICON.OLEMSGICON_INFO,
            0,
            out result);
    }
    ```

4. プロジェクトをビルドし、デバッグを開始します。 実験用インスタンスが表示されます。

5. [**テスト メニュー] メニュー**の **[サブ メニュー] を**クリックし、[サブ**コマンドのテスト**] をクリックします。 メッセージ ボックスが表示され、"TestCommand.SubItemCallback() 内のテスト コマンド" というテキストが表示されます。

## <a name="see-also"></a>関連項目

- [メニューを Visual Studio のメニュー バーに追加する](../extensibility/adding-a-menu-to-the-visual-studio-menu-bar.md)
- [コマンド、メニュー、およびツールバー](../extensibility/internals/commands-menus-and-toolbars.md)
