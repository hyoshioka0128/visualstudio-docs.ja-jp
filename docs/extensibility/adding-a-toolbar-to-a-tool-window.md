---
title: ツール ウィンドウへのツールバーの追加 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- tool windows, adding toolbars
- toolbars [Visual Studio], adding to tool windows
ms.assetid: 172f64b3-87f8-4292-9c1c-65bffa2b0970
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 094515eb94279623974bd7b55cc9923c49625a70
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80740247"
---
# <a name="add-a-toolbar-to-a-tool-window"></a>ツール ウィンドウにツール バーを追加する
このチュートリアルでは、ツール ウィンドウにツール バーを追加する方法を示します。

 ツールバーは、コマンドにバインドされたボタンを含む水平または垂直のストリップです。 ツール ウィンドウのツール バーの長さは、ツール バーのドッキング位置に応じて、常にツール ウィンドウの幅または高さと同じです。

 IDE のツールバーとは異なり、ツール ウィンドウのツールバーはドッキングする必要があり、移動やカスタマイズはできません。 VSPackage が umanaged コードで記述されている場合、ツール バーは任意の端にドッキングできます。

 ツールバーの追加方法の詳細については、「ツールバーの[追加](../extensibility/adding-a-toolbar.md)」を参照してください。

## <a name="prerequisites"></a>必須コンポーネント
 Visual Studio 2015 以降では、ダウンロード センターから Visual Studio SDK をインストールしません。 これは、Visual Studio のセットアップのオプション機能として含まれています。 VS SDK は後でインストールすることもできます。 詳細については、「 [Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-a-toolbar-for-a-tool-window"></a>ツール ウィンドウのツールバーを作成する

1. **TWTestCommand**という`TWToolbar`名前のメニュー コマンドと**TestToolWindow**という名前のツール ウィンドウの両方を持つ名前の VSIX プロジェクトを作成します。 詳細については、「メニュー[コマンドを使用した拡張機能の作成](../extensibility/creating-an-extension-with-a-menu-command.md)」および「[ツール ウィンドウを使用した拡張機能の作成](../extensibility/creating-an-extension-with-a-tool-window.md)」を参照してください。 ツール ウィンドウ テンプレートを追加する前に、コマンド項目テンプレートを追加する必要があります。

2. [*シンボル*] セクションを探します。 guidSymbol ノードで名前を付けて、次のように、ツール バーとツール バー グループを宣言します。

    ```xml
    <IDSymbol name="TWToolbar" value="0x1000" />
    <IDSymbol name="TWToolbarGroup" value="0x1050" />
    ```

3. セクションの上部に`Commands`セクションを`Menus`作成します。 ツールバーを`Menu`定義する要素を追加します。

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

     ツールバーはサブメニューのようにネストすることはできません。 したがって、親を割り当てる必要はありません。 また、ユーザーはツールバーを移動できるため、優先度を設定する必要はありません。 通常、ツール バーの初期配置はプログラムによって定義されますが、ユーザーによる以降の変更は保持されます。

4. [グループ] セクションで、ツールバーのコマンドを含むグループを定義します。

    ```xml

    <Group guid="guidTWTestCommandPackageCmdSet" id="TWToolbarGroup" priority="0x0000">
        <Parent guid="guidTWTestCommandPackageCmdSet" id="TWToolbar" />
    </Group>
    ```

5. [ボタン] セクションで、既存の Button 要素の親をツール バー グループに変更し、ツールバーが表示されるようにします。

    ```xml
    <Button guid="guidTWTestCommandPackageCmdSet" id="TWTestCommandId" priority="0x0100" type="Button">
        <Parent guid="guidTWTestCommandPackageCmdSet" id="TWToolbarGroup" />
        <Icon guid="guidImages" id="bmpPic1" />
        <Strings>
            <ButtonText>Invoke TWTestCommand</ButtonText>
        </Strings>
    </Button>
    ```

     既定では、ツールバーにコマンドがない場合は表示されません。

     新しいツール バーはツール ウィンドウに自動的に追加されないため、ツール バーを明示的に追加する必要があります。 これについては、次のセクションで説明します。

## <a name="add-the-toolbar-to-the-tool-window"></a>ツール ウィンドウにツール バーを追加する

1. *TWTestCommandPackageGuids.cs*に次の行を追加します。

    ```csharp
    public const string guidTWTestCommandPackageCmdSet = "00000000-0000-0000-0000-0000";  // get the GUID from the .vsct file
    public const int TWToolbar = 0x1000;
    ```

2. *TestToolWindow.cs*に次の using ステートメントを追加します。

    ```csharp
    using System.ComponentModel.Design;
    ```

3. コンストラクタで次の行を追加します。

    ```csharp
    this.ToolBar = new CommandID(new Guid(TWTestCommandPackageGuids.guidTWTestCommandPackageCmdSet), TWTestCommandPackageGuids.TWToolbar);
    ```

## <a name="test-the-toolbar-in-the-tool-window"></a>ツール ウィンドウでツール バーをテストする

1. プロジェクトをビルドし、デバッグを開始します。 Visual Studio の実験用インスタンスが表示されます。

2. [**表示/ その他のウィンドウ**] メニューで、[**ツール ウィンドウのテスト**] をクリックしてツール ウィンドウを表示します。

     ツール ウィンドウの左上、タイトルのすぐ下にツールバー (既定のアイコン) が表示されます。

3. ツール バーでアイコンをクリックして、メッセージ**TWTestCommand パッケージを表示**します。

## <a name="see-also"></a>関連項目
- [ツールバーを追加する](../extensibility/adding-a-toolbar.md)
