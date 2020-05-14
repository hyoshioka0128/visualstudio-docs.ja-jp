---
title: メニューを Visual Studio のメニュー バーに追加する |マイクロソフトドキュメント
ms.date: 3/16/2019
ms.topic: conceptual
helpviewer_keywords:
- menus, creating top level
- top-level menus
ms.assetid: 58fc1a31-2aeb-441c-8e48-c7d5cbcfe501
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 91e5a6e1714dbb87abc67fbf722c3bbd1a194a5b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80740312"
---
# <a name="add-a-menu-to-the-visual-studio-menu-bar"></a>メニューを Visual Studio のメニュー バーに追加する

このチュートリアルでは、Visual Studio 統合開発環境 (IDE) のメニュー バーにメニューを追加する方法を示します。 IDE のメニュー バーには、**ファイル**、**編集**、**表示**、ウィンドウ、**ヘルプ**などのメニュー カテゴリ**があります**。

Visual Studio のメニュー バーに新しいメニューを追加する前に、コマンドを既存のメニュー内に配置するかどうかを検討してください。 コマンドの配置の詳細については、「 [Visual Studio のメニューとコマンド」を](../extensibility/ux-guidelines/menus-and-commands-for-visual-studio.md)参照してください。

メニューはプロジェクトの *.vsct*ファイルで宣言されます。 メニューと *.vsct*ファイルの詳細については、「[コマンド、メニュー、およびツール バー](../extensibility/internals/commands-menus-and-toolbars.md)」を参照してください。

このチュートリアルを完了すると、1 つのコマンドを含む**TestMenu**という名前のメニューを作成できます。

> [!NOTE]
> VS 2019 では、拡張機能によって提供される最上位のメニューが**拡張機能**メニューの下に配置されます。

## <a name="prerequisites"></a>必須コンポーネント

Visual Studio 2015 以降では、ダウンロード センターから Visual Studio SDK をインストールしません。 これは、Visual Studio のセットアップのオプション機能として含まれています。 VS SDK は後でインストールすることもできます。 詳細については、「 [Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-a-vsix-project-that-has-a-custom-command-item-template"></a>カスタム コマンド項目テンプレートを持つ VSIX プロジェクトを作成する

1. という名前`TopLevelMenu`の VSIX プロジェクトを作成します。 VSIX プロジェクト テンプレートは、"vsix" を検索して **[新しいプロジェクト**] ダイアログで見つけることができます。  詳細については、「[メニュー コマンドを使用して拡張機能を作成する](../extensibility/creating-an-extension-with-a-menu-command.md)」を参照してください。

2. プロジェクトが開いたら、 **TestCommand**という名前のカスタム コマンド項目テンプレートを追加します。 ソリューション**エクスプローラ**で、プロジェクト ノードを右クリックし、[**Add** >  **新しい項目**の追加] を選択します。 [**新しい項目の追加]** ダイアログで **、[Visual C# / 拡張性**] に移動し、[カスタム**コマンド**] を選択します。 ウィンドウの下部にある [**名前]** フィールドで、コマンド ファイル名を *[TestCommand.cs*に変更します。

## <a name="create-a-menu-on-the-ide-menu-bar"></a>IDE メニューバーにメニューを作成する

::: moniker range="vs-2017"

1. **ソリューション エクスプローラー**で *、テスト コマンド パッケージ.vsct*を開きます。

    ファイルの末尾には、いくつかの\<\<GuidSymbol> ノードを含むシンボル>ノードがあります。 という名前のノードで、次のように新しいシンボルを追加します。

   ```xml
   <IDSymbol name="TopLevelMenu" value="0x1021"/>
   ```

2. [グループ]>ノードで[> グループ]ノードを\<作成>。 \< \< [メニュー \<> ノードで、次\<のようにメニュー> ノードを追加します。

   ```xml
   <Menus>
         <Menu guid="guidTestCommandPackageCmdSet" id="TopLevelMenu" priority="0x700" type="Menu">
           <Parent guid="guidSHLMainMenu"
                   id="IDG_VS_MM_TOOLSADDINS" />
           <Strings>
             <ButtonText>TestMenu</ButtonText>
             <CommandName>TestMenu</CommandName>
           </Strings>
       </Menu>
   </Menus>
   ```

    メニュー`guid`の`id`と の値は、コマンド セットとコマンド セット内の特定のメニューを指定します。

    親`guid`の`id`と の値は、Visual Studio メニュー バーの [ツール] メニューと [アドイン] メニューを含むセクションにメニューを配置します。

    文字列の値は`CommandName`、テキストがメニュー項目に表示されることを指定します。

3. [\<グループ>] セクションで、[\<グループ]>を\<見つけ、親>要素を変更して、追加したメニューをポイントします。

   ```csharp
   <Groups>
         <Group guid="guidTestCommandPackageCmdSet" id="MyMenuGroup" priority="0x0600">
           <Parent guid="guidTestCommandPackageCmdSet" id="TopLevelMenu"/>
         </Group>
       </Groups>
   ```

    これにより、グループが新しいメニューの一部になります。

::: moniker-end

::: moniker range=">=vs-2019"

1. **ソリューション エクスプローラー**で *、トップレベル メニュー パッケージを開きます*。

    ファイルの末尾には、いくつかの\<\<GuidSymbol> ノードを含むシンボル>ノードがあります。 名前のノードで、次のように新しいシンボルを追加します。

   ```xml
   <IDSymbol name="TopLevelMenu" value="0x1021"/>
   ```

2. [グループ]>ノードで[> グループ]ノードを\<作成>。 \< \< [メニュー \<> ノードで、次\<のようにメニュー> ノードを追加します。

   ```xml
   <Menus>
         <Menu guid="guidTopLevelMenuPackageCmdSet" id="TopLevelMenu" priority="0x700" type="Menu">
           <Parent guid="guidSHLMainMenu"
                   id="IDG_VS_MM_TOOLSADDINS" />
           <Strings>
             <ButtonText>TestMenu</ButtonText>
             <CommandName>TestMenu</CommandName>
           </Strings>
       </Menu>
   </Menus>
   ```

    メニュー`guid`の`id`と の値は、コマンド セットとコマンド セット内の特定のメニューを指定します。

    親`guid`の`id`と の値は、Visual Studio メニュー バーの [ツール] メニューと [アドイン] メニューを含むセクションにメニューを配置します。

    文字列の値は`CommandName`、テキストがメニュー項目に表示されることを指定します。

3. [\<グループ>] セクションで、[\<グループ]>を\<見つけ、親>要素を変更して、追加したメニューをポイントします。

   ```csharp
   <Groups>
         <Group guid="guidTopLevelMenuPackageCmdSet" id="MyMenuGroup" priority="0x0600">
           <Parent guid="guidTopLevelMenuPackageCmdSet" id="TopLevelMenu"/>
         </Group>
       </Groups>
   ```

    これにより、グループが新しいメニューの一部になります。

::: moniker-end

4. セクション `Buttons` を探します。 パッケージ テンプレート[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]によって、親が`Button`に設定された要素が生成されたこと`MyMenuGroup`に注目してください。 その結果、このコマンドはメニューに表示されます。

## <a name="build-and-test-the-extension"></a>拡張機能のビルドとテスト

1. プロジェクトをビルドし、デバッグを開始します。 実験用インスタンスのインスタンスが表示されます。

::: moniker range="vs-2017"

2. 実験用インスタンスのメニューバーには **、TestMenu**メニューが含まれている必要があります。

::: moniker-end

::: moniker range=">=vs-2019"

2. 実験用インスタンスの **[拡張機能**] メニューには **、TestMenu メニュー**が含まれている必要があります。

::: moniker-end

3. [**テスト メニュー] メニューの**[**テスト コマンドの呼び出し**] をクリックします。

     メッセージ ボックスが表示され、"トップレベルメニュー内のテスト コマンド パッケージ.TestCommand.MenuItemCallback()" というメッセージが表示されます。

## <a name="see-also"></a>関連項目

- [コマンド、メニュー、およびツールバー](../extensibility/internals/commands-menus-and-toolbars.md)
