---
title: メニューにサブメニューを追加する |Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
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
ms.openlocfilehash: 5887dba1ed1c583653b93792174524f8dfb84609
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "86972323"
---
# <a name="add-a-submenu-to-a-menu"></a>メニューにサブメニューを追加する
このチュートリアルでは、[ **Testmenu** ] メニューにサブメニューを追加する方法を示して、「 [Visual Studio のメニューバーにメニューを追加](../extensibility/adding-a-menu-to-the-visual-studio-menu-bar.md)する」のデモを基にして説明します。

 サブメニューは、別のメニューに表示されるセカンダリメニューです。 サブメニューは、名前の後に続く矢印で識別できます。 名前をクリックすると、サブメニューとそのコマンドが表示されます。

 このチュートリアルでは、Visual Studio のメニューバーのメニューにサブメニューを作成し、サブメニューに新しいコマンドを配置します。 このチュートリアルでは、新しいコマンドも実装しています。

## <a name="prerequisites"></a>前提条件
 Visual Studio 2015 以降では、ダウンロードセンターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップでオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「 [Visual STUDIO SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="add-a-submenu-to-a-menu"></a>メニューにサブメニューを追加する

1. 「 [Visual Studio のメニューバーにメニューを追加](../extensibility/adding-a-menu-to-the-visual-studio-menu-bar.md) する」の手順に従って、プロジェクトとメニュー項目を作成します。 このチュートリアルの手順では、VSIX プロジェクトの名前がであることを前提として `TopLevelMenu` います。

2. *Testcommandpackage. vsct*を開きます。 セクションで、サブ `<Symbols>` `<IDSymbol>` メニューの要素、サブメニューグループ、および `<GuidSymbol>` "guidTopLevelMenuCmdSet" という名前のノード内のコマンドの要素を追加します。 これは、 `<IDSymbol>` トップレベルメニューの要素を含むノードと同じです。

    ```xml
    <IDSymbol name="SubMenu" value="0x1100"/>
    <IDSymbol name="SubMenuGroup" value="0x1150"/>
    <IDSymbol name="cmdidTestSubCommand" value="0x0105"/>
    ```

3. 新しく作成したサブメニューをセクションに追加し `<Menus>` ます。

    ```xml
    <Menu guid="guidTestCommandPackageCmdSet" id="SubMenu" priority="0x0100" type="Menu">
        <Parent guid="guidTestCommandPackageCmdSet" id="MyMenuGroup"/>
        <Strings>
            <ButtonText>Sub Menu</ButtonText>
            <CommandName>Sub Menu</CommandName>
        </Strings>
    </Menu>
    ```

     親の GUID/ID ペアは、「 [メニューを Visual Studio に追加する](../extensibility/adding-a-menu-to-the-visual-studio-menu-bar.md)」で生成されたメニューグループを指定し、トップレベルメニューの子です。

4. 手順2で定義したメニューグループをセクションに追加 `<Groups>` し、サブメニューの子にします。

    ```xml
    <Group guid="guidTestCommandPackageCmdSet" id="SubMenuGroup" priority="0x0000">
        <Parent guid="guidTestCommandPackageCmdSet" id="SubMenu"/>
    </Group>
    ```

5. セクションに新しい要素を追加し `<Button>` `<Buttons>` て、手順 2. で作成したコマンドをサブメニューの項目として定義します。

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

6. ソリューションをビルドし、デバッグを開始します。 実験用のインスタンスが表示されます。

7. [ **Testmenu** ] をクリックすると、 **サブメニュー**という名前の新しいサブメニューが表示されます。 [ **サブメニュー** ] をクリックしてサブメニューを開き、新しいコマンド [ **Test Sub command**] を表示します。 [ **テストサブコマンド]** をクリックしても何も行われないことに注意してください。

## <a name="add-a-command"></a>コマンドの追加

1. *TestCommand.cs*を開き、既存のコマンド id の後に次のコマンド id を追加します。

    ```csharp
    public const int cmdidTestSubCmd = 0x0105;
    ```

2. サブコマンドを追加します。 コマンドコンストラクターを検索します。 メソッドの呼び出しの直後に、次の行を追加し `AddCommand` ます。

    ```csharp
    CommandID subCommandID = new CommandID(CommandSet, cmdidTestSubCmd);
    MenuCommand subItem = new MenuCommand(new EventHandler(SubItemCallback), subCommandID);
    commandService.AddCommand(subItem);
    ```

    `SubItemCallback`コマンドハンドラーは、後で定義します。 コンストラクターは次のようになります。

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
        ThreadHelper.ThrowIfNotOnUIThread();
        IVsUIShell uiShell = this.package.GetService<SVsUIShell, IVsUIShell>();
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

5. [ **Testmenu** ] メニューの [ **sub menu** ] をクリックし、[ **Test sub Command**] をクリックします。 メッセージボックスが表示され、"Test Command in TestCommand. SubItemCallback ()" というテキストが表示されます。

## <a name="see-also"></a>関連項目

- [メニューを Visual Studio のメニューバーに追加する](../extensibility/adding-a-menu-to-the-visual-studio-menu-bar.md)
- [コマンド、メニュー、およびツールバー](../extensibility/internals/commands-menus-and-toolbars.md)
