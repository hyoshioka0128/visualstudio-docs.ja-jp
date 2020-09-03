---
title: Visual Studio のメニューバーにメニューを追加する |Microsoft Docs
ms.date: 3/16/2019
ms.topic: how-to
helpviewer_keywords:
- menus, creating top level
- top-level menus
ms.assetid: 58fc1a31-2aeb-441c-8e48-c7d5cbcfe501
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 3eb5afbbe688c15f429054d50210a68769173e73
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "88801855"
---
# <a name="add-a-menu-to-the-visual-studio-menu-bar"></a>メニューを Visual Studio のメニューバーに追加する

このチュートリアルでは、Visual Studio 統合開発環境 (IDE) のメニューバーにメニューを追加する方法について説明します。 IDE のメニューバーには、[ **ファイル**]、[ **編集**]、[ **表示**]、[ **ウィンドウ**]、[ **ヘルプ**] などのメニューカテゴリがあります。

新しいメニューを Visual Studio のメニューバーに追加する前に、コマンドを既存のメニュー内に配置するかどうかを検討してください。 コマンドの配置の詳細については、「 [Visual Studio のメニューとコマンド](../extensibility/ux-guidelines/menus-and-commands-for-visual-studio.md)」を参照してください。

メニューは、プロジェクトの *vsct* ファイルで宣言されています。 メニューおよび *. vsct* ファイルの詳細については、「 [コマンド、メニュー、およびツールバー](../extensibility/internals/commands-menus-and-toolbars.md)」を参照してください。

このチュートリアルを完了すると、1つのコマンドを含む [ **Test Menu]** という名前のメニューを作成できます。

:::moniker range=">=vs-2019"
> [!NOTE]
> Visual Studio 2019 以降では、拡張機能によって提供されるトップレベルのメニューが [ **拡張** ] メニューに配置されます。
:::moniker-end

## <a name="prerequisites"></a>前提条件

Visual Studio 2015 以降では、ダウンロードセンターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップでオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「 [Visual STUDIO SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-a-vsix-project-that-has-a-custom-command-item-template"></a>カスタムコマンド項目テンプレートを持つ VSIX プロジェクトを作成する

1. という名前の VSIX プロジェクトを作成 `TopLevelMenu` します。 VSIX プロジェクトテンプレートは、"vsix" を検索することで、[ **新しいプロジェクト** ] ダイアログで見つけることができます。  詳細については、「 [メニューコマンドを使用して拡張機能を作成](../extensibility/creating-an-extension-with-a-menu-command.md)する」を参照してください。

::: moniker range="vs-2017"

2. プロジェクトが開いたら、 **Testcommand**という名前のカスタムコマンド項目テンプレートを追加します。 **ソリューションエクスプローラー**で、プロジェクトノードを右クリックし、[新しい項目の**追加**] を選択し  >   **New Item**ます。 [ **新しい項目の追加** ] ダイアログで、[ **Visual C#]/[拡張機能** ] にアクセスし、[ **カスタムコマンド**] を選択します。 ウィンドウの下部にある [ **名前** ] フィールドで、[コマンドファイル名] を *TestCommand.cs*に変更します。

::: moniker-end

::: moniker range=">=vs-2019"

2. プロジェクトが開いたら、 **Testcommand**という名前のカスタムコマンド項目テンプレートを追加します。 **ソリューションエクスプローラー**で、プロジェクトノードを右クリックし、[新しい項目の**追加**] を選択し  >   **New Item**ます。 [ **新しい項目の追加** ] ダイアログで、[ **Visual C#]/[拡張機能** ] にアクセスし、[ **コマンド**] を選択します。 ウィンドウの下部にある [ **名前** ] フィールドで、[コマンドファイル名] を *TestCommand.cs*に変更します。

::: moniker-end

## <a name="create-a-menu-on-the-ide-menu-bar"></a>IDE のメニューバーにメニューを作成する

::: moniker range="vs-2017"

1. **ソリューションエクスプローラー**で、 *testcommandpackage. vsct*を開きます。

    ファイルの末尾には、複数のノードを `<Symbols>` 含むノードがあり `<GuidSymbol>` ます。 という名前のノードに、次のように `guidTestCommandPackageCmdSet` 新しいシンボルを追加します。

   ```xml
   <IDSymbol name="TopLevelMenu" value="0x1021"/>
   ```

2. ノードの直前に `<Menus>` 、空 `<Commands>` のノードを作成 `<Groups>` します。 ノードで、次のように `<Menus>` ノードを追加し `<Menu>` ます。

   ```xml
   <Menus>
         <Menu guid="guidTestCommandPackageCmdSet" id="TopLevelMenu" priority="0x700" type="Menu">
           <Parent guid="guidSHLMainMenu"
                   id="IDG_VS_MM_TOOLSADDINS" />
           <Strings>
             <ButtonText>Test Menu</ButtonText>
           </Strings>
       </Menu>
   </Menus>
   ```

    メニューのおよびの値は、コマンドセット `guid` `id` と、コマンドセット内の特定のメニューを指定します。

    [ツール] メニューと [アドイン] メニューを `guid` `id` 含む、Visual Studio のメニューバーのセクションにある親の位置の値と値。

    要素は、 `<ButtonText>` テキストがメニュー項目に表示されることを指定します。

3. セクションで `<Groups>` 、を見つけて、追加した `<Group>` `<Parent>` メニューを指すように要素を変更します。

   ```xml
   <Groups>
       <Group guid="guidTestCommandPackageCmdSet" id="MyMenuGroup" priority="0x0600">
           <Parent guid="guidTestCommandPackageCmdSet" id="TopLevelMenu"/>
       </Group>
   </Groups>
   ```

    これにより、グループが新しいメニューに追加されます。

::: moniker-end

::: moniker range=">=vs-2019"

1. **ソリューションエクスプローラー**で、 *TopLevelMenuPackage*を開きます。

    ファイルの末尾には、複数のノードを `<Symbols>` 含むノードがあり `<GuidSymbol>` ます。 という名前のノードに、次のように `guidTopLevelMenuPackageCmdSet` 新しいシンボルを追加します。

   ```xml
   <IDSymbol name="TopLevelMenu" value="0x1021"/>
   ```

2. ノードの直前に `<Menus>` 、空 `<Commands>` のノードを作成 `<Groups>` します。 ノードで、次のように `<Menus>` ノードを追加し `<Menu>` ます。

   ```xml
   <Menus>
         <Menu guid="guidTopLevelMenuPackageCmdSet" id="TopLevelMenu" priority="0x700" type="Menu">
           <Parent guid="guidSHLMainMenu"
                   id="IDG_VS_MM_TOOLSADDINS" />
           <Strings>
             <ButtonText>Test Menu</ButtonText>
           </Strings>
       </Menu>
   </Menus>
   ```

    メニューのおよびの値は、コマンドセット `guid` `id` と、コマンドセット内の特定のメニューを指定します。

    [ツール] メニューと [アドイン] メニューを `guid` `id` 含む、Visual Studio のメニューバーのセクションにある親の位置の値と値。

    要素は、 `<ButtonText>` テキストがメニュー項目に表示されることを指定します。

3. セクションで `<Groups>` 、を見つけて、追加した `<Group>` `<Parent>` メニューを指すように要素を変更します。

   ```xml
   <Groups>
       <Group guid="guidTopLevelMenuPackageCmdSet" id="MyMenuGroup" priority="0x0600">
           <Parent guid="guidTopLevelMenuPackageCmdSet" id="TopLevelMenu"/>
       </Group>
   </Groups>
   ```

    これにより、グループが新しいメニューに追加されます。

::: moniker-end

4. セクションで、 `<Buttons>` ノードを見つけ `<Button>` ます。 次に、 `<Strings>` ノードで要素をに変更し `<ButtonText>` `Test Command` ます。

    パッケージテンプレートによって、 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 親がに設定された要素が生成されていることに注意して `Button` `MyMenuGroup` ください。 その結果、このコマンドがメニューに表示されます。

## <a name="build-and-test-the-extension"></a>拡張機能をビルドしてテストする

1. プロジェクトをビルドし、デバッグを開始します。 実験用インスタンスのインスタンスが表示されます。

::: moniker range="vs-2017"

2. 実験用インスタンスのメニューバーには、 **[テスト] メニュー** メニューが含まれている必要があります。

::: moniker-end

::: moniker range=">=vs-2019"

2. 実験用インスタンスの [ **拡張機能** ] メニューには、 **[テスト] メニュー** メニューが含まれている必要があります。

::: moniker-end

3. [ **テスト] メニュー** メニューで、[ **テストコマンド**] を選択します。

    メッセージボックスが表示され、"TestCommand in TopLevelMenu ()" というメッセージが表示されます。

## <a name="see-also"></a>関連項目

- [コマンド、メニュー、およびツールバー](../extensibility/internals/commands-menus-and-toolbars.md)
