---
title: ツールバーを追加する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- toolbars [Visual Studio], adding to IDE
- IDE, adding toolbars
ms.assetid: 17302c25-6f59-4e97-8c85-54f95336a07f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 655cd87fe59cf4f42361cc24a63eb56653caae1a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80740219"
---
# <a name="add-a-toolbar"></a>ツールバーの追加
このチュートリアルでは、ツール バーを Visual Studio IDE に追加する方法を示します。

 ツールバーは、コマンドにバインドされたボタンを含む水平または垂直のストリップです。 IDE の実装に応じて、IDE のツールバーを再配置したり、メインの IDE ウィンドウの任意の側にドッキングしたり、他のウィンドウの前面に表示したりできます。

 また、ユーザーは [**ユーザー設定]** ダイアログ ボックスを使用して、ツールバーにコマンドを追加したり、ツールバーからコマンドを削除したりできます。 通常、VSPackages のツール バーはユーザーがカスタマイズできます。 IDE はすべてのカスタマイズを処理し、VSPackage はコマンドに応答します。 VSPackage は、コマンドが物理的に配置されている場所を知る必要はありません。

 メニューの詳細については、「[コマンド、メニュー、およびツールバー](../extensibility/internals/commands-menus-and-toolbars.md)」を参照してください。

## <a name="prerequisites"></a>必須コンポーネント
 Visual Studio 2015 以降では、ダウンロード センターから Visual Studio SDK をインストールしません。 これは、Visual Studio のセットアップのオプション機能として含まれています。 VS SDK は後でインストールすることもできます。 詳細については、「 [Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-an-extension-with-a-toolbar"></a>ツールバーを使用して拡張機能を作成する
 という名前`IDEToolbar`の VSIX プロジェクトを作成します。 という名前のメニュー コマンド項目テンプレート**を追加します**。 これを行う方法については、「[メニュー コマンドを使用して拡張機能を作成する」を](../extensibility/creating-an-extension-with-a-menu-command.md)参照してください。

## <a name="create-a-toolbar-for-the-ide"></a>IDE のツールバーを作成する

1. *ツール バーテストコマンドパッケージ.vsct*で、シンボルセクションを探します。 名前の Guid シンボル要素で、次のように、ツール バーとツール バー グループの宣言を追加します。

    ```xml
    <IDSymbol name="Toolbar" value="0x1000" />
    <IDSymbol name="ToolbarGroup" value="0x1050" />

    ```

2. [コマンド] セクションの上部に [メニュー] セクションを作成します。 メニュー要素をメニュー セクションに追加して、ツールバーを定義します。

    ```xml
    <Menus>
        <Menu guid="guidToolbarTestCommandPackageCmdSet" id="Toolbar"
            type="Toolbar" >
            <CommandFlag>DefaultDocked</CommandFlag>
            <Strings>
                <ButtonText>Test Toolbar</ButtonText>
                <CommandName>Test Toolbar</CommandName>
            </Strings>
          </Menu>
    </Menus>
    ```

     サブメニューのようにツールバーをネストすることはできません。 したがって、親グループを割り当てる必要はありません。 また、ユーザーがツールバーを移動できるため、優先順位を設定する必要はありません。 通常、ツール バーの初期配置はプログラムによって定義されますが、ユーザーによる以降の変更は保持されます。

3. [[グループ](../extensibility/groups-element.md)] セクションで、既存のグループ エントリの後に、ツールバーのコマンドを含む[Group](../extensibility/group-element.md)要素を定義します。

    ```xml
    <Group guid="guidToolbarTestCommandPackageCmdSet" id="ToolbarGroup"
          priority="0x0000">
      <Parent guid="guidToolbarTestCommandPackageCmdSet" id="Toolbar"/>
    </Group>
    ```

4. ボタンをツールバーに表示します。 [ボタン] セクションで、[ボタン] の [親] ブロックをツールバーに置き換えます。 結果のボタン ブロックは次のようになります。

    ```xml
    <Button guid="guidToolbarTestCommandPackageCmdSet" id="ToolbarTestCommandId" priority="0x0100" type="Button">
        <Parent guid= "guidToolbarTestCommandPackageCmdSet" id="ToolbarGroup" />
                <Icon guid="guidImages" id="bmpPic1" />
        <Strings>
            <ButtonText>Invoke ToolbarTestCommand</ButtonText>
        </Strings>
    </Button>
    ```

     既定では、ツールバーにコマンドがない場合は表示されません。

5. プロジェクトをビルドし、デバッグを開始します。 実験用インスタンスが表示されます。

6. Visual Studio のメニュー バーを右クリックして、ツール バーの一覧を表示します。 [**テスト ツール バー] を選択**します。

7. ツールバーが[ファイル内を検索]アイコンの右側にアイコンとして表示されます。 アイコンをクリックすると、というメッセージ ボックスが**表示されます。内部 IDE ツールバー.ツールバーテストコマンド.メニュー項目コールバック()** の内部。

## <a name="see-also"></a>関連項目
- [コマンド、メニュー、およびツールバー](../extensibility/internals/commands-menus-and-toolbars.md)
