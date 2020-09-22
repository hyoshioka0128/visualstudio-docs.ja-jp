---
title: 文書.Vsct ファイル |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- VSCT files, manual authoring
ms.assetid: e9f715dc-12b7-439b-bdf3-f3dc75e62f1c
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 85e466e7ebb6294a77e89040260c16fe0043e372
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841837"
---
# <a name="authoring-vsct-files"></a>.Vsct ファイルの編集
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

このドキュメントでは、メニュー項目、ツールバー、およびその他のユーザーインターフェイス (UI) 要素を Visual Studio 統合開発環境 (IDE) に追加するために、vsct ファイルを作成する方法について説明します。 この手順は、まだ vsct ファイルがない Visual Studio パッケージ (VSPackage) に UI 要素を追加する場合に使用します。  
  
 新しいプロジェクトでは、Visual Studio パッケージテンプレートを使用することをお勧めします。これは、選択内容によっては、メニューコマンド、ツールウィンドウ、またはカスタムエディターに必要な要素が既に存在するためです。 この vsct ファイルを変更して、VSPackage の要件を満たすことができます。 Vsct ファイルを変更する方法の詳細については、「 [メニューとコマンドの拡張](../../extensibility/extending-menus-and-commands.md)」の例を参照してください。  
  
## <a name="authoring-the-file"></a>ファイルの作成  
 これらのフェーズで vsct ファイルを作成します。ファイルとリソースの構造を作成し、UI 要素を宣言し、UI 要素を IDE に配置し、特殊な動作を追加します。  
  
### <a name="file-structure"></a>ファイル構造  
 Vsct ファイルの基本構造は [Commandtable](../../extensibility/commandtable-element.md) ルート要素であり、 [Commands](../../extensibility/commands-element.md) 要素と [Symbols](../../extensibility/symbols-element.md) 要素が含まれています。  
  
##### <a name="to-create-the-file-structure"></a>ファイル構造を作成するには  
  
1. 「方法: を作成する」の手順に従って、vsct ファイルをプロジェクトに追加します。 [Vsct ファイル](../../extensibility/internals/how-to-create-a-dot-vsct-file.md)。  
  
2. 次の例に示すように、要素に必要な名前空間を追加し `CommandTable` ます。  
  
    ```xml  
    <CommandTable xmlns="http://schemas.microsoft.com/VisualStudio/2005-10-18/CommandTable"   
        xmlns:xs="http://www.w3.org/2001/XMLSchema">  
  
    ```  
  
3. 要素に、 `CommandTable` `Commands` すべてのカスタムメニュー、ツールバー、コマンドグループ、およびコマンドをホストする要素を追加します。 カスタム UI 要素が読み込まれるようにするには、 `Commands` 要素の `Package` 属性がパッケージの名前に設定されている必要があります。  
  
     要素の後に、 `Commands` 要素を追加して、 `Symbols` パッケージの guid、および UI 要素の名前とコマンド id を定義します。  
  
### <a name="including-visual-studio-resources"></a>Visual Studio リソースを含む  
 [Extern](../../extensibility/extern-element.md)要素を使用して、Visual Studio のコマンドを定義するファイルと、IDE に UI 要素を配置するために必要なメニューをアクセスします。 パッケージの外部で定義されているコマンドを使用する場合は、使用する [コマンド](../../extensibility/usedcommands-element.md) 要素を使用して Visual Studio に通知します。  
  
##### <a name="to-include-visual-studio-resources"></a>Visual Studio リソースを含めるには  
  
1. 要素の先頭に、 `CommandTable` `Extern` 参照する外部ファイルごとに1つの要素を追加し、属性を `href` ファイルの名前に設定します。 次のヘッダーファイルを参照して、Visual Studio リソースにアクセスできます。  
  
    - Stdidcmd は、Visual Studio によって公開されるすべてのコマンドの Id を定義します。  
  
    - Vsshlids. h には、Visual Studio メニューのコマンド Id が含まれています。  
  
2. パッケージが Visual Studio または他のパッケージで定義されているコマンドを呼び出す場合は、要素の後に要素を追加し `UsedCommands` `Commands` ます。 この要素には、パッケージの一部ではない、呼び出すコマンドごとに使用される [command](../../extensibility/usedcommand-element.md) 要素を設定します。 `guid` `id` 要素の属性と属性を、 `UsedCommand` 呼び出すコマンドの GUID と ID の値に設定します。 Visual Studio コマンドの Guid と Id を検索する方法の詳細については、「 [Visual Studio コマンドの guid と id](../../extensibility/internals/guids-and-ids-of-visual-studio-commands.md)」を参照してください。 他のパッケージからコマンドを呼び出すには、そのパッケージの vsct ファイルで定義されているように、GUID とコマンドの ID を使用します。  
  
### <a name="declaring-ui-elements"></a>UI 要素の宣言  
 すべての新しい UI 要素を、 `Symbols` . vsct ファイルのセクションで宣言します。  
  
##### <a name="to-declare-ui-elements"></a>UI 要素を宣言するには  
  
1. 要素に `Symbols` 、3つの [guidsymbol](../../extensibility/guidsymbol-element.md) 要素を追加します。 各 `GuidSymbol` 要素には、 `name` 属性と `value` 属性があります。 `name`要素の目的を反映するように属性を設定します。 `value`属性は GUID を受け取ります。 (GUID を生成するには、[ **ツール** ] メニューの [ **guid の作成**] をクリックし、[ **レジストリ形式**] を選択します)。  
  
     最初の `GuidSymbol` 要素はパッケージを表し、通常は子を持ちません。 2番目の `GuidSymbol` 要素はコマンドセットを表し、メニュー、グループ、およびコマンドを定義するすべての記号が含まれます。 3番目の `GuidSymbol` 要素はイメージストアを表し、コマンドのすべてのアイコンのシンボルが含まれています。 アイコンを使用するコマンドがない場合は、3番目の要素を省略でき `GuidSymbol` ます。  
  
2. `GuidSymbol`コマンドセットを表す要素で、1つまたは複数の[idsymbol](../../extensibility/idsymbol-element.md)要素を追加します。 これらはそれぞれ、UI に追加するメニュー、ツールバー、グループ、またはコマンドを表します。  
  
     要素ごとに `IDSymbol` 、属性を、対応する `name` メニュー、グループ、またはコマンドを参照するために使用する名前に設定し、要素をその `value` コマンド id を表す16進数に設定します。同じ親を持つ2つの `IDSymbol` 要素が同じ値を持つことはできません。  
  
3. UI 要素のいずれかにアイコンが必要な場合は、 `IDSymbol` イメージストアを表す要素に各アイコンの要素を追加 `GuidSymbol` します。  
  
### <a name="putting-ui-elements-in-the-ide"></a>IDE に UI 要素を配置する  
 [Menus](../../extensibility/menus-element.md)要素、 [groups](../../extensibility/groups-element.md)要素、および[Buttons](../../extensibility/buttons-element.md)要素には、パッケージで定義されているすべてのメニュー、グループ、およびコマンドの定義が含まれています。 これらのメニュー、グループ、およびコマンドは、UI 要素定義の一部である [親](../../extensibility/parent-element.md) 要素を使用するか、別の場所で定義された [commandplacement](../../extensibility/commandplacement-element.md) 要素を使用して、IDE に配置します。  
  
 `Menu`、 `Group` 、およびの各 `Button` 要素には、 `guid` 属性と属性があり `id` ます。 常に、 `guid` コマンドセットを表す要素の名前と一致するように属性を設定し、属性を、 `GuidSymbol` `id` `IDSymbol` セクション内のメニュー、グループ、またはコマンドを表す要素の名前に設定し `Symbols` ます。  
  
##### <a name="to-define-ui-elements"></a>UI 要素を定義するには  
  
1. 新しいメニュー、サブメニュー、ショートカットメニュー、またはツールバーを定義する場合は、要素 `Menus` に要素を追加し `Commands` ます。 次に、作成するメニューごとに、 [メニュー](../../extensibility/menu-element.md) 要素を要素に追加し `Menus` ます。  
  
    `guid` `id` 要素の属性と属性を設定 `Menu` し、属性を `type` 目的のメニューの種類に設定します。 また、属性を設定して、 `priority` 親グループ内のメニューの相対位置を設定することもできます。  
  
   > [!NOTE]
   > 属性は、 `priority` ツールバーやコンテキストメニューには適用されません。  
  
2. Visual Studio IDE のすべてのコマンドは、メニューとツールバーの直接の子であるコマンドグループでホストされている必要があります。 新しいメニューやツールバーを IDE に追加する場合は、新しいコマンドグループが含まれている必要があります。 コマンドを視覚的にグループ化できるように、既存のメニューやツールバーにコマンドグループを追加することもできます。  
  
    新しいコマンドグループを追加する場合は、最初に要素を作成 `Groups` してから、各コマンドグループの [group](../../extensibility/group-element.md) 要素を追加する必要があります。  
  
    `guid` `id` 各要素の属性と属性を設定 `Group` してから、属性を設定して、 `priority` 親メニューのグループの相対位置を設定します。 詳細については、「 [再利用可能なボタンのグループの作成](../../extensibility/creating-reusable-groups-of-buttons.md)」を参照してください。  
  
3. IDE に新しいコマンドを追加する場合は、要素に要素を追加し `Buttons` `Commands` ます。 次に、各コマンドに対して、要素に [Button](../../extensibility/button-element.md) 要素を追加し `Buttons` ます。  
  
   1. `guid` `id` 各要素の属性と属性を設定し、 `Button` 属性を `type` 目的のボタンの種類に設定します。 また、属性を設定して、 `priority` 親グループ内のコマンドの相対位置を設定することもできます。  
  
      > [!NOTE]
      > `type="button"`ツールバーの標準のメニューコマンドとボタンに使用します。  
  
   2. 要素に `Button` 、 [buttontext](../../extensibility/buttontext-element.md)要素と[CommandName](../../extensibility/commandname-element.md)要素を含む[Strings](../../extensibility/strings-element.md)要素を追加します。 要素は、 `ButtonText` メニュー項目のテキストラベル、またはツールバーボタンのツールヒントを提供します。 要素には、 `CommandName` コマンドウェルで使用するコマンドの名前を指定します。  
  
   3. コマンドにアイコンがある場合は、要素に [icon](../../extensibility/icon-element.md) 要素を作成 `Button` し、その `guid` `id` 属性と属性を `Bitmap` アイコンの要素に設定します。  
  
      > [!NOTE]
      > ツールバーのボタンにはアイコンが必要です。  
  
      詳細については、「 [Menucommands と OleMenuCommands](../../misc/menucommands-vs-olemenucommands.md)」を参照してください。  
  
4. いずれかのコマンドでアイコンが必要な場合は、要素に [ビットマップ](../../extensibility/bitmaps-element.md) 要素を追加し `Commands` ます。 次に、各アイコンに対して、要素に [Bitmap](../../extensibility/bitmap-element.md) 要素を追加し `Bitmaps` ます。 ここで、ビットマップリソースの場所を指定します。 詳細については、「 [メニューコマンドへのアイコンの追加](../../extensibility/adding-icons-to-menu-commands.md)」を参照してください。  
  
   ほとんどのメニュー、グループ、およびコマンドを正しく配置するには、親構造に依存することができます。 非常に大きなコマンドセットの場合、またはメニュー、グループ、またはコマンドを複数の場所に表示する必要がある場合は、コマンドの配置を指定することをお勧めします。  
  
##### <a name="to-rely-on-parenting-to-place-ui-elements-in-the-ide"></a>親を使用して IDE に UI 要素を配置するには  
  
1. 一般的な親の場合は、パッケージで定義されている `Parent` 、、およびの各要素に要素を作成し `Menu` `Group` `Command` ます。  
  
    要素のターゲットは、 `Parent` メニュー、グループ、またはコマンドを格納するグループです。  
  
   1. 属性を、 `guid` `GuidSymbol` コマンドセットを定義する要素の名前に設定します。 ターゲット要素がパッケージに含まれていない場合は、対応する vsct ファイルで定義されているように、そのコマンドセットの guid を使用します。  
  
   2. `id` `id` ターゲットメニューまたはグループの属性と一致するように属性を設定します。 Visual Studio によって公開されているメニューとグループの一覧については、「visual [Studio メニューの guid と id](../../extensibility/internals/guids-and-ids-of-visual-studio-menus.md) 」、または「 [Visual Studio のツールバーの guid と id](../../extensibility/internals/guids-and-ids-of-visual-studio-toolbars.md)」を参照してください。  
  
   IDE に配置する UI 要素が多数ある場合、または複数の場所に出現する要素がある場合は、次の手順に示すように、それらの配置を [commandplacements](../../extensibility/commandplacements-element.md) 要素に定義します。  
  
##### <a name="to-use-command-placement-to-place-ui-elements-in-the-ide"></a>コマンドの配置を使用して UI 要素を IDE に配置するには  
  
1. `Commands` 要素の後に、`CommandPlacements` 要素を追加します。  
  
2. 要素で `CommandPlacements` 、 `CommandPlacement` 配置するメニュー、グループ、またはコマンドごとに要素を追加します。  
  
    各 `CommandPlacement` 要素または要素は、1つ `Parent` の IDE の場所に1つのメニュー、グループ、またはコマンドを配置します。 UI 要素は親を1つだけ持つことができますが、複数のコマンドを配置することができます。 UI 要素を複数の場所に配置するには、 `CommandPlacement` 場所ごとに要素を追加します。  
  
3. 要素の `guid` 場合 `id` と同様に、各要素の属性と属性を、 `CommandPlacement` ホストするメニューまたはグループに設定し `Parent` ます。 また、属性を設定して、 `priority` UI 要素の相対位置を設定することもできます。  
  
   配置とコマンドの配置を組み合わせることができます。 ただし、非常に大きなコマンドセットの場合は、コマンドの配置のみを使用することをお勧めします。  
  
### <a name="adding-specialized-behaviors"></a>特殊な動作の追加  
 [Commandflag](../../extensibility/command-flag-element.md)要素を使用して、メニューやコマンドの外観や表示を変更するなどの動作を変更できます。 [VisibilityConstraints](../../extensibility/visibilityconstraints-element.md)を使用してコマンドを表示するタイミングに影響を与えたり、キー[バインド](../../extensibility/keybindings-element.md)を使用してキーボードショートカットを追加したりすることもできます。 特定の種類のメニューとコマンドには、既に特殊な動作が組み込まれています。  
  
##### <a name="to-add-specialized-behaviors"></a>特殊な動作を追加するには  
  
1. 特定の UI コンテキストでのみ UI 要素を表示するようにするには (たとえば、ソリューションが読み込まれるとき)、可視性の制約を使用します。  
  
   1. `Commands` 要素の後に、`VisibilityConstraints` 要素を追加します。  
  
   2. 制約する各 UI 項目に対して、 [VisibilityItem](../../extensibility/visibilityitem-element.md) 要素を追加します。  
  
   3. 要素ごとに、 `VisibilityItem` `guid` `id` 属性と属性をメニュー、グループ、またはコマンドに設定し、 `context` クラスで定義されているように、属性を目的の UI コンテキストに設定し <xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids80> ます。 詳細については、「 [VisibilityItem 要素](../../extensibility/visibilityitem-element.md)」を参照してください。  
  
2. コード内の UI 項目の可視性または可用性を設定するには、次のコマンドフラグの1つまたは複数を使用します。  
  
   - DefaultDisabled  
  
   - Defaul/Visible  
  
   - DynamicItemStart  
  
   - DynamicVisibility  
  
   - NoShowOnMenuController  
  
   - NotInTBList  
  
     詳細については、「 [Command Flag 要素](../../extensibility/command-flag-element.md)」を参照してください。  
  
3. 要素の表示方法を変更したり、要素の外観を動的に変更したりするには、次のコマンドフラグの1つまたは複数を使用します。  
  
   - 常に作成  
  
   - CommandWellOnly  
  
   - DefaultDocked  
  
   - DontCache  
  
   - DynamicItemStart  
  
   - FixMenuController  
  
   - IconAndText  
  
   - Pict  
  
   - StretchHorizontally  
  
   - TextMenuUseButton  
  
   - TextChanges  
  
   - TextOnly  
  
     詳細については、「 [Command Flag 要素](../../extensibility/command-flag-element.md)」を参照してください。  
  
4. コマンドを受信したときの要素の反応を変更するには、次のコマンドフラグの1つまたは複数を使用します。  
  
   - AllowParams  
  
   - [CaseSensitive]  
  
   - CommandWellOnly  
  
   - フィルタ  
  
   - NoAutoComplete  
  
   - NoButtonCustomize  
  
   - NoKeyCustomize  
  
   - NoToolbarClose  
  
   - PostExec  
  
   - RouteToDocs  
  
   - TextIsAnchorCommand  
  
     詳細については、「 [Command Flag 要素](../../extensibility/command-flag-element.md)」を参照してください。  
  
5. メニューまたはメニュー項目にメニュー依存のキーボードショートカットをアタッチするには、 `ButtonText` メニューまたはメニュー項目の要素にアンパサンド文字 (' & ') を追加します。 アンパサンドの後に続く文字は、親メニューが開いているときのアクティブなキーボードショートカットです。  
  
6. メニューに依存しないショートカットキーをコマンドにアタッチするには、キー [バインド](../../extensibility/keybindings-element.md)を使用します。 詳細については、「 [キーバインド要素](../../extensibility/keybinding-element.md)」を参照してください。  
  
7. メニューテキストをローカライズするには、要素を使用し `LocCanonicalName` ます。 詳細については、「 [Strings 要素](../../extensibility/strings-element.md)」を参照してください。  
  
   メニューとボタンの種類には、特殊な動作があります。 次の表では、いくつかの特殊なメニューとボタンの種類について説明します。 その他の型については、「 `types` [メニュー要素](../../extensibility/menu-element.md)、 [ボタン要素](../../extensibility/button-element.md)、および [コンボ要素](../../extensibility/combo-element.md)」の属性の説明を参照してください。  
  
   コンボ ボックス  
   コンボボックスは、ツールバーで使用できるドロップダウンリストです。 UI にコンボボックスを追加するには、要素に [Combos](../../extensibility/combos-element.md) 要素を作成し `Commands` ます。 次に、 `Combos` `Combo` 追加する各コンボボックスの要素を要素に追加します。 `Combo` 要素には、要素と同じ属性と子があり、 `Button` 属性と属性もあり `DefaultWidth` `idCommandList` ます。 `DefaultWidth`属性はピクセル単位の幅を設定し、 `idCommandList` 属性はコンボボックスの設定に使用されるコマンド ID をポイントします。 詳細については、要素のドキュメントを参照してください `Combo` 。  
  
   MenuController  
   メニューコントローラーは、その横に矢印が付いたボタンです。 矢印をクリックすると、一覧が表示されます。 メニューコントローラーを UI に追加するには、 `Menu` 必要な動作に応じて、要素を作成し、その `type` 属性を**menucontroller または menucontroller**に設定します。 **MenuControllerLatched** メニューコントローラーを設定するには、要素の親として設定し `Group` ます。 メニューコントローラーには、そのグループのすべての子がドロップダウンリストに表示されます。  
  
## <a name="see-also"></a>参照  
 [メニューとコマンドの拡張](../../extensibility/extending-menus-and-commands.md)   
 [Visual Studio コマンドテーブル (.Vsct) ファイル](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)   
 [VSCT XML スキーマ リファレンス](../../extensibility/vsct-xml-schema-reference.md)
