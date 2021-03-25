---
title: ツールバーにメニューコントローラーを追加する |Microsoft Docs
description: メニューコントローラーを作成して Visual Studio のツールウィンドウツールバーに追加する方法について説明し、メニューコントローラーのコマンドを実装してテストします。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- toolbars [Visual Studio], adding menu controllers
- menus, adding menu controllers to toolbars
- menu controllers, adding to toolbars
ms.assetid: 6af9b0b4-037f-404c-bb40-aaa1970768ea
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 304f4ea11abc332c01603f96b6b67c0bd22e38c6
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105060069"
---
# <a name="add-a-menu-controller-to-a-toolbar"></a>ツールバーにメニューコントローラーを追加する
このチュートリアルは、「ツール [ウィンドウにツールウィンドウを追加する」](../extensibility/adding-a-toolbar-to-a-tool-window.md) チュートリアルに基づいており、ツールウィンドウのツールバーにメニューコントローラーを追加する方法を示しています。 ここに示す手順は、「 [ツールバーの追加](../extensibility/adding-a-toolbar.md) 」チュートリアルで作成したツールバーにも適用できます。

メニューコントローラーは分割コントロールです。 メニューコントローラーの左側には最後に使用したコマンドが表示され、それをクリックすると実行できます。 メニューコントローラーの右側は矢印です。これをクリックすると、追加のコマンドの一覧が表示されます。 一覧でコマンドをクリックすると、コマンドが実行され、メニューコントローラーの左側のコマンドが置き換えられます。 このようにして、メニューコントローラーは、一覧から最後に使用したコマンドを常に表示するコマンドボタンのように動作します。

メニューコントローラーはメニューに表示できますが、最も頻繁に使用されるのはツールバーです。

## <a name="prerequisites"></a>前提条件
Visual Studio 2015 以降では、ダウンロードセンターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップでオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「 [Visual STUDIO SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-a-menu-controller"></a>メニューコントローラーを作成する

1. 「ツール [ウィンドウにツールバーを追加](../extensibility/adding-a-toolbar-to-a-tool-window.md) する」で説明されている手順に従って、ツールバーを持つツールウィンドウを作成します。

2. *Twtestcommandpackage. vsct* で、[シンボル] セクションにアクセスします。 **Guidtwtestcommand整理 Ecmdset** という guidsymbol 要素で、メニューコントローラー、メニューコントローラーグループ、3つのメニュー項目を宣言します。

    ```xml
    <IDSymbol name="TestMenuController" value="0x1300" /><IDSymbol name="TestMenuControllerGroup" value="0x1060" /><IDSymbol name="cmdidMCItem1" value="0x0130" /><IDSymbol name="cmdidMCItem2" value="0x0131" /><IDSymbol name="cmdidMCItem3" value="0x0132" />
    ```

3. [メニュー] セクションで、最後のメニューエントリの後にメニューコントローラーをメニューとして定義します。

    ```xml
    <Menu guid="guidTWTestCommandPackageCmdSet" id="TestMenuController" priority="0x0100" type="MenuController">
        <Parent guid="guidTWTestCommandPackageCmdSet" id="TWToolbarGroup" />
        <CommandFlag>IconAndText</CommandFlag>
        <CommandFlag>TextChanges</CommandFlag>
        <CommandFlag>TextIsAnchorCommand</CommandFlag>
        <Strings>
            <ButtonText>Test Menu Controller</ButtonText>
            <CommandName>Test Menu Controller</CommandName>
        </Strings>
    </Menu>
    ```

    `TextChanges` `TextIsAnchorCommand` メニューコントローラーが最後に選択したコマンドを反映できるようにするには、フラグとフラグを含める必要があります。

4. [グループ] セクションで、最後のグループエントリの後にメニューコントローラーグループを追加します。

    ```xml
    <Group guid="guidTWTestCommandPackageCmdSet" id="TestMenuControllerGroup" priority="0x000">
        <Parent guid="guidTWTestCommandPackageCmdSet" id="TestMenuController" />
    </Group>
    ```

    メニューコントローラーを親として設定すると、このグループに配置されているすべてのコマンドがメニューコントローラーに表示されます。 `priority`属性が省略されています。これは、メニューコントローラー上の唯一のグループであるため、これを既定値の0に設定します。

5. [ボタン] セクションで、最後のボタンのエントリの後に、各メニュー項目の Button 要素を追加します。

    ```xml
    <Button guid="guidTWTestCommandPackageCmdSet" id="cmdidMCItem1" priority="0x0000" type="Button">
        <Parent guid="guidTWTestCommandPackageCmdSet" id="TestMenuControllerGroup" />
        <Icon guid="guidImages" id="bmpPic1" />
        <CommandFlag>IconAndText</CommandFlag>
        <Strings>
            <ButtonText>MC Item 1</ButtonText>
            <CommandName>MC Item 1</CommandName>
        </Strings>
    </Button>
    <Button guid="guidTWTestCommandPackageCmdSet" id="cmdidMCItem2" priority="0x0100" type="Button">
        <Parent guid="guidTWTestCommandPackageCmdSet" id="TestMenuControllerGroup" />
        <Icon guid="guidImages" id="bmpPic2" />
        <CommandFlag>IconAndText</CommandFlag>
        <Strings>
            <ButtonText>MC Item 2</ButtonText>
            <CommandName>MC Item 2</CommandName>
        </Strings>
    </Button>
    <Button guid="guidTWTestCommandPackageCmdSet" id="cmdidMCItem3" priority="0x0200" type="Button">
        <Parent guid="guidTWTestCommandPackageCmdSet" id="TestMenuControllerGroup" />
        <Icon guid="guidImages" id="bmpPicSearch" />
        <CommandFlag>IconAndText</CommandFlag>
        <Strings>
            <ButtonText>MC Item 3</ButtonText>
            <CommandName>MC Item 3</CommandName>
        </Strings>
    </Button>
    ```

6. この時点で、メニューコントローラーを見ることができます。 プロジェクトをビルドし、デバッグを開始します。 実験用のインスタンスが表示されます。

   1. [ **表示]/[その他のウィンドウ** ] メニューで、[ **テスト ToolWindow**] を開きます。

   2. ツールウィンドウのツールバーにメニューコントローラーが表示されます。

   3. メニューコントローラーの右側にある矢印をクリックすると、使用可能な3つのコマンドが表示されます。

      コマンドをクリックすると、メニューコントローラーのタイトルが変更され、そのコマンドが表示されることに注意してください。 次のセクションでは、これらのコマンドをアクティブにするコードを追加します。

## <a name="implement-the-menu-controller-commands"></a>メニューコントローラーのコマンドを実装する

1. *Twtestcommandpackageguids .cs* で、既存のコマンド id の後に3つのメニュー項目のコマンド id を追加します。

    ```csharp
    public const int cmdidMCItem1 = 0x130;
    public const int cmdidMCItem2 = 0x131;
    public const int cmdidMCItem3 = 0x132;
    ```

2. *Twtestcommand .cs* で、クラスの先頭に次のコードを追加します `TWTestCommand` 。

    ```csharp
    private int currentMCCommand; // The currently selected menu controller command
    ```

3. TWTestCommand コンストラクターで、メソッドの最後の呼び出しの後に `AddCommand` 、同じハンドラーを使用して各コマンドのイベントをルーティングするコードを追加します。

    ```csharp
    for (int i = TWTestCommandPackageGuids.cmdidMCItem1; i <=
        TWTestCommandPackageGuids.cmdidMCItem3; i++)
    {
        CommandID cmdID = new
        CommandID(new Guid(TWTestCommandPackageGuids.guidTWTestCommandPackageCmdSet), i);
        OleMenuCommand mc = new OleMenuCommand(new
          EventHandler(OnMCItemClicked), cmdID);
        mc.BeforeQueryStatus += new EventHandler(OnMCItemQueryStatus);
        commandService.AddCommand(mc);
        // The first item is, by default, checked. 
        if (TWTestCommandPackageGuids.cmdidMCItem1 == i)
        {
            mc.Checked = true;
            this.currentMCCommand = i;
        }
    }
    ```

4. **Twtestcommand** クラスにイベントハンドラーを追加して、選択したコマンドをチェック対象としてマークします。

    ```csharp
    private void OnMCItemQueryStatus(object sender, EventArgs e)
    {
        OleMenuCommand mc = sender as OleMenuCommand;
        if (null != mc)
        {
            mc.Checked = (mc.CommandID.ID == this.currentMCCommand);
        }
    }
    ```

5. ユーザーがメニューコントローラーでコマンドを選択したときにメッセージボックスを表示するイベントハンドラーを追加します。

    ```csharp
    private void OnMCItemClicked(object sender, EventArgs e)
    {
        OleMenuCommand mc = sender as OleMenuCommand;
        if (null != mc)
        {
            string selection;
            switch (mc.CommandID.ID)
            {
                case c.cmdidMCItem1:
                    selection = "Menu controller Item 1";
                    break;

                case TWTestCommandPackageGuids.cmdidMCItem2:
                    selection = "Menu controller Item 2";
                    break;

                case TWTestCommandPackageGuids.cmdidMCItem3:
                    selection = "Menu controller Item 3";
                    break;

                default:
                    selection = "Unknown command";
                    break;
            }
            this.currentMCCommand = mc.CommandID.ID;

            IVsUIShell uiShell =
              (IVsUIShell) ServiceProvider.GetService(typeof(SVsUIShell));
            Guid clsid = Guid.Empty;
            int result;
            uiShell.ShowMessageBox(
                    0,
                    ref clsid,
                    "Test Tool Window Toolbar Package",
                    string.Format(CultureInfo.CurrentCulture,
                                 "You selected {0}", selection),
                    string.Empty,
                    0,
                    OLEMSGBUTTON.OLEMSGBUTTON_OK,
                    OLEMSGDEFBUTTON.OLEMSGDEFBUTTON_FIRST,
                    OLEMSGICON.OLEMSGICON_INFO,
                    0,
                    out result);
        }
    }
    ```

## <a name="testing-the-menu-controller"></a>メニューコントローラーのテスト

1. プロジェクトをビルドし、デバッグを開始します。 実験用のインスタンスが表示されます。

2. [**表示]/[その他のウィンドウ**] メニューで **テスト ToolWindow** を開きます。

    ツールウィンドウのツールバーにメニューコントローラーが表示され、 **MC 項目 1** が表示されます。

3. 矢印の左側にあるメニューコントローラーのボタンをクリックします。

    3つの項目が表示されます。最初の項目が選択されており、そのアイコンの周りに強調表示ボックスがあります。 [ **MC 項目 3**] をクリックします。

    ダイアログボックスが開き、 **[メニューコントローラー項目 3]** というメッセージが表示されます。 メッセージがメニューコントローラーボタンのテキストに対応することに注意してください。 メニューコントローラーボタンに **MC 項目 3** が表示されるようになりました。

## <a name="see-also"></a>こちらもご覧ください
- [ツールウィンドウへのツールバーの追加](../extensibility/adding-a-toolbar-to-a-tool-window.md)
- [ツールバーの追加](../extensibility/adding-a-toolbar.md)
