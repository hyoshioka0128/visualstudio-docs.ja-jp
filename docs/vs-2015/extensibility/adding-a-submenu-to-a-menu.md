---
title: メニューにサブメニューを追加する |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- context menus
- submenus, cascading
- cascading submenus
- menus, creating cascading submenus
ms.assetid: 692600cb-d052-40e2-bdae-4354ae7c6c84
caps.latest.revision: 44
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: f458d46395c3a902e62ba5dd4ac7d624c326700c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68184890"
---
# <a name="adding-a-submenu-to-a-menu"></a>サブメニューのメニューへの追加
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このチュートリアルでは、[ **Testmenu** ] メニューにサブメニューを追加する方法を示して、 [Visual Studio のメニューバーにメニュー](../extensibility/adding-a-menu-to-the-visual-studio-menu-bar.md)を追加する方法のデモについて説明します。  
  
 サブメニューは、別のメニューに表示されるセカンダリメニューです。 サブメニューは、名前の後に続く矢印で識別できます。 名前をクリックすると、サブメニューとそのコマンドが表示されます。  
  
 このチュートリアルでは、Visual Studio のメニューバーのメニューにサブメニューを作成し、サブメニューに新しいコマンドを配置します。 このチュートリアルでは、新しいコマンドも実装しています。  
  
## <a name="prerequisites"></a>前提条件  
 Visual Studio 2015 以降では、ダウンロードセンターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップでオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「 [Visual STUDIO SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。  
  
## <a name="adding-a-submenu-to-a-menu"></a>サブメニューのメニューへの追加  
  
1. 「 [Visual Studio のメニューバーにメニューを追加](../extensibility/adding-a-menu-to-the-visual-studio-menu-bar.md) する」の手順に従って、プロジェクトとメニュー項目を作成します。 このチュートリアルの手順では、VSIX プロジェクトの名前がであることを前提として `TopLevelMenu` います。  
  
2. TestCommandPackage. vsct を開きます。 セクションで、サブ `<Symbols>` `<IDSymbol>` メニューの要素、サブメニューグループ、および `<GuidSymbol>` "guidTopLevelMenuCmdSet" という名前のノード内のコマンドの要素を追加します。 これは、 `<IDSymbol>` トップレベルメニューの要素を含むノードと同じです。  
  
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
  
     親の GUID/ID ペアは、メニューを [Visual Studio のメニューバーに追加する](../extensibility/adding-a-menu-to-the-visual-studio-menu-bar.md)ときに生成されたメニューグループを指定し、トップレベルメニューの子です。  
  
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
  
## <a name="adding-a-command"></a>コマンドの追加  
  
1. TestCommand.cs を開き、既存のコマンド ID の後に次のコマンド ID を追加します。  
  
    ```csharp  
    public const int cmdidTestSubCmd = 0x105;  
    ```  
  
2. サブコマンドを追加します。 コマンドコンストラクターを検索します。 メソッドの呼び出しの直後に、次の行を追加し `AddCommand` ます。  
  
    ```csharp  
    CommandID subCommandID = new CommandID(CommandSet, (int)TestCommandPackageGuids.cmdidTestSubCmd);  
    MenuCommand subItem = new MenuCommand(  
        new EventHandler(SubItemCallback), subCommandID);  
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
                    MenuCommand subItem = new MenuCommand(  
                        new EventHandler(SubItemCallback), subCommandID);  
                    commandService.AddCommand(subItem);  
                }  
    ```  
  
3. SubItemCallback () を追加します。 これは、サブメニューの新しいコマンドがクリックされたときに呼び出されるメソッドです。  
  
    ```csharp  
    private void SubItemCallback(object sender, EventArgs e)  
    {  
        IVsUIShell uiShell = (IVsUIShell)this.ServiceProvider.GetService(  
            typeof(SVsUIShell));  
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
  
## <a name="see-also"></a>参照  
 [Visual Studio のメニューバーへのメニューの追加](../extensibility/adding-a-menu-to-the-visual-studio-menu-bar.md)   
 [コマンド、メニュー、およびツール バー](../extensibility/internals/commands-menus-and-toolbars.md)
