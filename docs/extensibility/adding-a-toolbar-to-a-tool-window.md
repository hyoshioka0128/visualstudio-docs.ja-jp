---
title: ツールウィンドウへのツールバーの追加 |Microsoft Docs
description: 'Visual Studio 統合開発環境 (IDE: integrated development environment) のツールウィンドウにコマンドにバインドされているボタンを含むツールバーを追加する方法について説明します。'
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- tool windows, adding toolbars
- toolbars [Visual Studio], adding to tool windows
ms.assetid: 172f64b3-87f8-4292-9c1c-65bffa2b0970
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 1847801ed9dcbb1b7c7145c86b1998b54e2bb5d9
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105055792"
---
# <a name="add-a-toolbar-to-a-tool-window"></a>ツールウィンドウにツールバーを追加する
このチュートリアルでは、ツールウィンドウにツールバーを追加する方法について説明します。

 ツールバーは、コマンドにバインドされたボタンを含む、水平または垂直のストリップです。 ツールウィンドウのツールバーの長さは、ツールバーがドッキングされている場所に応じて、ツールウィンドウの幅または高さと常に同じです。

 IDE のツールバーとは異なり、ツールウィンドウのツールバーはドッキングされている必要があり、移動またはカスタマイズすることはできません。 VSPackage が umanaged 切れのコードで記述されている場合、ツールバーは任意の端にドッキングできます。

 ツールバーを追加する方法の詳細については、「 [ツールバーの追加](../extensibility/adding-a-toolbar.md)」を参照してください。

## <a name="prerequisites"></a>前提条件
 Visual Studio 2015 以降では、ダウンロードセンターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップでオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「 [Visual STUDIO SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-a-toolbar-for-a-tool-window"></a>ツールウィンドウのツールバーを作成する

1. `TWToolbar` **Twtestcommand** という名前のメニューコマンドと **TestToolWindow** という名前のツールウィンドウの両方を持つという名前の VSIX プロジェクトを作成します。 詳細については、「 [メニューコマンドを使用して拡張機能を作成](../extensibility/creating-an-extension-with-a-menu-command.md) する」および「 [ツールウィンドウで拡張機能を作成](../extensibility/creating-an-extension-with-a-tool-window.md)する」を参照してください。 ツールウィンドウテンプレートを追加する前に、コマンド項目テンプレートを追加する必要があります。

2. *Twtestcommandpackage. vsct* で、[シンボル] セクションを探します。 Guidtwtestcommand蔵書 Ecmdset という GuidSymbol ノードで、次のようにツールバーとツールバーグループを宣言します。

    ```xml
    <IDSymbol name="TWToolbar" value="0x1000" />
    <IDSymbol name="TWToolbarGroup" value="0x1050" />
    ```

3. セクションの上部で `Commands` 、セクションを作成 `Menus` します。 要素を追加し `Menu` て、ツールバーを定義します。

    ```xml
    <Menus>
        <Menu guid="guidTWTestCommandPackageCmdSet" id="TWToolbar" type="ToolWindowToolbar">
            <CommandFlag>DefaultDocked</CommandFlag>
            <Strings>
                <ButtonText>Test Toolbar</ButtonText>
                <CommandName>Test Toolbar</CommandName>
            </Strings>
        </Menu>
    </Menus>
    ```

     ツールバーは、サブメニューのように入れ子にすることはできません。 したがって、親を割り当てる必要はありません。 また、ユーザーはツールバーを移動できるため、優先度を設定する必要はありません。 通常、ツールバーの最初の配置はプログラムによって定義されますが、ユーザーによるその後の変更は保持されます。

4. [グループ] セクションで、ツールバーのコマンドを含むグループを定義します。

    ```xml

    <Group guid="guidTWTestCommandPackageCmdSet" id="TWToolbarGroup" priority="0x0000">
        <Parent guid="guidTWTestCommandPackageCmdSet" id="TWToolbar" />
    </Group>
    ```

5. [ボタン] セクションで、既存の Button 要素の親をツールバーグループに変更して、ツールバーが表示されるようにします。

    ```xml
    <Button guid="guidTWTestCommandPackageCmdSet" id="TWTestCommandId" priority="0x0100" type="Button">
        <Parent guid="guidTWTestCommandPackageCmdSet" id="TWToolbarGroup" />
        <Icon guid="guidImages" id="bmpPic1" />
        <Strings>
            <ButtonText>Invoke TWTestCommand</ButtonText>
        </Strings>
    </Button>
    ```

     既定では、ツールバーにコマンドがない場合、ツールバーは表示されません。

     ツールウィンドウに新しいツールバーが自動的に追加されないため、ツールバーを明示的に追加する必要があります。 これについては、次のセクションで説明します。

## <a name="add-the-toolbar-to-the-tool-window"></a>ツールウィンドウにツールバーを追加する

1. *Twtestcommandpackageguids .cs* で、次の行を追加します。

    ```csharp
    public const string guidTWTestCommandPackageCmdSet = "00000000-0000-0000-0000-0000";  // get the GUID from the .vsct file
    public const int TWToolbar = 0x1000;
    ```

2. *TestToolWindow* で、次の using ステートメントを追加します。

    ```csharp
    using System.ComponentModel.Design;
    ```

3. TestToolWindow コンストラクターで、次の行を追加します。

    ```csharp
    this.ToolBar = new CommandID(new Guid(TWTestCommandPackageGuids.guidTWTestCommandPackageCmdSet), TWTestCommandPackageGuids.TWToolbar);
    ```

## <a name="test-the-toolbar-in-the-tool-window"></a>ツールウィンドウのツールバーをテストする

1. プロジェクトをビルドし、デバッグを開始します。 Visual Studio の実験用インスタンスが表示されます。

2. [表示] メニューの [ **その他のウィンドウ** ] メニューで、[ **テスト ToolWindow** ] をクリックしてツールウィンドウを表示します。

     ツールウィンドウの左上にあるツールバー (既定のアイコン) が、タイトルのすぐ下に表示されます。

3. ツールバーで、アイコンをクリックして、 **Twtestcommandpackage 内に Twtestcommandpackage というメッセージを表示します。 TWTestCommand. MenuItemCallback ()**。

## <a name="see-also"></a>こちらもご覧ください
- [ツールバーの追加](../extensibility/adding-a-toolbar.md)
