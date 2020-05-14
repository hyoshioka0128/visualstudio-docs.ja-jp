﻿---
title: 最近使用した一覧のサブメニューへの追加 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- MRU lists
- menus, creating MRU list
- most recently used
ms.assetid: 27d4bbcf-99b1-498f-8b66-40002e3db0f8
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: cf389c0da7ec0aafb6e47dae8f09ffdc3b1d1e4d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80740301"
---
# <a name="add-a-most-recently-used-list-to-a-submenu"></a>最近使用したリストをサブメニューに追加する
このチュートリアルでは、「[サブメニューをメニューに追加する](../extensibility/adding-a-submenu-to-a-menu.md)」のデモンストレーションを基に、サブメニューに動的リストを追加する方法を示します。 動的リストは、最近使用された (MRU) リストを作成するための基礎となります。

動的メニューリストは、メニューのプレースホルダから始まります。 メニューが表示されるたびに、Visual Studio 統合開発環境 (IDE) は、プレースホルダーに表示されるすべてのコマンドを VSPackage に要求します。 動的リストは、メニューの任意の場所に表示されます。 ただし、動的リストは通常、サブメニューまたはメニューの下部に自身で保存され、表示されます。 これらの設計パターンを使用すると、メニュー上の他のコマンドの位置に影響を与えることなく、コマンドの動的リストを展開および縮小できます。 このチュートリアルでは、動的 MRU リストは、サブメニューの残りの部分と線で区切られた既存のサブメニューの下部に表示されます。

技術的には、動的リストをツールバーに適用することもできます。 ただし、ユーザーが変更する特定の手順を実行しない限り、ツールバーは変更されないままにする必要があるため、この使用は推奨しません。

このチュートリアルでは、1 つの項目が選択されるたびに順序を変更する 4 つの項目の MRU リストを作成します (選択した項目はリストの先頭に移動します)。

メニューと *.vsct*ファイルの詳細については、「[コマンド、メニュー、およびツール バー](../extensibility/internals/commands-menus-and-toolbars.md)」を参照してください。

## <a name="prerequisites"></a>必須コンポーネント
このチュートリアルを行うには、Visual Studio SDK をインストールする必要があります。 詳細については、「 [Visual Studio SDK](../extensibility/visual-studio-sdk.md)」を参照してください。

## <a name="create-an-extension"></a>拡張機能を作成する

- [メニューへのサブメニューの追加](../extensibility/adding-a-submenu-to-a-menu.md)の手順に従って、次の手順で変更するサブメニューを作成します。

  このチュートリアルの手順では、VSPackage`TopLevelMenu`の名前が[、Visual Studio メニュー バーにメニューを追加](../extensibility/adding-a-menu-to-the-visual-studio-menu-bar.md)で使用される名前であることを前提としています。

## <a name="create-a-dynamic-item-list-command"></a>動的な項目一覧コマンドを作成する

1. *を*開きます。

2. `Symbols`セクションの guidTestCommandPackageCmdSet という名前の`GuidSymbol`ノードに、次のようにグループと`MRUListGroup`コマンドのシンボル`cmdidMRUList`を追加します。

    ```csharp
    <IDSymbol name="MRUListGroup" value="0x1200"/>
    <IDSymbol name="cmdidMRUList" value="0x0200"/>
    ```

3. セクションで`Groups`、既存のグループエントリの後に宣言されたグループを追加します。

    ```cpp
    <Group guid="guidTestCommandPackageCmdSet" id="MRUListGroup"
            priority="0x0100">
        <Parent guid="guidTestCommandPackageCmdSet" id="SubMenu"/>
    </Group>

    ```

4. セクションで`Buttons`、既存のボタン エントリの後に、新しく宣言されたコマンドを表すノードを追加します。

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

    この`DynamicItemStart`フラグを使用すると、コマンドを動的に生成できます。

5. プロジェクトをビルドし、デバッグを開始して、新しいコマンドの表示をテストします。

    **[TestMenu] メニュー**で、新しいサブメニューの **[サブメニュー]** をクリックして、新しいコマンドである**MRU プレースホルダ**を表示します。 次の手順でコマンドの動的 MRU リストが実装された後、サブメニューが開かれるたびに、このコマンド・ラベルがそのリストに置き換えられます。

## <a name="filling-the-mru-list"></a>MRU リストの入力

1. *TestCommandPackageGuids.cs*で、クラス定義の既存のコマンド ID の後に次`TestCommandPackageGuids`の行を追加します。

    ```csharp
    public const string guidTestCommandPackageCmdSet = "00000000-0000-0000-0000-00000000"; // get the GUID from the .vsct file
    public const uint cmdidMRUList = 0x200;
    ```

2. *TestCommand.cs*に次の using ステートメントを追加します。

    ```csharp
    using System.Collections;
    ```

3. 最後の AddCommand 呼び出しの後に、TestCommand コンストラクターに次のコードを追加します。 は`InitMRUMenu`後で定義されます。

    ```csharp
    this.InitMRUMenu(commandService);
    ```

4. クラスに次のコードを追加します。 このコードは、MRU リストに表示される項目を表す文字列のリストを初期化します。

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

5. メソッドの`InitializeMRUList`後にメソッドを`InitMRUMenu`追加します。 これにより、MRU リスト メニュー コマンドが初期化されます。

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

    MRU リスト内の可能な項目ごとに、メニュー コマンド オブジェクトを作成する必要があります。 IDE は、`OnMRUQueryStatus`項目がなくなるまで、MRU リスト内の各項目のメソッドを呼び出します。 マネージ コードでは、IDE が項目がなくなったことを認識する唯一の方法は、すべての可能な項目を最初に作成することです。 必要に応じて、メニュー コマンドの作成後に使用`mc.Visible = false;`して、追加項目を最初に表示しないように設定できます。 これらの項目は、`mc.Visible = true;``OnMRUQueryStatus`メソッドで後で表示できます。

6. メソッドの`InitMRUMenu`後に、次`OnMRUQueryStatus`のメソッドを追加します。 これは、各 MRU 項目のテキストを設定するハンドラーです。

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

7. メソッドの`OnMRUQueryStatus`後に、次`OnMRUExec`のメソッドを追加します。 MRU 項目を選択するためのハンドラです。 このメソッドは、選択した項目をリストの先頭に移動し、選択した項目をメッセージ ボックスに表示します。

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

## <a name="testing-the-mru-list"></a>MRU リストのテスト

1. プロジェクトをビルドし、デバッグを開始します。

2. [**テスト メニュー] メニューの**[**テスト コマンドの呼び出し**] をクリックします。 これにより、コマンドが選択されたことを示すメッセージ ボックスが表示されます。

    > [!NOTE]
    > この手順は、VSPackage を強制的に読み込み、MRU リストを正しく表示するために必要です。 このステップをスキップすると、MRU リストは表示されません。

3. [**テスト メニュー] メニュー**の [サブ**メニュー]** をクリックします。 4 つの項目のリストは、区切り記号の下のサブメニューの最後に表示されます。 **[項目 3]** をクリックすると、メッセージ ボックスが表示され **、"選択された項目 3"** というテキストが表示されます。 (4 つの項目の一覧が表示されない場合は、前の手順の手順に従っていることを確認してください)。

4. サブメニューを再度開きます。 項目**3**がリストの先頭に表示され、他の項目が 1 つ下の位置に押し下げられていたことに注目してください。 **[項目 3]** をもう一度クリックすると、メッセージ ボックスに **[選択された項目 3]** と表示され、テキストがコマンド ラベルと共に新しい位置に正しく移動したことを示します。

## <a name="see-also"></a>関連項目
- [メニュー項目の動的な追加](../extensibility/dynamically-adding-menu-items.md)
