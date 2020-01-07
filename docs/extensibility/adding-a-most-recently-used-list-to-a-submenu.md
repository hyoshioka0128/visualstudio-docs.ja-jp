---
title: 最近使用した一覧のサブメニューへの追加 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- MRU lists
- menus, creating MRU list
- most recently used
ms.assetid: 27d4bbcf-99b1-498f-8b66-40002e3db0f8
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6eb32f81947f7359f5912e8a558e8df5002a0b80
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66352406"
---
# <a name="add-a-most-recently-used-list-to-a-submenu"></a>最近使用した一覧のサブメニューへの追加します。
このチュートリアルのデモに基づいて[メニューにサブメニューを追加](../extensibility/adding-a-submenu-to-a-menu.md)し、サブメニューに動的な一覧を追加する方法を示しています。 動的な一覧は、最近使用 (MRU) の一覧を作成するための基礎を形成します。

動的メニュー リストは、メニュー上のプレース ホルダーで始まります。 たびに、メニューを表示すると、Visual Studio 統合開発環境 (IDE) が、プレース ホルダーに表示されるすべてのコマンド、VSPackage を要求します。 動的な一覧は、メニューの任意の場所に発生します。 ただし、動的なリストは通常格納されているし、またはメニューの下部にあるサブメニューには、単独で表示されます。 これらの設計パターンを使用すると、展開し、その他のコマンド メニューの位置に影響を与えずに縮小するためのコマンドの動的リストを有効にします。 このチュートリアルでは、サブメニューの残りの部分から 1 行で区切られた、既存のサブメニューの下部にある動的 MRU 一覧が表示されます。

技術的には、動的な一覧は、ツールバーにも適用できます。 ただし、ユーザーが特定の手順を変更しない限りツールバーを変更する必要がありますされませんので、その使用状況お勧めします。

このチュートリアルは、MRU 一覧の順序を変更するたびにそれらの 1 つが選択されている 4 つの項目を作成します (選択したアイテムは、一覧の先頭に移動します)。

メニューの詳細については、 *.vsct*ファイルを参照してください[コマンド、メニューのおよびツールバー](../extensibility/internals/commands-menus-and-toolbars.md)します。

## <a name="prerequisites"></a>必須コンポーネント
このチュートリアルに従うには、Visual Studio SDK をインストールする必要があります。 詳細については、次を参照してください。 [Visual Studio SDK](../extensibility/visual-studio-sdk.md)します。

## <a name="create-an-extension"></a>拡張機能を作成します。

- 次の手順では、[サブメニューのメニューに追加](../extensibility/adding-a-submenu-to-a-menu.md)で、次の手順が変更されるサブメニューを作成します。

  このチュートリアルの手順では、VSPackage の名前があると仮定`TopLevelMenu`で使用される名前である[Visual Studio のメニュー バーにメニューを追加](../extensibility/adding-a-menu-to-the-visual-studio-menu-bar.md)します。

## <a name="create-a-dynamic-item-list-command"></a>動的アイテム一覧のコマンドを作成します。

1. 開いている*TestCommandPackage.vsct*します。

2. `Symbols`セクションで、 `GuidSymbol` guidTestCommandPackageCmdSet、という名前のノード追加のシンボル、`MRUListGroup`グループと`cmdidMRUList`コマンドを次のようにします。

    ```csharp
    <IDSymbol name="MRUListGroup" value="0x1200"/>
    <IDSymbol name="cmdidMRUList" value="0x0200"/>
    ```

3. `Groups`セクションで、既存のグループのエントリの後に宣言されたグループを追加します。

    ```cpp
    <Group guid="guidTestCommandPackageCmdSet" id="MRUListGroup"
            priority="0x0100">
        <Parent guid="guidTestCommandPackageCmdSet" id="SubMenu"/>
    </Group>

    ```

4. `Buttons`セクションで、ボタンの既存のエントリの後に新しく宣言のコマンドを表すノードを追加します。

    ```csharp
    <Button guid="guidTestCommandPackageCmdSet" id="cmdidMRUList"
        type="Button" priority="0x0100">
        <Parent guid="guidTestCommandPackageCmdSet" id="MRUListGroup" />
        <CommandFlag>DynamicItemStart</CommandFlag>
        <Strings>
            <CommandName>cmdidMRUList</CommandName>
            <ButtonText>MRU Placeholder</ButtonText>
        </Strings>
    </Button>
    ```

    `DynamicItemStart`フラグを動的に生成するコマンドを使用できます。

5. プロジェクトをビルドし、新しいコマンドの表示をテストするデバッグを開始します。

    **TestMenu**  メニューの 新規作成 のサブメニューをクリックします。**サブメニュー**新しいのコマンドを表示するには、 **MRU のプレース ホルダー**します。 コマンドの動的 MRU 一覧が次の手順で実装されるは、そのリストで毎回、サブメニューが開かれているときに、このコマンドのラベルが置き換えられます。

## <a name="filling-the-mru-list"></a>MRU 一覧を入力

1. *TestCommandPackageGuids.cs*、既存のコマンド Id の後に次の行を追加、`TestCommandPackageGuids`クラスの定義。

    ```csharp
    public const string guidTestCommandPackageCmdSet = "00000000-0000-0000-0000-00000000"; // get the GUID from the .vsct file
    public const uint cmdidMRUList = 0x200;
    ```

2. *TestCommand.cs*次を追加するステートメントを使用します。

    ```csharp
    using System.Collections;
    ```

3. AddCommand の最後の呼び出し後、TestCommand コンス トラクターで、次のコードを追加します。 `InitMRUMenu`後で定義されています。

    ```csharp
    this.InitMRUMenu(commandService);
    ```

4. TestCommand クラスでは、次のコードを追加します。 このコードでは、MRU 一覧に表示される項目を表す文字列のリストを初期化します。

    ```csharp
    private int numMRUItems = 4;
    private int baseMRUID = (int)TestCommandPackageGuids.cmdidMRUList;
    private ArrayList mruList;

    private void InitializeMRUList()
    {
        if (null == this.mruList)
        {
            this.mruList = new ArrayList();
            if (null != this.mruList)
            {
                for (int i = 0; i < this.numMRUItems; i++)
                {
                    this.mruList.Add(string.Format(CultureInfo.CurrentCulture,
                        "Item {0}", i + 1));
                }
            }
        }
    }
    ```

5. 後に、`InitializeMRUList`メソッドを追加、`InitMRUMenu`メソッド。 これには、MRU 一覧のメニュー コマンドを初期化します。

    ```csharp
    private void InitMRUMenu(OleMenuCommandService mcs)
    {
        InitializeMRUList();
        for (int i = 0; i < this.numMRUItems; i++)
        {
            var cmdID = new CommandID(
                new Guid(TestCommandPackageGuids.guidTestCommandPackageCmdSet), this.baseMRUID + i);
            var mc = new OleMenuCommand(
                new EventHandler(OnMRUExec), cmdID);
            mc.BeforeQueryStatus += new EventHandler(OnMRUQueryStatus);
            mcs.AddCommand(mc);
        }
    }
    ```

    MRU 一覧にすべての可能な項目のメニュー コマンド オブジェクトを作成する必要があります。 IDE の呼び出し、`OnMRUQueryStatus`がこれ以上項目までの MRU 一覧の各項目のメソッド。 マネージ コードでは、ide がこれ以上項目があることを知る唯一の方法は、最初使用可能なすべての項目を作成します。 使用して追加の項目を非表示としてが最初にマークでくする場合は、`mc.Visible = false;`メニュー コマンドを作成した後。 これらの項目から表示できる以降を使用して`mc.Visible = true;`で、`OnMRUQueryStatus`メソッド。

6. 後に、`InitMRUMenu`メソッドでは、次の追加`OnMRUQueryStatus`メソッド。 これは、MRU の各項目のテキストを設定するハンドラーです。

    ```csharp
    private void OnMRUQueryStatus(object sender, EventArgs e)
    {
        OleMenuCommand menuCommand = sender as OleMenuCommand;
        if (null != menuCommand)
        {
            int MRUItemIndex = menuCommand.CommandID.ID - this.baseMRUID;
            if (MRUItemIndex >= 0 && MRUItemIndex < this.mruList.Count)
            {
                menuCommand.Text = this.mruList[MRUItemIndex] as string;
            }
        }
    }
    ```

7. 後に、`OnMRUQueryStatus`メソッドでは、次の追加`OnMRUExec`メソッド。 これは、最近使用した項目を選択するためのハンドラーです。 このメソッドは、選択した項目を一覧の先頭に移動し、メッセージ ボックスに、選択した項目が表示されます。

    ```csharp
    private void OnMRUExec(object sender, EventArgs e)
    {
        var menuCommand = sender as OleMenuCommand;
        if (null != menuCommand)
        {
            int MRUItemIndex = menuCommand.CommandID.ID - this.baseMRUID;
            if (MRUItemIndex >= 0 && MRUItemIndex < this.mruList.Count)
            {
                string selection = this.mruList[MRUItemIndex] as string;
                for (int i = MRUItemIndex; i > 0; i--)
                {
                    this.mruList[i] = this.mruList[i - 1];
                }
                this.mruList[0] = selection;
                System.Windows.Forms.MessageBox.Show(
                    string.Format(CultureInfo.CurrentCulture,
                                  "Selected {0}", selection));
            }
        }
    }

    ```

## <a name="testing-the-mru-list"></a>MRU 一覧のテスト

1. プロジェクトをビルドし、デバッグを開始します。

2. **TestMenu**  メニューのをクリックして**呼び出す TestCommand**します。 これを行うには、コマンドが選択されていることを示すメッセージ ボックスが表示されます。

    > [!NOTE]
    > この手順は、読み込みし、正しく MRU 一覧を表示するには、VSPackage を強制的に必要です。 この手順をスキップする場合は、MRU 一覧は表示されません。

3. **テスト メニュー**  メニューのをクリックして**サブメニュー**します。 4 つの項目の一覧は、区切り記号の下のサブメニューの最後に表示されます。 クリックすると**項目 3**、メッセージ ボックスが表示され、テキストを表示する必要があります**選択項目 3**します。 (4 つの項目の一覧が表示されない場合確保のため、前の手順の指示に従っていること。)

4. サブメニューをもう一度開きます。 注意して**項目 3**一覧の上部にあるようになり、1 つ下の他の項目がプッシュされました。 をクリックして**項目 3**もう一度と、メッセージ ボックスが表示されることがわかります**選択項目 3**テキストがコマンドのラベルと共に新しい位置に移動が正しくことを示します。

## <a name="see-also"></a>関連項目
- [メニュー項目を動的に追加します。](../extensibility/dynamically-adding-menu-items.md)
