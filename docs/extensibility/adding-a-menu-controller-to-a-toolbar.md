---
title: ツールバーへのメニューコントローラの追加 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- toolbars [Visual Studio], adding menu controllers
- menus, adding menu controllers to toolbars
- menu controllers, adding to toolbars
ms.assetid: 6af9b0b4-037f-404c-bb40-aaa1970768ea
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d4dcb9e51f6633476a8f0eadea30da513e5ef760
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80740318"
---
# <a name="add-a-menu-controller-to-a-toolbar"></a>メニュー コントローラをツールバーに追加する
このチュートリアルでは、[ツール ウィンドウへのツール バーの追加](../extensibility/adding-a-toolbar-to-a-tool-window.md)に関するチュートリアルを参照し、ツール ウィンドウのツール バーにメニュー コントローラーを追加する方法を示します。 ここに示す手順は、ツールバーの追加のチュートリアルで作成した[ツールバーにも](../extensibility/adding-a-toolbar.md)適用できます。

メニュー コントローラは分割コントロールです。 メニュー コントローラの左側には最後に使用したコマンドが表示され、クリックして実行できます。 メニュー コントローラの右側は矢印で、クリックすると追加コマンドの一覧が表示されます。 一覧のコマンドをクリックすると、コマンドが実行され、メニュー コントローラの左側のコマンドが置き換えられます。 このように、メニュー コントローラは、常に最後に使用したコマンドを一覧から表示するコマンド ボタンのように動作します。

メニュー コントローラはメニューに表示できますが、ツールバーで最もよく使用されます。

## <a name="prerequisites"></a>必須コンポーネント
Visual Studio 2015 以降では、ダウンロード センターから Visual Studio SDK をインストールしません。 これは、Visual Studio のセットアップのオプション機能として含まれています。 VS SDK は後でインストールすることもできます。 詳細については、「 [Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-a-menu-controller"></a>メニュー コントローラを作成する

1. ツールバーを持つツール ウィンドウを作成するには、「[ツール ウィンドウにツール バーを追加する](../extensibility/adding-a-toolbar-to-a-tool-window.md)」で説明されている手順に従います。

2. の*TWTestCommandPackage.vsct*[シンボル] セクションに移動します。 guidSymbol 要素で**guidTWTestCommandPackageCmdSet**を宣言するメニュー コント ローラー、メニュー コント ローラー グループ、および 3 つのメニュー項目。

    ```xml
    <IDSymbol name="TestMenuController" value="0x1300" /><IDSymbol name="TestMenuControllerGroup" value="0x1060" /><IDSymbol name="cmdidMCItem1" value="0x0130" /><IDSymbol name="cmdidMCItem2" value="0x0131" /><IDSymbol name="cmdidMCItem3" value="0x0132" />
    ```

3. メニューセクションで、最後のメニューエントリの後に、メニューコントローラをメニューとして定義します。

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

    最後`TextChanges`に`TextIsAnchorCommand`選択したコマンドを反映するようにメニュー コントローラを有効にするには、 および フラグを含める必要があります。

4. [グループ] セクションで、最後のグループ エントリの後にメニュー コントローラ グループを追加します。

    ```xml
    <Group guid="guidTWTestCommandPackageCmdSet" id="TestMenuControllerGroup" priority="0x000">
        <Parent guid="guidTWTestCommandPackageCmdSet" id="TestMenuController" />
    </Group>
    ```

    メニュー コントローラを親として設定すると、このグループに配置されたコマンドはメニュー コントローラに表示されます。 属性`priority`は省略され、メニュー コントローラの唯一のグループであるため、既定値の 0 に設定されます。

5. [ボタン] セクションで、最後のボタン エントリの後に、各メニュー項目の Button 要素を追加します。

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

6. この時点で、メニュー コントローラを見ることができます。 プロジェクトをビルドし、デバッグを開始します。 実験用インスタンスが表示されます。

   1. [**表示/ その他のウィンドウ**] メニューで、[**テスト ツール ウィンドウ**] を開きます。

   2. メニュー コントローラがツール ウィンドウのツール バーに表示されます。

   3. メニュー コントローラの右側にある矢印をクリックすると、3 つのコマンドが表示されます。

      コマンドをクリックすると、メニュー コントローラのタイトルが変更され、そのコマンドが表示されます。 次のセクションでは、これらのコマンドをアクティブにするコードを追加します。

## <a name="implement-the-menu-controller-commands"></a>メニュー コントローラ コマンドを実装する

1. *TWTestCommandPackageGuids.cs*で、既存のコマンド ID の後に 3 つのメニュー項目のコマンド ID を追加します。

    ```csharp
    public const int cmdidMCItem1 = 0x130;
    public const int cmdidMCItem2 = 0x131;
    public const int cmdidMCItem3 = 0x132;
    ```

2. *TWTestCommand.cs*で、クラスの先頭に次のコードを追加`TWTestCommand`します。

    ```csharp
    private int currentMCCommand; // The currently selected menu controller command
    ```

3. TWTestCommand コンストラクターで、`AddCommand`メソッドの最後の呼び出しの後に、同じハンドラーを使用して各コマンドのイベントをルーティングするコードを追加します。

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

4. イベント ハンドラーを**TWTestCommand**クラスに追加して、選択したコマンドをチェックマークします。

    ```csharp
    private void OnMCItemQueryStatus(object sender, EventArgs e)
    {
        OleMenuCommand mc = sender as OleMenuCommand;
        if (null != mc)
        {
            mc.Checked = (mc.CommandID.ID == this.currentMCCommand);
        }
    }
    ```

5. ユーザーがメニュー コントローラーのコマンドを選択したときに MessageBox を表示するイベント ハンドラーを追加します。

    ```csharp
    private void OnMCItemClicked(object sender, EventArgs e)
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

## <a name="testing-the-menu-controller"></a>メニュー コントローラのテスト

1. プロジェクトをビルドし、デバッグを開始します。 実験用インスタンスが表示されます。

2. **[表示/ その他**のウィンドウ] メニューの **[テスト ツール]** ウィンドウを開きます。

    メニュー コントローラはツール ウィンドウのツールバーに表示され **、MC 項目 1**が表示されます。

3. 矢印の左側にあるメニュー コントローラ ボタンをクリックします。

    3 つの項目が表示され、最初の項目が選択され、アイコンの周りにハイライト ボックスが表示されます。 [MC**アイテム 3]** をクリックします。

    **メニュー コントローラの項目 3 を選択した**メッセージが表示されたダイアログ ボックスが表示されます。 メッセージがメニュー コントローラ ボタンのテキストに対応していることに注目してください。 メニュー コントローラ ボタンに**MC 項目 3**が表示されるようになりました。

## <a name="see-also"></a>関連項目
- [ツール ウィンドウへのツールバーの追加](../extensibility/adding-a-toolbar-to-a-tool-window.md)
- [ツールバーの追加](../extensibility/adding-a-toolbar.md)
