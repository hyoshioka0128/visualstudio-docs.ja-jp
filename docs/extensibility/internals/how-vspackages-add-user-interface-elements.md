---
title: Vspackage Add User Interface Elements |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "81649596"
---
# <a name="how-vspackages-add-user-interface-elements"></a>Vspackage のユーザーインターフェイス要素の追加方法
VSPackage を使用すると、ユーザーインターフェイス (UI) 要素 (メニュー、ツールバー、ツールウィンドウなど) を、 *vsct* ファイルを使用して Visual Studio に追加できます。

UI 要素のデザインガイドラインについては、「 [Visual Studio ユーザーエクスペリエンスガイドライン](../../extensibility/ux-guidelines/visual-studio-user-experience-guidelines.md)」を参照してください。

## <a name="the-visual-studio-command-table-architecture"></a>Visual Studio コマンドテーブルのアーキテクチャ
前述のように、コマンドテーブルのアーキテクチャでは、上記のアーキテクチャの原則がサポートされています。 コマンドテーブルアーキテクチャの抽象化、データ構造、ツールの背後にある理念は次のとおりです。

- 項目には、メニュー、コマンド、およびグループの3つの基本的な種類があります。 メニューは、メニュー、サブメニュー、ツールバー、またはツールウィンドウとして UI に表示できます。 コマンドは、ユーザーが IDE で実行できる手順で、メニュー項目、ボタン、リストボックス、またはその他のコントロールとして公開できます。 グループは、メニューとコマンドの両方のコンテナーです。

- 各項目は、項目、他の項目に対する相対的な優先順位、およびその動作を変更するフラグを記述する定義によって指定されます。

- 各項目には、項目の親を説明する配置があります。 項目は複数の親を持つことができるため、UI 内の複数の場所に表示できます。

すべてのコマンドは、そのグループ内の唯一の子であっても、親としてグループを持つ必要があります。 すべての標準メニューにも親グループが必要です。 ツールバーとツールウィンドウは、独自の親として機能します。 グループは、メインの Visual Studio のメニューバー、または任意のメニュー、ツールバー、またはツールウィンドウの親としてを持つことができます。

### <a name="how-items-are-defined"></a>項目の定義方法
*Vsct*ファイルは XML 形式で書式設定されます。 パッケージの UI 要素を定義し、それらの要素が IDE に表示される場所を決定します。 パッケージ内のすべてのメニュー、グループ、またはコマンドには、最初にセクションの GUID と ID が割り当てられ `Symbols` ます。 他のすべての *vsct* ファイルでは、各メニュー、コマンド、およびグループが GUID と ID の組み合わせによって識別されます。 次の例は、 `Symbols` テンプレートで **メニューコマンド** が選択されたときに Visual Studio パッケージテンプレートによって生成される一般的なセクションを示しています。

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

セクションの最上位レベルの要素 `Symbols` は、 [guidsymbol 要素](../../extensibility/guidsymbol-element.md)です。 `GuidSymbol` 要素は、パッケージとそのコンポーネント部分を識別するために IDE によって使用される Guid に名前を割り当てます。

> [!NOTE]
> Guid は、Visual Studio パッケージテンプレートによって自動的に生成されます。 [**ツール**] メニューの [ **guid の作成**] をクリックして、一意の guid を作成することもできます。

最初の `GuidSymbol` 要素は、 `guid<PackageName>Pkg` パッケージ自体の GUID です。 これは、Visual Studio でパッケージを読み込むために使用される GUID です。 通常、子要素はありません。

慣例により、メニューとコマンドは2番目の要素の下にグループ化され、 `GuidSymbol` `guid<PackageName>CmdSet` ビットマップは3番目の要素の下に `GuidSymbol` `guidImages` あります。 この規則に従う必要はありませんが、各メニュー、グループ、コマンド、およびビットマップは、要素の子である必要があり `GuidSymbol` ます。

パッケージコマンドセットを表す2番目の `GuidSymbol` 要素には、複数の `IDSymbol` 要素があります。 各 [Idsymbol 要素](../../extensibility/idsymbol-element.md) は、名前を数値にマップします。また、コマンドセットの一部であるメニュー、グループ、またはコマンドを表すことができます。 `IDSymbol`3 番目の要素の要素は、 `GuidSymbol` コマンドのアイコンとして使用できるビットマップを表します。 GUID と ID のペアはアプリケーション内で一意である必要があるため、同じ要素の2つの子が `GuidSymbol` 同じ値を持つことはできません。

### <a name="menus-groups-and-commands"></a>メニュー、グループ、およびコマンド
メニュー、グループ、またはコマンドに GUID と ID がある場合は、IDE に追加できます。 すべての UI 要素には、次のものが必要です。

- `guid`UI 要素が定義されている要素の名前と一致する属性 `GuidSymbol` 。

- `id`関連付けられている要素の名前と一致する属性 `IDSymbol` 。

属性と属性を一緒に使う `guid` と、 `id` UI 要素の *署名* が構成されます。

- `priority`親メニューまたはグループ内の UI 要素の配置を決定する属性。

- [Parent element](../../extensibility/parent-element.md) `guid` `id` 親のメニューまたはグループのシグネチャを指定する属性と属性を持つ親要素。

#### <a name="menus"></a>メニュー
各メニューは、セクションの [menu 要素](../../extensibility/menu-element.md) として定義され `Menus` ます。 メニューには `guid` 、、、の各 `id` `priority` 属性、および要素と、 `Parent` 次の追加の属性と子が必要です。

- `type`メニューをメニューの一種として、またはツールバーとして IDE に表示するかどうかを指定する属性です。

- **コマンド**ウィンドウでメニューにアクセスするために使用される名前を指定する、 [buttontext 要素](../../extensibility/buttontext-element.md)を含む[Strings 要素](../../extensibility/strings-element.md)。この[要素は、](../../extensibility/commandname-element.md)IDE のメニューのタイトルを指定します。

- 省略可能なフラグ。 [Commandflag 要素](../../extensibility/command-flag-element.md)は、IDE での外観や動作を変更するためにメニュー定義に表示されることがあります。

すべての `Menu` 要素は、ツールバーなどのドッキング可能な要素でない限り、親としてグループを持つ必要があります。 ドッキング可能なメニューは、独自の親です。 属性のメニューと値の詳細については `type` 、 [メニュー要素](../../extensibility/menu-element.md) のドキュメントを参照してください。

次の例は、Visual Studio のメニューバーの [ **ツール** ] メニューの横に表示されるメニューを示しています。

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
グループは、 `Groups` *vsct* ファイルのセクションで定義されている項目です。 グループはコンテナーにすぎません。 これらは、メニュー上の分割線としてではなく、IDE には表示されません。 したがって、 [Group 要素](../../extensibility/group-element.md) は、そのシグネチャ、優先度、および親によってのみ定義されます。

グループには、メニュー、別のグループ、またはそれ自体を親として設定できます。 ただし、親は通常、メニューまたはツールバーです。 前の例のメニューはグループの子であり、 `IDG_VS_MM_TOOLSADDINS` そのグループは Visual Studio のメニューバーの子です。 次の例のグループは、前の例のメニューの子です。

```xml
<Group guid="guidTopLevelMenuCmdSet" id="MyMenuGroup" priority="0x0600">
  <Parent guid="guidTopLevelMenuCmdSet" id="TopLevelMenu"/>
</Group>
```

このグループはメニューの一部であるため、通常はコマンドを含んでいます。 ただし、他のメニューを含めることもできます。 次の例に示すように、サブメニューが定義されています。

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
IDE に提供されるコマンドは、 [ボタン要素](../../extensibility/button-element.md) または [コンボ要素](../../extensibility/combo-element.md)のいずれかとして定義されます。 メニューまたはツールバーに表示するには、コマンドに親としてのグループが必要です。

##### <a name="buttons"></a>ボタン
ボタンは、セクションで定義されてい `Buttons` ます。 ユーザーが1つのコマンドを実行するためにクリックしたメニュー項目、ボタン、またはその他の要素は、ボタンと見なされます。 一部のボタンの種類には、リスト機能を含めることもできます。 ボタンには、メニューの必須属性とオプション属性があります。また、IDE 内のボタンを表すビットマップの GUID と ID を指定する [Icon 要素](../../extensibility/icon-element.md) を使用することもできます。 ボタンとその属性の詳細については、「 [ボタン要素](../../extensibility/buttons-element.md) のドキュメント」を参照してください。

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

##### <a name="combos"></a>Combos
Combos は、セクションで定義されてい `Combos` ます。 各 `Combo` 要素は、IDE のドロップダウンリストボックスを表します。 リストボックスは、コンボボックスの属性の値に応じて、ユーザーが書き込み可能にすることも、無効にすることもでき `type` ます。 Combos には、ボタンと同じ要素と動作があります。また、次の属性を追加することもできます。

- `defaultWidth`ピクセル幅を指定する属性。

- `idCommandList`リストボックスに表示される項目を含むリストを指定する属性。 コマンド一覧は、コンボボックスと同じノードで宣言されている必要があり `GuidSymbol` ます。

次の例では、複合要素を定義します。

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
アイコンと共に表示されるコマンドには、 `Icon` その GUID と ID を使用してビットマップを参照する要素が含まれている必要があります。 各ビットマップは、セクションの [bitmap 要素](../../extensibility/bitmap-element.md) として定義され `Bitmaps` ます。 定義に必要な属性は、 `Bitmap` `guid` `href` ソースファイルを指すおよびだけです。 ソースファイルがリソースストリップの場合は、使用可能なイメージを一覧表示するために使用される **リスト** 属性も必要です。 詳細については、 [Bitmap 要素](../../extensibility/bitmap-element.md) のドキュメントを参照してください。

### <a name="parenting"></a>親子
次の規則は、項目が親として別の項目を呼び出す方法を制御します。

|要素|コマンドテーブルのこのセクションで定義されています。|(親またはセクション内の配置によって、 `CommandPlacements` またはその両方) が含まれている可能性があります。|含めることができます (親と呼ばれます)|
|-------------| - | - | - |
|グループ|[Groups 要素](../../extensibility/groups-element.md)、IDE、other vspackage|メニュー、グループ、項目自体|メニュー、グループ、およびコマンド|
|メニュー|[Menus 要素](../../extensibility/menus-element.md)、IDE、other vspackage|1 ~ *n 個* のグループ|0 ~ *n 個* のグループ|
|ツール バー|[Menus 要素](../../extensibility/menus-element.md)、IDE、other vspackage|項目自体|0 ~ *n 個* のグループ|
|メニュー項目|[Buttons 要素](../../extensibility/buttons-element.md)、IDE、other vspackage|1 ~ *n* 個のグループ、項目自体|-0 ~ *n 個* のグループ|
|Button|[Buttons 要素](../../extensibility/buttons-element.md)、IDE、other vspackage|1 ~ *n* 個のグループ、項目自体||
|複合|[Combos 要素](../../extensibility/combos-element.md)、IDE、other vspackage|1 ~ *n* 個のグループ、項目自体||

### <a name="menu-command-and-group-placement"></a>メニュー、コマンド、およびグループの配置
メニュー、グループ、またはコマンドは、IDE 内の複数の場所に表示できます。 複数の場所に項目を表示するには、その項目を `CommandPlacements` [commandplacement 要素](../../extensibility/commandplacement-element.md)としてセクションに追加する必要があります。 任意のメニュー、グループ、またはコマンドをコマンドの配置として追加できます。 ただし、複数の状況に依存した場所には表示されないため、この方法でツールバーを配置することはできません。

コマンドの配置 `guid` には、、、 `id` および属性があり `priority` ます。 GUID と ID は、配置されている項目の GUID と ID と一致する必要があります。 属性は、 `priority` 他の項目に関する項目の配置を制御します。 IDE では、同じ優先順位を持つ複数の項目がマージされると、パッケージがビルドされるたびに同じ順序でパッケージリソースが読み込まれるとは限らないため、配置が未定義になります。

メニューまたはグループが複数の場所に表示される場合は、そのメニューまたはグループのすべての子が各インスタンスに表示されます。

## <a name="command-visibility-and-context"></a>コマンドの可視性とコンテキスト
複数の Vspackage がインストールされている場合、メニュー、メニュー項目、およびツールバーの高まっによって IDE が乱雑になることがあります。 この問題を回避するには、 *表示の制約* とコマンドフラグを使用して、個々の UI 要素の表示を制御できます。

### <a name="visibility-constraints"></a>可視性の制約
可視性の制約は、セクションの [VisibilityItem 要素](../../extensibility/visibilityitem-element.md) として設定され `VisibilityConstraints` ます。 可視性の制約では、ターゲット項目が表示される特定の UI コンテキストを定義します。 このセクションに含まれているメニューまたはコマンドは、定義されているコンテキストのいずれかがアクティブな場合にのみ表示されます。 メニューまたはコマンドがこのセクションで参照されていない場合は、常に既定で表示されます。 このセクションは、グループには適用されません。

`VisibilityItem` 要素には、次のように3つの属性が必要です。 `guid` `id` ターゲットの UI 要素のおよびと `context` です。 属性は、 `context` ターゲット項目を表示するタイミングを指定し、有効な UI コンテキストをその値として受け取ります。 Visual Studio の UI コンテキスト定数は、クラスのメンバーです <xref:Microsoft.VisualStudio.VSConstants> 。 すべて `VisibilityItem` の要素は、1つのコンテキスト値のみを取ることができます。 2つ目のコンテキストを適用するには、 `VisibilityItem` 次の例に示すように、同じ項目を指す2番目の要素を作成します。

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

### <a name="command-flags"></a>コマンドフラグ
次のコマンドフラグは、それらが適用されるメニューとコマンドの可視性に影響を与える可能性があります。

`AlwaysCreate` メニューは、グループまたはボタンがない場合でも作成されます。

有効期間: `Menu`

`CommandWellOnly` コマンドがトップレベルメニューに表示されず、追加のシェルカスタマイズに使用できるようにする場合は、このフラグを適用します。たとえば、キーにバインドします。 VSPackage をインストールした後、ユーザーは [ **オプション** ] ダイアログボックスを開き、[ **キーボード環境** ] カテゴリの下にあるコマンドの配置を編集することで、これらのコマンドをカスタマイズできます。 ショートカットメニュー、ツールバー、メニューコントローラー、またはサブメニューの配置には影響しません。

有効な対象: `Button` 、 `Combo`

`DefaultDisabled` 既定では、コマンドを実装する VSPackage が読み込まれていない場合、または QueryStatus メソッドが呼び出されていない場合、コマンドは無効になります。

有効な対象: `Button` 、 `Combo`

`DefaultInvisible` 既定では、コマンドを実装する VSPackage が読み込まれていない場合、または QueryStatus メソッドが呼び出されていない場合、コマンドは非表示になります。

はフラグと組み合わせる必要があり `DynamicVisibility` ます。

有効な対象: `Button` 、 `Combo` 、 `Menu`

`DynamicVisibility` コマンドの表示は、 `QueryStatus` セクションに含まれているメソッドまたはコンテキスト GUID を使用して変更できます `VisibilityConstraints` 。

ツールバーではなく、メニューに表示されるコマンドに適用されます。 `OLECMDF_INVISIBLE`メソッドからフラグが返された場合、最上位のツールバー項目は無効にすることができますが、非表示にすることはできません `QueryStatus` 。

メニューでは、このフラグは、メンバーが非表示のときに自動的に非表示にする必要があることも示しています。 このフラグは、通常、トップレベルのメニューには既にこの動作があるため、サブメニューに割り当てられます。

はフラグと組み合わせる必要があり `DefaultInvisible` ます。

有効な対象: `Button` 、 `Combo` 、 `Menu`

`NoShowOnMenuController` このフラグを持つコマンドがメニューコントローラーに配置されている場合、このコマンドはドロップダウンリストに表示されません。

有効期間: `Button`

コマンドフラグの詳細については、 [commandflag 要素](../../extensibility/command-flag-element.md) のドキュメントを参照してください。

#### <a name="general-requirements"></a>一般的な要件
コマンドは、表示して有効にする前に、次の一連のテストに合格する必要があります。

- コマンドが正しく配置されています。

- `DefaultInvisible`フラグが設定されていません。

- 親メニューまたはツールバーが表示されます。

- [VisibilityConstraints element](../../extensibility/visibilityconstraints-element.md)セクションにコンテキストエントリがあるため、コマンドは非表示になりません。

- インターフェイスを実装する VSPackage コードは、 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> コマンドを表示して有効にします。 インターフェイスコードをインターセプトして操作していません。

- ユーザーがコマンドをクリックすると、 [ルーティングアルゴリズム](../../extensibility/internals/command-routing-algorithm.md)に記載されている手順に従います。

## <a name="call-pre-defined-commands"></a>定義済みコマンドの呼び出し
使用される [コマンド要素](../../extensibility/usedcommands-element.md) は、vspackage が他の vspackage または IDE によって提供されるコマンドにアクセスできるようにします。 これを行うには、使用するコマンドの GUID と ID を持つ、使用する [コマンド要素](../../extensibility/usedcommand-element.md) を作成します。 これにより、現在の Visual Studio の構成に含まれていない場合でも、Visual Studio によってコマンドが読み込まれるようになります。 詳細については、「 [Used command 要素](../../extensibility/usedcommand-element.md)」を参照してください。

## <a name="interface-element-appearance"></a>インターフェイス要素の外観
コマンド要素の選択と配置に関する考慮事項は次のとおりです。

- [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] には、配置に応じて異なるさまざまな UI 要素が用意されています。

- フラグを使用して定義された UI 要素は、 `DefaultInvisible` メソッドの VSPackage 実装によって表示されていない場合 <xref:EnvDTE.IDTCommandTarget.QueryStatus%2A> 、またはセクション内の特定の ui コンテキストに関連付けられていない場合は、IDE に表示されません `VisibilityConstraints` 。

- コマンドが正常に配置されていても、表示されない場合があります。 これは、VSPackage が実装している (または実装されていない) インターフェイスによっては、IDE が一部のコマンドを自動的に非表示にしたり表示したりするためです。 たとえば、VSPackage の一部のビルドインターフェイスを実装すると、ビルド関連のメニュー項目が自動的に表示されます。

- `CommandWellOnly`UI 要素の定義にフラグを適用すると、そのコマンドがカスタマイズによってのみ追加されることになります。

- コマンドは、特定の UI コンテキストでのみ使用できます。たとえば、IDE がデザインビューのときにダイアログボックスが表示される場合にのみ使用できます。

- 特定の UI 要素が IDE に表示されるようにするには、1つまたは複数のインターフェイスを実装するか、コードを記述する必要があります。

## <a name="see-also"></a>関連項目
- [メニューとコマンドを拡張する](../../extensibility/extending-menus-and-commands.md)
