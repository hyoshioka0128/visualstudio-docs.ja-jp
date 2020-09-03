---
title: 最近使用した一覧をサブメニューに追加する |Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
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
ms.openlocfilehash: 3f73f948befc7665ecc3a40f816389bfaae8e4fd
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85904201"
---
# <a name="add-a-most-recently-used-list-to-a-submenu"></a>最近使用した一覧をサブメニューに追加する
このチュートリアルは、「 [メニューにサブ](../extensibility/adding-a-submenu-to-a-menu.md)メニューを追加する」のデモを基にしており、サブメニューに動的リストを追加する方法を示しています。 動的リストは、最近使用した (MRU) リストを作成するための基礎となります。

動的メニューリストは、メニューのプレースホルダーから始まります。 メニューが表示されるたびに、Visual Studio 統合開発環境 (IDE: integrated development environment) によって、プレースホルダーに表示されるすべてのコマンドが VSPackage に要求されます。 動的リストは、メニュー上の任意の場所で実行できます。 ただし、動的な一覧は通常、サブメニューやメニューの下部に格納されて表示されます。 これらの設計パターンを使用すると、メニュー上の他のコマンドの位置に影響を与えずに、コマンドの動的リストを拡張およびコントラクトすることができます。 このチュートリアルでは、既存のサブメニューの一番下に動的 MRU リストが表示されます。これは、サブメニューの残りの部分から、行によって区切られています。

技術的には、動的リストをツールバーに適用することもできます。 ただし、ツールバーが変更されないようにするには、ユーザーが特定の手順を実行する必要があります。

このチュートリアルでは、4つの項目のいずれかが選択されるたびに順序を変更する MRU リストを作成します (選択した項目が一覧の一番上に移動します)。

メニューおよび *. vsct* ファイルの詳細については、「 [コマンド、メニュー、およびツールバー](../extensibility/internals/commands-menus-and-toolbars.md)」を参照してください。

## <a name="prerequisites"></a>前提条件
このチュートリアルを行うには、Visual Studio SDK をインストールする必要があります。 詳細については、「 [Visual STUDIO SDK](../extensibility/visual-studio-sdk.md)」を参照してください。

## <a name="create-an-extension"></a>拡張機能を作成する

- 「 [メニューにサブ](../extensibility/adding-a-submenu-to-a-menu.md) メニューを追加する」の手順に従って、次の手順で変更されるサブメニューを作成します。

  このチュートリアルの手順では、VSPackage の名前がであることを前提としています。これは、 `TestCommand` [Visual Studio のメニューバーに [メニューの追加](../extensibility/adding-a-menu-to-the-visual-studio-menu-bar.md)] で使用される名前です。

## <a name="create-a-dynamic-item-list-command"></a>動的な項目リストの作成コマンド

1. *Testcommandpackage. vsct*を開きます。

2. セクションで、 `Symbols` `GuidSymbol` Guidtestcommand蔵書 Ecmdset という名前のノードのグループとコマンドのシンボルを次のように追加し `MRUListGroup` `cmdidMRUList` ます。

    ```xml
    <IDSymbol name="MRUListGroup" value="0x1200"/>
    <IDSymbol name="cmdidMRUList" value="0x0200"/>
    ```

3. セクションで `Groups` 、宣言されたグループを既存のグループエントリの後に追加します。

    ```xml
    <Group guid="guidTestCommandPackageCmdSet" id="MRUListGroup"
            priority="0x0100">
        <Parent guid="guidTestCommandPackageCmdSet" id="SubMenu"/>
    </Group>
    ```

4. セクションで、新しく宣言された `Buttons` コマンドを表すノードを既存のボタンエントリの後に追加します。

    ```xml
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

    `DynamicItemStart`フラグを使用すると、コマンドを動的に生成できます。

5. プロジェクトをビルドし、デバッグを開始して、新しいコマンドの表示をテストします。

    [ **Testmenu** ] メニューの [new] サブ **メニュー (サブメニュー**) をクリックして、新しいコマンドである **MRU プレースホルダー**を表示します。 次の手順で動的 MRU のコマンド一覧が実装されたら、サブメニューが開かれるたびに、このコマンドラベルがそのリストに置き換えられます。

## <a name="filling-the-mru-list"></a>MRU リストの入力

1. *TestCommandPackageGuids.cs*で、クラス定義の既存のコマンド id の後に次の行を追加し `TestCommandPackageGuids` ます。

    ```csharp
    public const string guidTestCommandPackageCmdSet = "00000000-0000-0000-0000-00000000"; // get the GUID from the .vsct file
    public const uint cmdidMRUList = 0x200;
    ```

2. *TestCommand.cs*で、次の using ステートメントを追加します。

    ```csharp
    using System.Collections;
    ```

3. 最後の AddCommand 呼び出しの後に、TestCommand コンストラクターに次のコードを追加します。 は `InitMRUMenu` 後で定義されます

    ```csharp
    this.InitMRUMenu(commandService);
    ```

4. TestCommand クラスに次のコードを追加します。 このコードは、MRU リストに表示される項目を表す文字列のリストを初期化します。

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

5. メソッドの後 `InitializeMRUList` に、メソッドを追加し `InitMRUMenu` ます。 これにより、MRU リストメニューコマンドが初期化されます。

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

    MRU 一覧に表示されるすべての項目に対して、メニューコマンドオブジェクトを作成する必要があります。 IDE は、 `OnMRUQueryStatus` 項目がなくなるまで、MRU リストの各項目に対してメソッドを呼び出します。 マネージコードでは、これ以上項目がないことを IDE が確認する唯一の方法は、可能なすべての項目を最初に作成することです。 必要に応じて、 `mc.Visible = false;` メニューコマンドが作成された後でを使用して、追加の項目を最初に非表示にすることができます。 これらの項目は、後でメソッドでを使用して表示でき `mc.Visible = true;` `OnMRUQueryStatus` ます。

6. メソッドの後 `InitMRUMenu` に、次のメソッドを追加し `OnMRUQueryStatus` ます。 これは、各 MRU 項目のテキストを設定するハンドラーです。

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

7. メソッドの後 `OnMRUQueryStatus` に、次のメソッドを追加し `OnMRUExec` ます。 これは、MRU 項目を選択するためのハンドラーです。 このメソッドは、選択した項目を一覧の一番上に移動し、選択した項目をメッセージボックスに表示します。

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

2. [ **Testmenu] メニュー** の [ **Testmenu の呼び出し**] をクリックします。 この操作を実行すると、コマンドが選択されたことを示すメッセージボックスが表示されます。

    > [!NOTE]
    > この手順は、VSPackage に MRU リストを読み込んで正しく表示するために必要です。 この手順を省略した場合、MRU の一覧は表示されません。

3. [ **テスト] メニュー** メニューの [ **サブメニュー**] をクリックします。 サブメニューの末尾の区切り記号の下に、4つの項目の一覧が表示されます。 **項目 3**をクリックすると、メッセージボックスが表示され、**選択項目 3**というテキストが表示されます。 (4 つの項目の一覧が表示されない場合は、前の手順の指示に従っていることを確認してください)。

4. もう一度サブメニューを開きます。 **項目 3**がリストの一番上にあり、他の項目が1つ下に移動されていることを確認します。 もう一度 **項目 3** をクリックすると、メッセージボックスにはまだ **選択された項目 3**が表示されます。これは、テキストがコマンドラベルと共に新しい位置に正しく移動したことを示しています。

## <a name="see-also"></a>関連項目
- [動的にメニュー項目を追加する](../extensibility/dynamically-adding-menu-items.md)
