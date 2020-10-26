---
title: メニューバーへのメニューの追加 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- menus, creating top level
- top-level menus
ms.assetid: 58fc1a31-2aeb-441c-8e48-c7d5cbcfe501
caps.latest.revision: 52
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 64ab627d785e8b00b5159969a01dc1102df30359
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68184924"
---
# <a name="adding-a-menu-to-the-visual-studio-menu-bar"></a>Visual Studio のメニュー バーへのメニューの追加
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このチュートリアルでは、Visual Studio 統合開発環境 (IDE) のメニューバーにメニューを追加する方法について説明します。 IDE のメニューバーには、[ **ファイル**]、[ **編集**]、[ **表示**]、[ **ウィンドウ**]、[ **ヘルプ**] などのメニューカテゴリがあります。

 新しいメニューを Visual Studio のメニューバーに追加する前に、コマンドを既存のメニュー内に配置するかどうかを検討してください。 コマンドの配置の詳細については、「 [Visual Studio のメニューとコマンド](../extensibility/ux-guidelines/menus-and-commands-for-visual-studio.md)」を参照してください。

 メニューは、プロジェクトの vsct ファイルで宣言されています。 メニューおよび. vsct ファイルの詳細については、「 [コマンド、メニュー、およびツールバー](../extensibility/internals/commands-menus-and-toolbars.md)」を参照してください。

 このチュートリアルを完了すると、1つのコマンドを含む **Testmenu** という名前のメニューを作成できます。

## <a name="prerequisites"></a>必須コンポーネント
 Visual Studio 2015 以降では、ダウンロードセンターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップでオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「 [Visual STUDIO SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="creating-a-vsix-project-that-has-a-custom-command-item-template"></a>カスタムコマンド項目テンプレートを持つ VSIX プロジェクトを作成する

1. という名前の VSIX プロジェクトを作成 `TopLevelMenu` します。 VSIX プロジェクトテンプレートは、[**新しいプロジェクト**] ダイアログボックスの [ **Visual C#** の  /  **機能拡張**] の下に表示されます。  詳細については、「 [メニューコマンドを使用した拡張機能の作成](../extensibility/creating-an-extension-with-a-menu-command.md)」を参照してください。

2. プロジェクトが開いたら、 **Testcommand**という名前のカスタムコマンド項目テンプレートを追加します。 **ソリューションエクスプローラー**で、プロジェクトノードを右クリックし、[追加]、[**新しい項目**] の順に選択します。 [ **新しい項目の追加** ] ダイアログで、[ **Visual C#]/[拡張機能** ] にアクセスし、[ **カスタムコマンド**] を選択します。 ウィンドウの下部にある [ **名前** ] フィールドで、[コマンドファイル名] を **TestCommand.cs**に変更します。

## <a name="creating-a-menu-on-the-ide-menu-bar"></a>IDE のメニューバーにメニューを作成する

#### <a name="to-create-a-menu"></a>メニューを作成するには

1. **ソリューションエクスプローラー**で、TestCommandPackage. vsct を開きます。

     ファイルの末尾には、複数のノードを \<Symbols> 含むノードがあり \<GuidSymbol> ます。 Guidtestcommand蔵書 Ecmdset という名前のノードで、次のように新しいシンボルを追加します。

    ```xml
    <IDSymbol name="TopLevelMenu" value="0x1021"/>
    ```

2. ノードの直前に \<Menus> 、空 \<Commands> のノードを作成 \<Groups> します。 ノードで、次のように \<Menus> ノードを追加し \<Menu> ます。

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

     メニューのおよびの値は、コマンドセット `guid` `id` と、コマンドセット内の特定のメニューを指定します。

     [ツール] メニューと [アドイン] メニューを `guid` `id` 含む、Visual Studio のメニューバーのセクションにある親の位置の値と値。

     文字列の値は、 `CommandName` テキストがメニュー項目に表示されることを指定します。

3. セクションで \<Groups> 、を見つけて、追加した \<Group> \<Parent> メニューを指すように要素を変更します。

    ```csharp
    <Groups>
          <Group guid="guidTestCommandPackageCmdSet" id="MyMenuGroup" priority="0x0600">
            <Parent guid="guidTestCommandPackageCmdSet" id="TopLevelMenu"/>
          </Group>
        </Groups>
    ```

     これにより、グループが新しいメニューに追加されます。

4. セクション `Buttons` を探します。 パッケージテンプレートによって、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 親がに設定された要素が生成されていることに注意して `Button` `MyMenuGroup` ください。 その結果、このコマンドがメニューに表示されます。

## <a name="building-and-testing-the-extension"></a>拡張機能のビルドとテスト

1. プロジェクトをビルドし、デバッグを開始します。 実験用インスタンスのインスタンスが表示されます。

2. 実験用インスタンスのメニューバーには、 **Testmenu** メニューが含まれている必要があります。

3. [ **Testmenu] メニュー** の [ **Test コマンドの呼び出し**] をクリックします。

     メッセージボックスが表示され、"TestCommand Package in TopLevelMenu ()" というメッセージが表示されます。 これは、新しいコマンドが動作することを示します。

## <a name="see-also"></a>参照
 [コマンド、メニュー、およびツール バー](../extensibility/internals/commands-menus-and-toolbars.md)
