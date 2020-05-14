---
title: ソリューション エクスプローラーのツール バーにコマンドを追加する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- toolbars [Visual Studio], adding buttons
- buttons [Visual Studio], adding to Solution Explorer
- Solution Explorer, adding buttons
ms.assetid: f6411557-2f4b-4e9f-b02e-fce12a6ac7e9
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 44a14d87fbb5754d7af35d3add9e438351877a49
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80740341"
---
# <a name="add-a-command-to-the-solution-explorer-toolbar"></a>ソリューション エクスプローラーのツール バーにコマンドを追加する
このチュートリアルでは、**ソリューション エクスプローラー**のツール バーにボタンを追加する方法について説明します。

 ツール バーまたはメニューのコマンドは、Visual Studio のボタンと呼ばれます。 ボタンがクリックされると、コマンド ハンドラーのコードが実行されます。 通常、関連するコマンドはグループ化されて 1 つのグループになります。 メニューまたはツールバーは、グループのコンテナとして機能します。 優先度は、グループ内の個々のコマンドがメニューまたはツールバーに表示される順序を決定します。 ボタンの表示を制御することで、ツールバーまたはメニューにボタンが表示されないようにすることができます。 `<VisibilityConstraints>` *.vsct*ファイルのセクションにリストされているコマンドは、関連するコンテキストにのみ表示されます。 グループに表示設定を適用できません。

 メニュー、ツール バー コマンド、および *.vsct*ファイルの詳細については、「[コマンド、メニュー、およびツール バー](../extensibility/internals/commands-menus-and-toolbars.md)」を参照してください。

> [!NOTE]
> コマンド テーブルの構成 (*.ctc*) ファイルの代わりに XML コマンド テーブル *(.vsct)* ファイルを使用して、VSPackages でのメニューとコマンドの表示方法を定義します。 詳細については[、「Visual Studio コマンド テーブル 」を参照してください。Vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)。

## <a name="prerequisites"></a>必須コンポーネント
 Visual Studio 2015 以降では、ダウンロード センターから Visual Studio SDK をインストールしません。 これは、Visual Studio のセットアップのオプション機能として含まれています。 VS SDK は後でインストールすることもできます。 詳細については、「 [Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-an-extension-with-a-menu-command"></a>メニュー コマンドを使用して拡張機能を作成する
 という名前`SolutionToolbar`の VSIX プロジェクトを作成します。 **ToolbarButton**という名前のメニュー コマンド項目テンプレートを追加します。 これを行う方法については、「[メニュー コマンドを使用して拡張機能を作成する」を](../extensibility/creating-an-extension-with-a-menu-command.md)参照してください。

## <a name="add-a-button-to-the-solution-explorer-toolbar"></a>ソリューション エクスプローラーのツール バーにボタンを追加する
 チュートリアルのこのセクションでは、**ソリューション エクスプローラー**のツール バーにボタンを追加する方法について説明します。 ボタンがクリックされると、コールバック メソッドのコードが実行されます。

1. ツール*バー ボタンパッケージ.vsct*ファイルで、`<Symbols>`セクションに移動します。 ノード`<GuidSymbol>`には、パッケージ テンプレートによって生成されたメニュー グループとコマンドが含まれています。 このノード`<IDSymbol>`に要素を追加して、コマンドを保持するグループを宣言します。

    ```xml
    <IDSymbol name="SolutionToolbarGroup" value="0x0190"/>
    ```

2. セクションで`<Groups>`、既存のグループエントリの後に、前のステップで宣言した新しいグループを定義します。

    ```xml
    <Group guid="guidToolbarButtonPackageCmdSet"
           id="SolutionToolbarGroup" priority="0xF000">
            <Parent guid="guidSHLMainMenu" id="IDM_VS_TOOL_PROJWIN"/>
          </Group>
    ```

     親 GUID:ID ペアを`guidSHLMainMenu`設定`IDM_VS_TOOL_PROJWIN`し、このグループを**ソリューション エクスプローラー**のツール バーに配置し、優先度の高い値を設定すると、他のコマンド グループの後に配置されます。

3. `<Buttons>`セクションで、前のステップで定義したグループを`<Button>`反映するように生成されたエントリの親 ID を変更します。 変更された`<Button>`要素は次のようになります。

    ```xml
    <Button guid="guidToolbarButtonPackageCmdSet" id="ToolbarButtonId" priority="0x0100" type="Button">
        <Parent guid="guidToolbarButtonPackageCmdSet" id="SolutionToolbarGroup" />
        <Icon guid="guidImages" id="bmpPicStrikethrough" />
        <Strings>
            <ButtonText>Invoke ToolbarButton</ButtonText>
        </Strings>
    </Button>
    ```

4. プロジェクトをビルドし、デバッグを開始します。 実験用インスタンスが表示されます。

     **ソリューション エクスプローラー**のツール バーには、既存のボタンの右側に新しいコマンド ボタンが表示されます。 ボタンアイコンは取り消し線です。

5. 新しいボタンをクリックします。

     メッセージを持つダイアログ ボックス**ツール バー ボタンパッケージソリューション ツール バー バー バー.ツールバー ボタン.MenuItemCallback() が**表示される必要があります。

## <a name="control-the-visibility-of-a-button"></a>ボタンの表示を制御する
 チュートリアルのこのセクションでは、ツール バー上のボタンの表示を制御する方法を示します。 コンテキストを*SolutionToolbar.vsct*ファイルの`<VisibilityConstraints>`セクション内の 1 つ以上のプロジェクトに設定すると、プロジェクトが開いているときにのみボタンが表示されるように制限できます。

### <a name="to-display-a-button-when-one-or-more-projects-are-open"></a>1 つ以上のプロジェクトが開いているときにボタンを表示するには

1. ツール`<Buttons>`バー*ボタンパッケージ.vsct*のセクションで、 タグと`<Button>``<Icons>`の間の既存の`<Strings>`要素に 2 つのコマンド フラグを追加します。

   ```xml
   <CommandFlag>DefaultInvisible</CommandFlag>
   <CommandFlag>DynamicVisibility</CommandFlag>
   ```

    および フラグは`DefaultInvisible`、 セクションのエントリを有効にするように設定する必要があります。 `DynamicVisibility` `<VisibilityConstraints>`

2. 2`<VisibilityConstraints>`つの`<VisibilityItem>`エントリを含むセクションを作成します。 終了`</Commands>`タグの直後に新しいセクションを配置します。

   ```xml
   <VisibilityConstraints>
       <VisibilityItem guid="guidToolbarButtonPackageCmdSet"
             id="ToolbarButtonId"
             context="UICONTEXT_SolutionHasSingleProject" />
       <VisibilityItem guid="guidToolbarButtonPackageCmdSet"
             id="ToolbarButtonId"
             context="UICONTEXT_SolutionHasMultipleProjects" />
   </VisibilityConstraints>
   ```

    各表示項目は、指定されたボタンが表示される条件を表します。 複数の条件を適用するには、同じボタンに対して複数のエントリを作成する必要があります。

3. プロジェクトをビルドし、デバッグを開始します。 実験用インスタンスが表示されます。

    **ソリューション エクスプローラー**のツール バーには取り消し線ボタンがありません。

4. プロジェクトを含むソリューションを開きます。

    取り消し線ボタンは、既存のボタンの右側のツールバーに表示されます。

5. **[ファイル]** メニューの **[ソリューションを閉じる]** をクリックします。 ボタンがツールバーから消えます。

   ボタンの表示は、VSPackage[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]が読み込まれるまでによって制御されます。 VS パッケージが読み込まれた後、ボタンの表示設定は、VSPackage によって制御されます。  詳細については、「[メニュー コマンドと OleMenu コマンド](/visualstudio/extensibility/menucommands-vs-olemenucommands?view=vs-2015)」を参照してください。

## <a name="see-also"></a>関連項目
- [コマンド、メニュー、およびツールバー](../extensibility/internals/commands-menus-and-toolbars.md)
