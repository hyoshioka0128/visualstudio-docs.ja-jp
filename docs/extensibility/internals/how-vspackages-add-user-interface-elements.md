---
title: VS パッケージがユーザー インターフェイス要素を追加する方法 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- user interfaces, adding elements
- UI element design [Visual Studio SDK], VSPackages
- VSPackages, contributing UI elements
ms.assetid: abc5d9d9-b267-48a1-92ad-75fbf2f4c1b9
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1d9cc3184009dd98e743064db1b8eb2abe6059d1
ms.sourcegitcommit: ade07bd1cf69b8b494d171ae648cfdd54f7800d3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81649596"
---
# <a name="how-vspackages-add-user-interface-elements"></a>VSPackages がユーザー インターフェイス要素を追加する方法
VSPackage は、メニュー、ツール バー、ツール ウィンドウなどのユーザー インターフェイス (UI) 要素を *.vsct*ファイルを使用して Visual Studio に追加できます。

UI 要素のデザイン ガイドラインは[、Visual Studio ユーザー エクスペリエンスのガイドライン](../../extensibility/ux-guidelines/visual-studio-user-experience-guidelines.md)を参照してください。

## <a name="the-visual-studio-command-table-architecture"></a>Visual Studio コマンド テーブルのアーキテクチャ
前述のように、コマンド テーブル アーキテクチャは、前述のアーキテクチャの原則をサポートします。 コマンド テーブル アーキテクチャの抽象化、データ構造、およびツールの背後にある原則は次のとおりです。

- 基本的な項目には、メニュー、コマンド、およびグループの 3 種類があります。 メニューは、メニュー、サブメニュー、ツールバー、またはツール ウィンドウとして UI で公開できます。 コマンドは、ユーザーが IDE で実行できるプロシージャで、メニュー項目、ボタン、リスト ボックス、またはその他のコントロールとして公開できます。 グループは、メニューとコマンドの両方のコンテナです。

- 各項目は、項目、その他の項目に対する優先順位、および動作を変更するフラグを記述する定義によって指定されます。

- 各アイテムには、アイテムの親を記述する配置があります。 アイテムは複数の親を持つことができるので、UI 内の複数の場所に表示できます。

すべてのコマンドは、そのグループ内の唯一の子であっても、その親としてグループを持っている必要があります。 すべての標準メニューには、親グループが必要です。 ツールバーとツール ウィンドウは、独自の親として機能します。 グループは、親として Visual Studio のメイン メニュー バー、または任意のメニュー、ツール バー、またはツール ウィンドウを持つことができます。

### <a name="how-items-are-defined"></a>アイテムの定義方法
*vsct*ファイルは XML 形式でフォーマットされます。 パッケージの UI 要素を定義し、それらの要素が IDE 内のどこに表示されるかを決定します。 パッケージ内のすべてのメニュー、グループ、またはコマンドには、まずセクションの GUID と`Symbols`ID が割り当てられます。 vsct ファイルの *.vsct*残りの部分では、各メニュー、コマンド、およびグループは、GUID と ID の組み合わせによって識別されます。 次の例は、テンプレート`Symbols`で**メニュー コマンド**が選択されたときに Visual Studio パッケージ テンプレートによって生成される一般的なセクションを示しています。

```xml
<Symbols>
  <!-- This is the package guid. -->
  <GuidSymbol name="guidMenuTextPkg" value="{b1253bc6-d266-402b-89e7-5e3d3b22c746}" />

  <!-- This is the guid used to group the menu commands together -->
  <GuidSymbol name="guidMenuTextCmdSet" value="{a633d4e4-6c65-4436-a138-1abeba7c9a69}">
    <IDSymbol name="MyMenuGroup" value="0x1020" />
    <IDSymbol name="cmdidMyCommand" value="0x0100" />
  </GuidSymbol>

  <GuidSymbol name="guidImages" value="{53323d9a-972d-4671-bb5b-9e418480922f}">
    <IDSymbol name="bmpPic1" value="1" />
    <IDSymbol name="bmpPic2" value="2" />
    <IDSymbol name="bmpPicSearch" value="3" />
    <IDSymbol name="bmpPicX" value="4" />
    <IDSymbol name="bmpPicArrows" value="5" />
  </GuidSymbol>
</Symbols>
```

`Symbols`セクションの最上位要素は[GuidSymbol 要素](../../extensibility/guidsymbol-element.md)です。 `GuidSymbol`要素は、パッケージとそのコンポーネントパーツを識別するために IDE で使用される GUID に名前をマップします。

> [!NOTE]
> GUID は、Visual Studio パッケージ テンプレートによって自動的に生成されます。 [**ツール**] メニューの [GUID の作成] をクリックして、一意の**GUID を作成**することもできます。

最初`GuidSymbol`の要素は`guid<PackageName>Pkg`、パッケージ自体の GUID です。 これは、パッケージを読み込むために Visual Studio によって使用される GUID です。 通常、子要素はありません。

慣例により、メニューとコマンドは 2 番目`GuidSymbol`の要素`guid<PackageName>CmdSet`の下にグループ化され、ビットマップ`GuidSymbol`は`guidImages`3 番目の要素の下に表示されます。 この規則に従う必要はありませんが、各メニュー、グループ、コマンド、およびビットマップは`GuidSymbol`要素の子である必要があります。

2 番目`GuidSymbol`の要素では、パッケージ コマンド セットを表`IDSymbol`す要素が複数あります。 各[IDSymbol 要素](../../extensibility/idsymbol-element.md)は、名前を数値にマップし、コマンド セットの一部であるメニュー、グループ、またはコマンドを表します。 3`IDSymbol`番目`GuidSymbol`の要素の要素は、コマンドのアイコンとして使用できるビットマップを表します。 GUID/ID ペアはアプリケーション内で一意である必要があるため、同じ`GuidSymbol`要素の 2 つの子が同じ値を持つ可能性はありません。

### <a name="menus-groups-and-commands"></a>メニュー、グループ、およびコマンド
メニュー、グループ、またはコマンドに GUID と ID がある場合は、IDE に追加できます。 すべての UI 要素には、次のものが必要です。

- UI`guid`要素が定義されている`GuidSymbol`要素の名前と一致する属性。

- 関連`id`付けられた`IDSymbol`要素の名前と一致する属性。

属性と`guid`属性`id`を組み合わせて、UI 要素の*シグネチャ*を構成します。

- 親`priority`メニューまたはグループ内の UI 要素の配置を決定する属性。

- 親メニューまたはグループの`guid`シグネチャ`id`を指定する属性と属性を持つ親[要素](../../extensibility/parent-element.md)。

#### <a name="menus"></a>メニュー
各メニューは、 セクション内の Menu `Menus` [要素](../../extensibility/menu-element.md)として定義されます。 メニューには`guid`、 `id`、および`priority`属性、および`Parent`要素、および次の追加属性と子が必要です。

- メニュー`type`をメニューの一種として表示するか、ツールバーとして IDE に表示するかを指定する属性。

- IDE のメニューのタイトルを指定する[ButtonText 要素](../../extensibility/buttontext-element.md)、およびメニューにアクセスするために**コマンド**ウィンドウで使用される名前を指定する[CommandName 要素](../../extensibility/commandname-element.md)を含む[文字列要素](../../extensibility/strings-element.md)。

- 省略可能なフラグ。 メニュー定義に表示される[CommandFlag 要素](../../extensibility/command-flag-element.md)は、IDE での外観や動作を変更します。

ツールバー`Menu`などのドッキング可能な要素でない限り、すべての要素は親としてグループを持つ必要があります。 ドッキング可能なメニューは、それ自体の親です。 `type`属性のメニューと値の詳細については[、Menu 要素](../../extensibility/menu-element.md)のドキュメントを参照してください。

次の例は、Visual Studio のメニュー バーの **[ツール]** メニューの横に表示されるメニューを示しています。

```xml
<Menu guid="guidTopLevelMenuCmdSet" id="TopLevelMenu" priority="0x700" type="Menu">
  <Parent guid="guidSHLMainMenu" id="IDG_VS_MM_TOOLSADDINS" />
  <Strings>
    <ButtonText>TestMenu</ButtonText>
    <CommandName>TestMenu</CommandName>
  </Strings>
</Menu>
```

#### <a name="groups"></a>グループ
グループは`Groups`*、.vsct*ファイルのセクションで定義されている項目です。 グループは単なるコンテナです。 メニュー上の分割線以外は IDE に表示されません。 したがって[、Group 要素](../../extensibility/group-element.md)は、そのシグネチャ、優先度、および親によってのみ定義されます。

グループには、メニュー、別のグループ、または親としてグループを設定できます。 ただし、親は通常、メニューまたはツールバーです。 上の例のメニューはグループの`IDG_VS_MM_TOOLSADDINS`子で、そのグループは Visual Studio のメニュー バーの子です。 次の例のグループは、前の例のメニューの子です。

```xml
<Group guid="guidTopLevelMenuCmdSet" id="MyMenuGroup" priority="0x0600">
  <Parent guid="guidTopLevelMenuCmdSet" id="TopLevelMenu"/>
</Group>
```

メニューの一部であるため、通常、このグループにはコマンドが含まれます。 ただし、他のメニューも含まれる可能性があります。 次の例に示すように、サブメニューの定義は次のようになります。

```xml
<Menu guid="guidTopLevelMenuCmdSet" id="SubMenu" priority="0x0100" type="Menu">
  <Parent guid="guidTopLevelMenuCmdSet" id="MyMenuGroup"/>
  <Strings>
    <ButtonText>Sub Menu</ButtonText>
    <CommandName>Sub Menu</CommandName>
  </Strings>
</Menu>
```

#### <a name="commands"></a>コマンド
IDE に提供されるコマンドは、 [Button 要素](../../extensibility/button-element.md)または Combo[要素](../../extensibility/combo-element.md)として定義されます。 メニューまたはツールバーに表示するには、コマンドの親としてグループが必要です。

##### <a name="buttons"></a>Buttons (ボタン)
ボタンは`Buttons`セクションで定義されます。 ユーザーが 1 つのコマンドを実行するためにクリックしたメニュー項目、ボタン、またはその他の要素は、ボタンと見なされます。 一部のボタンの種類には、リスト機能を含めることができます。 ボタンには、メニューと同じ必須およびオプションの属性があり、また、IDE のボタンを表すビットマップの GUID と ID を指定する[Icon 要素](../../extensibility/icon-element.md)を持つことができます。 ボタンとその属性の詳細については[、Buttons 要素](../../extensibility/buttons-element.md)のドキュメントを参照してください。

次の例のボタンは、前の例のグループの子であり、そのグループの親メニューのメニュー項目として IDE に表示されます。

```xml
<Button guid="guidTopLevelMenuCmdSet" id="cmdidTestCommand" priority="0x0100" type="Button">
  <Parent guid="guidTopLevelMenuCmdSet" id="MyMenuGroup" />
  <Icon guid="guidImages" id="bmpPic1" />
  <Strings>
    <CommandName>cmdidTestCommand</CommandName>
    <ButtonText>Test Command</ButtonText>
  </Strings>
</Button>
```

##### <a name="combos"></a>コンボ
コンボは`Combos`セクションで定義されます。 各`Combo`要素は、IDE のドロップダウン リスト ボックスを表します。 コンボの`type`属性の値によっては、リスト ボックスがユーザーによって書き込み可能である場合と書き込みできない場合があります。 コンボには、ボタンと同じ要素と動作があり、さらに次の属性を持つことができます。

- ピクセル`defaultWidth`幅を指定する属性。

- リスト`idCommandList`ボックスに表示される項目を含むリストを指定する属性。 コマンド・リストは、コンボを含む`GuidSymbol`同じノードで宣言する必要があります。

次の例では、コンボ要素を定義します。

```xml
<Combos>
  <Combo guid="guidFirstToolWinCmdSet"
         id="cmdidWindowsMediaFilename"
         priority="0x0100" type="DynamicCombo"
         idCommandList="cmdidWindowsMediaFilenameGetList"
         defaultWidth="130">
    <Parent guid="guidFirstToolWinCmdSet"
            id="ToolbarGroupID" />
    <CommandFlag>IconAndText</CommandFlag>
    <CommandFlag>CommandWellOnly</CommandFlag>
    <CommandFlag>StretchHorizontally</CommandFlag>
    <Strings>
      <CommandName>Filename</CommandName>
      <ButtonText>Enter a Filename</ButtonText>
    </Strings>
  </Combo>
</Combos>
```

##### <a name="bitmaps"></a>ビットマップ
アイコンと共に表示されるコマンドには、GUID と`Icon`ID を使用してビットマップを参照する要素を含める必要があります。 各ビットマップは、セクション内で[ビットマップ要素](../../extensibility/bitmap-element.md)として`Bitmaps`定義されます。 定義に`Bitmap`必要な属性は`guid`、 と`href`だけです。 ソース ファイルがリソース ストリップの場合は、利用できるイメージをストリップに一覧表示するために **、usedList**属性も必要です。 詳細については[、Bitmap 要素](../../extensibility/bitmap-element.md)のドキュメントを参照してください。

### <a name="parenting"></a>子育て
次の規則は、アイテムが別のアイテムを親アイテムとして呼び出す方法を制御します。

|要素|コマンド テーブルのこのセクションで定義|含まれている可能性があります (親として、またはセクション内の`CommandPlacements`配置によって、またはその両方)|含まれる可能性 (親と呼ばれます)|
|-------------| - | - | - |
|グループ|[要素](../../extensibility/groups-element.md)、IDE、その他の VS パッケージをグループ化します。|メニュー、グループ、アイテム自体|メニュー、グループ、およびコマンド|
|メニュー|[メニュー要素](../../extensibility/menus-element.md)、IDE、その他の VS パッケージ|1 から*n 個*のグループ|0 から*n 個*のグループ|
|ツール バー|[メニュー要素](../../extensibility/menus-element.md)、IDE、その他の VS パッケージ|アイテム自体|0 から*n 個*のグループ|
|メニュー項目|[ボタン要素](../../extensibility/buttons-element.md)、IDE、その他の VS パッケージ|1 から*n*個のグループ、アイテム自体|-0 から*n 個*のグループ|
|Button|[ボタン要素](../../extensibility/buttons-element.md)、IDE、その他の VS パッケージ|1 から*n*個のグループ、アイテム自体||
|複合|[要素 、IDE、](../../extensibility/combos-element.md)その他の VS パッケージをコンボ|1 から*n*個のグループ、アイテム自体||

### <a name="menu-command-and-group-placement"></a>メニュー、コマンド、およびグループ配置
メニュー、グループ、またはコマンドは、IDE 内の複数の場所に表示できます。 アイテムを複数の場所に表示するには、セクションに[CommandPlacement](../../extensibility/commandplacement-element.md)要素`CommandPlacements`として追加する必要があります。 任意のメニュー、グループ、またはコマンドをコマンド配置として追加できます。 ただし、複数の状況依存の場所に表示できないため、ツール バーをこの方法で配置することはできません。

コマンド配置には、 `guid` `id`、および`priority`属性があります。 GUID と ID は、配置されている項目の GUID と ID と一致する必要があります。 属性`priority`は、他の項目に関するアイテムの配置を制御します。 同じ優先度を持つ複数の項目をマージする場合、パッケージがビルドされるたびにパッケージリソースが同じ順序で読み取られるとは限らないため、それらの配置は未定義になります。

メニューまたはグループが複数の場所に表示される場合、そのメニューまたはグループのすべての子が各インスタンスに表示されます。

## <a name="command-visibility-and-context"></a>コマンドの可視性とコンテキスト
複数の VSPackages がインストールされている場合、メニュー、メニュー項目、およびツールバーが多用されると、IDE が煩雑になることがあります。 この問題を回避するには、可視性制約とコマンド フラグを使用して、個々の UI 要素の*表示を*制御できます。

### <a name="visibility-constraints"></a>可視性制約
可視制約は、セクション内の[VisibilityItem](../../extensibility/visibilityitem-element.md)要素`VisibilityConstraints`として設定されます。 可視性制約は、ターゲット項目が表示される特定の UI コンテキストを定義します。 このセクションに含まれるメニューまたはコマンドは、定義されたコンテキストのいずれかがアクティブな場合にのみ表示されます。 このセクションでメニューまたはコマンドが参照されていない場合、既定では常に表示されます。 このセクションはグループには適用されません。

`VisibilityItem`要素には、ターゲット UI 要素`guid`と`id`の 3 つの属性が必要です`context`。 この`context`属性は、ターゲット項目を表示するタイミングを指定し、有効な UI コンテキストをその値として受け取ります。 Visual Studio の UI コンテキスト定数は、<xref:Microsoft.VisualStudio.VSConstants>クラスのメンバーです。 すべての`VisibilityItem`要素は、1 つのコンテキスト値のみを受け取ることができます。 2 番目のコンテキストを適用するには、`VisibilityItem`次の例に示すように、同じ項目を指す 2 番目の要素を作成します。

```xml
<VisibilityConstraints>
  <VisibilityItem guid="guidSolutionToolbarCmdSet"
        id="cmdidTestCmd"
        context="UICONTEXT_SolutionHasSingleProject" />
  <VisibilityItem guid="guidSolutionToolbarCmdSet"
        id="cmdidTestCmd"
        context="UICONTEXT_SolutionHasMultipleProjects" />
</VisibilityConstraints>
```

### <a name="command-flags"></a>コマンド フラグ
次のコマンド フラグは、適用するメニューとコマンドの表示に影響を与える可能性があります。

`AlwaysCreate`メニューは、グループやボタンがなくても作成されます。

有効な対象:`Menu`

`CommandWellOnly`コマンドが最上位のメニューに表示されず、追加のシェルカスタマイズ (キーへのバインドなど) に使用できるようにする場合は、このフラグを適用します。 VSPackage をインストールした後、ユーザーは **[オプション]** ダイアログ ボックスを開き、[**キーボード環境**]カテゴリの下でコマンドの配置を編集することで、これらのコマンドをカスタマイズできます。 ショートカット メニュー、ツールバー、メニュー コントローラ、サブメニューの配置には影響しません。

有効な場合`Button`:`Combo`

`DefaultDisabled`既定では、コマンドを実装する VSPackage が読み込まれていないか、QueryStatus メソッドが呼び出されていない場合は、コマンドは無効になります。

有効な場合`Button`:`Combo`

`DefaultInvisible`既定では、コマンドを実装する VSPackage が読み込まれていないか、QueryStatus メソッドが呼び出されていない場合、コマンドは表示されません。

`DynamicVisibility`フラグと組み合わせる必要があります。

に有効: `Button` `Combo`,`Menu`

`DynamicVisibility`コマンドの表示設定は、メソッドまたは`QueryStatus``VisibilityConstraints`セクションに含まれているコンテキスト GUID を使用して変更できます。

ツールバーではなく、メニューに表示されるコマンドに適用されます。 `QueryStatus`メソッドから`OLECMDF_INVISIBLE`フラグが返された場合、トップレベルのツール バー項目は無効にできますが、非表示にすることはできません。

メニュー上では、このフラグは、メンバーが非表示のときに自動的に非表示にする必要があることを示します。 トップレベルメニューには既にこの動作が存在するため、通常、このフラグはサブメニューに割り当てられます。

`DefaultInvisible`フラグと組み合わせる必要があります。

に有効: `Button` `Combo`,`Menu`

`NoShowOnMenuController`このフラグを持つコマンドがメニュー コントローラに配置されている場合、そのコマンドはドロップダウン リストに表示されません。

有効な対象:`Button`

コマンド フラグの詳細については[、CommandFlag 要素](../../extensibility/command-flag-element.md)のドキュメントを参照してください。

#### <a name="general-requirements"></a>一般的な要件
コマンドを表示して有効にするには、次の一連のテストに合格する必要があります。

- コマンドは正しく配置されています。

- `DefaultInvisible`フラグが設定されていません。

- 親メニューまたはツールバーが表示されます。

- [VisibilityConstraints 要素](../../extensibility/visibilityconstraints-element.md)セクションのコンテキスト エントリが原因で、コマンドは表示されません。

- インターフェイスを実装する VSPackage<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>コードを表示し、コマンドを有効にします。 インターフェイス コードによってインターセプトされ、そのコードに対して機能する。

- ユーザーがコマンドをクリックすると、「[ルーティング アルゴリズム](../../extensibility/internals/command-routing-algorithm.md)」で概説されている手順が適用されます。

## <a name="call-pre-defined-commands"></a>定義済みコマンドの呼び出し
[この要素](../../extensibility/usedcommands-element.md)を使用すると、VS パッケージは、他の VS パッケージまたは IDE によって提供されるコマンドにアクセスできます。 これを行うには、使用するコマンドの GUID と ID を持つ[UsedCommand 要素](../../extensibility/usedcommand-element.md)を作成します。 これにより、現在の Visual Studio 構成の一部ではない場合でも、コマンドが Visual Studio によって読み込まれるようになります。 詳細については、「 [UsedCommand 要素](../../extensibility/usedcommand-element.md)」を参照してください。

## <a name="interface-element-appearance"></a>インターフェイス要素の外観
コマンド要素の選択および配置に関する考慮事項は、次のとおりです。

- [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]には、配置によって表示される UI 要素が多数用意されています。

- このフラグを`DefaultInvisible`使用して定義された UI 要素は、<xref:EnvDTE.IDTCommandTarget.QueryStatus%2A>メソッドの VSPackage 実装によって表示されるか、`VisibilityConstraints`セクション内の特定の UI コンテキストに関連付けられている場合を除き、IDE に表示されません。

- 正常に配置されたコマンドでも表示されない場合があります。 これは、VSPackage が実装している (または実装されていない) インターフェイスに応じて、IDE が自動的に一部のコマンドを非表示または表示するためです。 たとえば、VSPackage の一部のビルド インターフェイスの実装では、ビルド関連のメニュー項目が自動的に表示されます。

- UI 要素`CommandWellOnly`の定義にフラグを適用すると、カスタマイズによってのみコマンドを追加できます。

- コマンドは、IDE がデザイン ビューのときにダイアログ ボックスが表示される場合など、特定の UI コンテキストでのみ使用できます。

- IDE に表示される特定の UI 要素を作成するには、1 つ以上のインターフェイスを実装するか、コードを記述する必要があります。

## <a name="see-also"></a>関連項目
- [メニューとコマンドの拡張](../../extensibility/extending-menus-and-commands.md)
