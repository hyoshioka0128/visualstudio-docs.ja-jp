---
title: オーサリング。Vsct ファイル |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSCT files, manual authoring
ms.assetid: e9f715dc-12b7-439b-bdf3-f3dc75e62f1c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: dfa276d04e2d312d7ff00b1e9bc0015beb1e254e
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80709995"
---
# <a name="author-vsct-files"></a>作成者 .vsct ファイル
このドキュメントでは、Visual Studio 統合開発環境 (IDE) にメニュー項目、ツール バー、およびその他のユーザー インターフェイス (UI) 要素を追加する *.vsct*ファイルを作成する方法を示します。 Vsct ファイルが存在しない Visual Studio パッケージ (VSPackage) に UI *.vsct*要素を追加する場合は、次の手順を使用します。

 新しいプロジェクトの場合は、Visual Studio パッケージ テンプレートを使用することをお勧めします *.vsct*ファイルを生成する.vsct ファイルは、選択内容に応じて、メニュー コマンド、ツール ウィンドウ、またはカスタム エディターに必要な要素が既に含まれています。 VSPackage の要件を満たすように、この *.vsct*ファイルを変更できます。 *vsct*ファイルを変更する方法の詳細については、「[メニューとコマンドの拡張](../../extensibility/extending-menus-and-commands.md)」の例を参照してください。

## <a name="author-the-file"></a>ファイルの作成
 次のフェーズで *.vsct*ファイルを作成する: ファイルとリソースの構造を作成し、UI 要素を宣言し、UI 要素を IDE に配置し、特殊な動作を追加します。

### <a name="file-structure"></a>ファイル構造
 *vsct*ファイルの基本構造は、コマンド要素と[シンボル](../../extensibility/symbols-element.md)要素を含む[CommandTable](../../extensibility/commands-element.md)ルート要素です。 [CommandTable](../../extensibility/commandtable-element.md)

#### <a name="to-create-the-file-structure"></a>ファイル構造を作成するには

1. 「方法 : *.vsct*ファイルを作成する」の手順に従って、[プロジェクトに .vsct ファイルを](../../extensibility/internals/how-to-create-a-dot-vsct-file.md)追加します。

2. 次の例に示すように、`CommandTable`必要な名前空間を要素に追加します。

    ```xml
    <CommandTable xmlns="http://schemas.microsoft.com/VisualStudio/2005-10-18/CommandTable"
        xmlns:xs="http://www.w3.org/2001/XMLSchema">

    ```

3. `CommandTable`要素で、カスタム メニュー `Commands` 、ツールバー、コマンド グループ、およびコマンドをすべてホストする要素を追加します。 カスタム UI 要素を読み込むことができる`Commands`ように、要素の`Package`属性をパッケージの名前に設定する必要があります。

     要素の`Commands`後に、パッケージ`Symbols`の GUID を定義する要素と、UI 要素の名前とコマンド ID を追加します。

### <a name="include-visual-studio-resources"></a>ビジュアル スタジオ のリソースを含める
 [Extern](../../extensibility/extern-element.md)要素を使用して、Visual Studio のコマンドを定義するファイルと、IDE に UI 要素を配置するために必要なメニューにアクセスします。 パッケージの外部で定義されたコマンドを使用する場合は[、UsedCommands](../../extensibility/usedcommands-element.md)要素を使用して Visual Studio に通知します。

#### <a name="to-include-visual-studio-resources"></a>ビジュアル スタジオ リソースを含めるには

1. 要素の上部で`CommandTable`、参照する外部ファイル`Extern`ごとに 1 つの要素を追加し、`href`その属性をファイルの名前に設定します。 Visual Studio リソースにアクセスするには、次のヘッダー ファイルを参照できます。

   - *Stdidcmd.h*: Visual Studio によって公開されるすべてのコマンドの ID を定義します。

   - *Vsshlids.h*: Visual Studio メニューのコマンド ID が含まれています。

2. Visual Studio またはその他のパッケージによって定義されているコマンドをパッケージが呼び出す`UsedCommands`場合は、`Commands`要素の後に要素を追加します。 パッケージの一部ではない各コマンドを呼び出す場合は、この要素に[UsedCommand](../../extensibility/usedcommand-element.md)要素を設定します。 要素`guid`の属性`id`と属性を`UsedCommand`、呼び出すコマンドの GUID 値と ID 値に設定します。

   Visual Studio コマンドの GUID と ID を検索する方法の詳細については[、「Visual Studio コマンドの GUID と ID](../../extensibility/internals/guids-and-ids-of-visual-studio-commands.md)」を参照してください。 他のパッケージからコマンドを呼び出す場合は、それらのパッケージの *.vsct*ファイルで定義されているコマンドの GUID と ID を使用します。

### <a name="declare-ui-elements"></a>UI 要素の宣言
 `Symbols` *vsct*ファイルのセクションですべての新しい UI 要素を宣言します。

#### <a name="to-declare-ui-elements"></a>UI 要素を宣言するには

1. 要素に`Symbols`、3 つの[GuidSymbol](../../extensibility/guidsymbol-element.md)要素を追加します。 各`GuidSymbol`要素には、`name`属性と属性`value`があります。 要素の`name`目的を反映するように属性を設定します。 属性`value`は GUID を受け取ります。 (GUID を生成するには、[**ツール**] メニューの **[GUID**の作成] をクリックし、[**レジストリ形式**] をクリックします。

     最初`GuidSymbol`の要素はパッケージを表し、通常は子がありません。 2`GuidSymbol`番目の要素はコマンド セットを表し、メニュー、グループ、およびコマンドを定義するすべてのシンボルを含みます。 3`GuidSymbol`番目の要素は、イメージ ストアを表し、コマンドのすべてのアイコンのシンボルを含みます。 アイコンを使用するコマンドがない場合は、3 番目`GuidSymbol`の要素を省略できます。

2. コマンド`GuidSymbol`セットを表す要素に、1 つ以上の[IDSymbol](../../extensibility/idsymbol-element.md)要素を追加します。 これらの各要素は、UI に追加するメニュー、ツールバー、グループ、またはコマンドを表します。

     各`IDSymbol`要素に対して、`name`対応するメニュー、グループ、またはコマンドを参照するために使用する名前に属性を設定し、その`value`要素のコマンド ID を表す 16 進数に設定します。 同じ`IDSymbol`親を持つ 2 つの要素が同じ値を持つ可能性はありません。

3. いずれかの UI 要素にアイコンが必要な場合`IDSymbol`は、イメージ ストアを`GuidSymbol`表す要素に各アイコンの要素を追加します。

### <a name="put-ui-elements-in-the-ide"></a>UI 要素を IDE に配置する
 [メニュー](../../extensibility/menus-element.md)、[グループ](../../extensibility/groups-element.md)、および[ボタン](../../extensibility/buttons-element.md)の各要素には、パッケージで定義されているすべてのメニュー、グループ、およびコマンドの定義が含まれます。 これらのメニュー、グループ、およびコマンドを IDE に配置するには、UI 要素定義の一部である[Parent](../../extensibility/parent-element.md)要素を使用するか、他の場所で定義されている[CommandPlacement](../../extensibility/commandplacement-element.md)要素を使用します。

 各`Menu``Group`要素`Button`、、および`guid`要素には`id`、属性と属性があります。 常に、`guid`コマンド セットを`GuidSymbol`表す要素の名前と一致`id`するように属性を設定し、この属性をセクション内`IDSymbol`のメニュー、グループ、またはコマンドを表す要素の`Symbols`名前に設定します。

#### <a name="to-define-ui-elements"></a>UI 要素を定義するには

1. 新しいメニュー、サブメニュー、ショートカット メニュー、またはツールバーを定義する場合は、要素を`Menus`要素に追加`Commands`します。 次に、作成する各メニューに対して、[Menu](../../extensibility/menu-element.md)要素に Menu`Menus`要素を追加します。

    要素の`guid`属性`id`と属性を`Menu`設定し、属性を`type`必要なメニューの種類に設定します。 親グループ内の`priority`メニューの相対位置を設定するように属性を設定することもできます。

   > [!NOTE]
   > この`priority`属性は、ツールバーおよびコンテキスト メニューには適用されません。

2. Visual Studio IDE のすべてのコマンドは、メニューとツール バーの直接の子であるコマンド グループによってホストされている必要があります。 新しいメニューまたはツールバーを IDE に追加する場合は、これらのメニューまたはツールバーに新しいコマンドグループが含まれている必要があります。 コマンドグループを既存のメニューやツールバーに追加して、コマンドを視覚的にグループ化することもできます。

    新しいコマンド グループを追加する場合は、まず`Groups`要素を作成し、その後、各コマンド グループの[Group](../../extensibility/group-element.md)要素を追加する必要があります。

    各`Group`要素`guid`の`id`属性と 属性を設定し、親`priority`メニューのグループの相対位置を設定する属性を設定します。 詳細については、「[ボタンの再利用可能なグループを作成する](../../extensibility/creating-reusable-groups-of-buttons.md)」を参照してください。

3. IDE に新しいコマンドを追加する場合は、`Buttons`要素を要素`Commands`に追加します。 次に、各コマンドに対して、[要素](../../extensibility/button-element.md)に`Buttons`Button 要素を追加します。

   1. 各`Button`要素`guid`の`id`属性と 属性を設定し、`type`その属性を目的のボタンの種類に設定します。 親グループ内のコマンド`priority`の相対位置を設定する属性を設定することもできます。

       > [!NOTE]
       > ツール`type="button"`バーの標準のメニュー コマンドとボタンに使用します。

   2. 要素に`Button`、[ボタンテキスト](../../extensibility/buttontext-element.md)要素と[コマンド名](../../extensibility/commandname-element.md)要素を含む[文字列](../../extensibility/strings-element.md)要素を追加します。 要素`ButtonText`は、メニュー項目のテキスト ラベル、またはツール バー ボタンのツールヒントを提供します。 この`CommandName`要素は、コマンドウェルで使用するコマンドの名前を提供します。

   3. コマンドにアイコンがある場合は、要素に[Icon](../../extensibility/icon-element.md)要素を`Button`作成し、その`guid`要素と`id`属性をアイコン`Bitmap`の要素に設定します。

       > [!NOTE]
       > ツールバーのボタンにはアイコンが必要です。

   詳細については、「[メニュー コマンドと OleMenu コマンド](/visualstudio/extensibility/menucommands-vs-olemenucommands?view=vs-2015)」を参照してください。

4. コマンドにアイコンが必要な場合は、要素に[Bitmaps](../../extensibility/bitmaps-element.md) `Commands`要素を追加します。 次に、各アイコンに対して、[要素](../../extensibility/bitmap-element.md)に`Bitmaps`Bitmap 要素を追加します。 ここでビットマップ リソースの場所を指定します。 詳細については、「メニュー[コマンドにアイコンを追加する」を](../../extensibility/adding-icons-to-menu-commands.md)参照してください。

   ほとんどのメニュー、グループ、およびコマンドを正しく配置するには、親の構造に依存できます。 非常に大きなコマンド セットの場合、またはメニュー、グループ、またはコマンドが複数の場所に表示される必要がある場合は、コマンドの配置を指定することをお勧めします。

#### <a name="to-rely-on-parenting-to-place-ui-elements-in-the-ide"></a>IDE に UI 要素を配置する親に依存するには

1. 一般的な親を作成するには`Parent`、パッケージで`Menu`定義`Group`されている要素`Command`、、および要素をそれぞれ作成します。

    要素の`Parent`ターゲットは、メニュー、グループ、またはコマンドを含むメニューまたはグループです。

   1. 属性を`guid`、コマンド セットを定義`GuidSymbol`する要素の名前に設定します。 ターゲット要素がパッケージの一部でない場合は、対応する *.vsct*ファイルで定義されているコマンド セットの guid を使用します。

   2. ターゲットメニュー`id`またはグループの属性`id`と一致するように属性を設定します。 Visual Studio によって公開されるメニューとグループの一覧については[、「Visual Studio のメニューの GUID と ID、](../../extensibility/internals/guids-and-ids-of-visual-studio-menus.md)または Visual Studio[ツール バーの GUID と ID](../../extensibility/internals/guids-and-ids-of-visual-studio-toolbars.md)」を参照してください。

   IDE に配置する UI 要素が多数ある場合、または複数の場所に表示する必要がある要素がある場合は、次の手順に示すように[、CommandPlacements](../../extensibility/commandplacements-element.md)要素でその配置を定義します。

#### <a name="to-use-command-placement-to-place-ui-elements-in-the-ide"></a>コマンド配置を使用して IDE に UI 要素を配置するには

1. `Commands` 要素の後に、`CommandPlacements` 要素を追加します。

2. 要素に`CommandPlacements`、配置する`CommandPlacement`メニュー、グループ、またはコマンドごとに要素を追加します。

    各`CommandPlacement`要素または`Parent`要素は、1 つの IDE の場所に 1 つのメニュー、グループ、またはコマンドを配置します。 UI 要素は 1 つの親しか持てありませんが、複数のコマンド配置を持つことができます。 UI 要素を複数の場所に配置するには、各`CommandPlacement`場所に要素を追加します。

3. 要素の`guid`場合`id`と同様に`CommandPlacement`、各要素の属性と属性をホスト メニューまたはグループに`Parent`設定します。 UI 要素の`priority`相対位置を設定する属性を設定することもできます。

   子育てとコマンド配置によって配置を混在させることができます。 ただし、非常に大きなコマンド セットの場合は、コマンド配置のみを使用することをお勧めします。

### <a name="add-specialized-behaviors"></a>特殊な動作を追加する
 [CommandFlag](../../extensibility/command-flag-element.md)要素を使用して、メニューやコマンドの動作を変更して、表示や表示設定を変更できます。 また[、VisibilityConstraints](../../extensibility/visibilityconstraints-element.md)要素を使用してコマンドが表示されるタイミングや[、KeyBindings](../../extensibility/keybindings-element.md)要素を使用してキーボード ショートカットを追加する場合にも影響を与えることができます。 特定の種類のメニューやコマンドには、既に特殊な動作が組み込まれています。

#### <a name="to-add-specialized-behaviors"></a>特殊な動作を追加するには

1. ソリューションが読み込まれる場合など、特定の UI コンテキストでのみ UI 要素を表示するには、可視性制約を使用します。

   1. `Commands` 要素の後に、`VisibilityConstraints` 要素を追加します。

   2. 制約する各 UI 項目に対して[、VisibilityItem](../../extensibility/visibilityitem-element.md)要素を追加します。

   3. 各`VisibilityItem``guid`要素に対して、`id`属性と属性をメニュー、グループ、またはコマンドに設定し、`context`クラスで定義されているとおりに、属性を必要な<xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids80>UI コンテキストに設定します。

2. コード内の UI 項目の可視性または可用性を設定するには、次のコマンド フラグの 1 つ以上を使用します。

   - `DefaultDisabled`

   - `DefaultInvisible`

   - `DynamicItemStart`

   - `DynamicVisibility`

   - `NoShowOnMenuController`

   - `NotInTBList`

   詳細については、[コマンド フラグ](../../extensibility/command-flag-element.md)要素を参照してください。

3. 要素の表示方法を変更したり、要素の外観を動的に変更したりするには、次のコマンド フラグを使用します。

   - `AlwaysCreate`

   - `CommandWellOnly`

   - `DefaultDocked`

   - `DontCache`

   - `DynamicItemStart`

   - `FixMenuController`

   - `IconAndText`

   - `Pict`

   - `StretchHorizontally`

   - `TextMenuUseButton`

   - `TextChanges`

   - `TextOnly`

   詳細については、[コマンド フラグ](../../extensibility/command-flag-element.md)要素を参照してください。

4. 要素がコマンドを受け取ったときに反応する方法を変更するには、次のコマンド フラグの 1 つ以上を使用します。

   - `AllowParams`

   - `CaseSensitive`

   - `CommandWellOnly`

   - `FilterKeys`

   - `NoAutoComplete`

   - `NoButtonCustomize`

   - `NoKeyCustomize`

   - `NoToolbarClose`

   - `PostExec`

   - `RouteToDocs`

   - `TextIsAnchorCommand`

   詳細については、[コマンド フラグ](../../extensibility/command-flag-element.md)要素を参照してください。

5. メニューまたはメニューの項目にメニュー依存のショートカット キーをアタッチするには、メニューまたはメニュー項目の`ButtonText`要素にアンパサンド文字 (&) を追加します。 アンパサンドの後に続く文字は、親メニューが開いているときにアクティブなキーボードショートカットです。

6. メニューに依存しないキーボード ショートカットをコマンドにアタッチするには[、KeyBindings](../../extensibility/keybindings-element.md)要素を使用します。 詳細については[、「KeyBinding](../../extensibility/keybinding-element.md)要素」を参照してください。

7. メニュー テキストをローカライズするには、要素`LocCanonicalName`を使用します。 詳細については[、Strings](../../extensibility/strings-element.md)要素を参照してください。

   メニューやボタンの種類には、特殊な動作が含まれるものがあります。 次の一覧では、いくつかの特殊なメニューとボタンの種類について説明します。 `types`その他の型については、[メニュー](../../extensibility/menu-element.md)、[ボタン](../../extensibility/button-element.md)、[およびコンボ](../../extensibility/combo-element.md)の各要素の属性の説明を参照してください。

   - コンボ ボックス: コンボ ボックスは、ツールバーで使用できるドロップダウン リストです。 UI にコンボ ボックスを追加するには、要素に[コンボ](../../extensibility/combos-element.md)要素を`Commands`作成します。 次に、追加`Combos`する各`Combo`コンボ ボックスの要素を要素に追加します。 `Combo`要素は、`Button`要素と同じ属性と子を持`DefaultWidth`ち`idCommandList`、属性と属性も持ちます。 属性`DefaultWidth`は幅をピクセル単位で設定し、`idCommandList`属性はコンボ ボックスの設定に使用されるコマンド ID を指します。

   - メニュー コントローラ: メニュー コントローラは、横に矢印が付いたボタンです。 矢印をクリックするとリストが開きます。 メニュー コントローラーを UI に追加するには、`Menu`要素を作成し`type`、その`MenuController`属性`MenuControllerLatched`を、必要な動作に応じて or に設定します。 メニュー コントローラーを設定するには、要素の親として設定します`Group`。 メニュー コントローラは、そのグループのすべての子をドロップダウン リストに表示します。

## <a name="see-also"></a>関連項目
- [メニューとコマンドの拡張](../../extensibility/extending-menus-and-commands.md)
- [Visual Studio コマンド テーブル (.vsct) ファイル](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
- [VSCT XML スキーマ リファレンス](../../extensibility/vsct-xml-schema-reference.md)
