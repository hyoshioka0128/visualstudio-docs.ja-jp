---
title: 有向グラフマークアップ言語 (DGML) リファレンス |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: reference
ms.assetid: cc3e4ae7-60fa-4e22-9227-98020b480b73
caps.latest.revision: 10
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: c676c57d6e6e6008611133235df8d525752f16b5
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/10/2020
ms.locfileid: "75849500"
---
# <a name="directed-graph-markup-language-dgml-reference"></a>Directed Graph Markup Language (DGML) リファレンス
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Directed Graph Markup Language (DGML) は、視覚化と、複雑性の分析を実行するために使用する情報を記述する、Visual Studio でコード マップを保持するために使用される形式です。 DGML では、単純な XML を使用して、循環と非循環の両方の有向グラフを記述します。 有向グラフは、リンク (エッジ) によって接続されている一連のノードです。 ノードとリンクを使用すると、ネットワーク構造 (ソフトウェア プロジェクトの要素など) を表すことができます。

 一部のバージョンの Visual Studio では、DGML 機能のサブセットのみがサポートされています。「[アーキテクチャツールとモデリングツールのバージョンサポート](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)」を参照してください。

> [!NOTE]
> .dgml ファイルを編集するときは、各要素とその値に使用できる属性が IntelliSense によって識別されます。 属性で色を指定するには、一般的な色の名前 ("Blue" など) または ARGB 16 進値 ("#ffa0b1c3" など) を使用してください。 DGML では、WPF (Windows Presentation Foundation) 色定義形式の小さいサブセットを使用します。 詳細については、「 [Colors クラス](https://msdn.microsoft.com/library/system.windows.media.colors.aspx)」を参照してください。

## <a name="DGML"></a>DGML 構文
 次の表は、DGML で使用される要素の種類について説明しています。

- `<DirectedGraph></DirectedGraph>`

   この要素は、コード マップ (.dgml) ドキュメントのルート要素です。 他のすべての DGML 要素は、この要素のスコープ内に表示されます。

   追加できる属性 (省略可能) は次のとおりです。

   `Background`-マップの背景の色

   `BackgroundImage`-マップの背景として使用するイメージファイルの場所。

   `GraphDirection`-マップがツリーレイアウト (`Sugiyama`) に設定されている場合、ほとんどのリンクが指定した方向 (`TopToBottom`、`BottomToTop`、`LeftToRight`、または `RightToLeft`) になるようにノードを配置します。 「[マップレイアウトの変更](../modeling/browse-and-rearrange-code-maps.md#Selecting)」を参照してください。

   `Layout`-マップを、`None`、`Sugiyama` (ツリーレイアウト)、`ForceDirected` (クイッククラスター)、または `DependencyMatrix`の各レイアウトに設定します。 「[マップレイアウトの変更](../modeling/browse-and-rearrange-code-maps.md#Selecting)」を参照してください。

   `NeighborhoodDistance`-マップがツリーレイアウトまたはクイッククラスターレイアウトに設定されている場合、指定された数 (1-7) のリンクが選択したノードから離れているノードのみを表示します。 「[マップレイアウトの変更](../modeling/browse-and-rearrange-code-maps.md#Selecting)」を参照してください。

   例:

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <DirectedGraph Title="DrivingTest" Background="Blue" xmlns="http://schemas.microsoft.com/vs/2009/dgml">
     <Nodes>
        ...
     </Nodes>
     <Links>
        ...
     </Links>
     <Categories>
        ...
     </Categories>
     <Properties>
        ...
     </Properties>
  </DirectedGraph>
  ```

- `<Nodes></Nodes>`

   この省略可能な要素には、マップ上のノードを定義する `<Node/>` 要素の一覧が含まれます。 詳細については、`<Node/>` 要素を参照してください。

  > [!NOTE]
  > `<Link/>` 要素内の未定義のノードを参照すると、マップは `<Node/>` 要素を自動的に作成します。

   例:

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <DirectedGraph Title="DrivingTest" xmlns="http://schemas.microsoft.com/vs/2009/dgml">
     <Nodes>
        <Node ... />
     </Nodes>
     <Links>
        <Link ... />
     </Links>
  </DirectedGraph>
  ```

- `<Node/>`

   この要素は、単一のノードを定義します。 この要素は、`<Nodes><Nodes/>` 要素の一覧内に表示されます。

   この要素には、次の属性が必要です。

   `Id`-個別の `Label` 属性が指定されていない場合に、ノードの一意の名前と `Label` 属性の既定値。 この名前は、名前を参照するリンクの `Source` 属性または `Target` 属性と一致する必要があります。

   追加できる属性 (省略可能) の一部を次に示します。

   `Label`-ノードの表示名。

   スタイル属性。 「 [Customize code maps by editing the DGML files](../modeling/customize-code-maps-by-editing-the-dgml-files.md)」を参照してください。

   `Category`-この属性を共有する要素を識別するカテゴリの名前。 詳細については、`<Category/>` 要素を参照してください。

   `Property`-同じプロパティ値を持つ要素を識別するプロパティの名前。 詳細については、`<Property/>` 要素を参照してください。

   `Group` - ノードに他のノードが含まれている場合は、この属性を `Expanded` または `Collapsed` に設定して、そのコンテンツの表示と非表示を切り替えます。 `<Link/>` 属性を含み、親ノードをリンク元ノード、子ノードをリンク先ノードとして指定する `Category="Contains"` 要素が必要です。 「[グループコード要素](../modeling/customize-code-maps-by-editing-the-dgml-files.md#OrganizeNodes)」を参照してください。

   `Visibility`-この属性を `Visible`、`Hidden`、または `Collapsed`に設定します。 `System.Windows.Visibility`が使用されます。 「[ノードとリンクの非表示または表示](../modeling/browse-and-rearrange-code-maps.md#HidingShowing)」を参照してください。

   `Reference` - この属性をドキュメントまたは URL へのリンクに設定します。 「[コード要素とリンクへのドキュメントまたは url のリンク」を](../modeling/customize-code-maps-by-editing-the-dgml-files.md#AddReferences)参照してください。

   例:

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <DirectedGraph Title="DrivingTest" xmlns="http://schemas.microsoft.com/vs/2009/dgml">
     <Nodes>
        <Node Id="Driver" Label="Student" Category="Person" />
        <Node Id="Passenger" Label="Instructor" Category="Person" />
        <Node Id="Car" Label="Car" Category="Automobile" />
        <Node Id="Truck" Label="Truck" Category="Automobile" />
     </Nodes>
     <Links>
        <Link ... />
     </Links>
     <Categories>
        <Category Id="Person" Background="Orange" />
        <Category Id="Automobile" Background="Yellow"/>
     </Categories>
  </DirectedGraph>
  ```

- `<Links></Links>`

   この要素には、ノード間のリンクを定義する `<Link>` 要素の一覧が含まれます。 詳細については、`<Link/>` 要素を参照してください。

   例:

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <DirectedGraph Title="DrivingTest" xmlns="http://schemas.microsoft.com/vs/2009/dgml">
     <Links>
        <Link ... />
     </Links>
  </DirectedGraph>
  ```

- `<Link/>`

   この要素は、リンク元ノードをリンク先ノードに接続する単一のリンクを定義します。 この要素は、`<Links></Links>` 要素の一覧内に表示されます。

  > [!NOTE]
  > この要素が未定義のノードを参照すると、マップ ドキュメントでは、指定された属性 (存在する場合) を含むノードが自動的に作成されます。

   この要素には、次の属性が必要です。

   `Source`-リンクのソースノード

   `Target` - リンク先ノード。

   追加できる属性 (省略可能) の一部を次に示します。

   `Label`-リンクの表示名

   スタイル属性。 「 [Customize code maps by editing the DGML files](../modeling/customize-code-maps-by-editing-the-dgml-files.md)」を参照してください。

   `Category`-この属性を共有する要素を識別するカテゴリの名前。 詳細については、`<Category/>` 要素を参照してください。

   `Property`-同じプロパティ値を持つ要素を識別するプロパティの名前。 詳細については、`<Property/>` 要素を参照してください。

   例:

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <DirectedGraph Title="DrivingTest" xmlns="http://schemas.microsoft.com/vs/2009/dgml">
     <Nodes>
        <Node Id="Driver" Label="Student" Category="Person" />
        <Node Id="Passenger" Label="Instructor" Category="Person" />
        <Node Id="Car" Label="Car" Category="Automobile" />
        <Node Id="Truck" Label="Truck" Category="Automobile" />
     </Nodes>
     <Links>
        <Category Id="Person" Background="Orange" />
        <Category Id="Automobile" Background="Yellow"/>
        <Link Source="Driver" Target="Car" Label="Passed" Stroke="Black" Background="Green" Category="PassedTest" />
        <Link Source="Driver" Target="Truck" Label="Failed" Stroke="Black" Background="Red" Category="PassedTest" />
     </Links>
  </DirectedGraph>
  ```

- `<Categories></Categories>`

   この要素には、`<Category/>` 要素の一覧が含まれます。 詳細については、`<Category/>` 要素を参照してください。

   例:

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <DirectedGraph Title="DrivingTest" xmlns="http://schemas.microsoft.com/vs/2009/dgml">
     <Categories>
         <Category ... />
     </Categories>
  </DirectedGraph>
  ```

- `<Category/>`

   この要素は、この属性を共有する要素を識別するために使用される `Category` 属性を定義します。 `Category` 属性を使用すると、マップ要素の整理、継承による共有属性の提供、または追加のメタデータの定義が可能になります。

   この要素には、次の属性が必要です。

   `Id` - カテゴリの一意の名前。`Label` 属性が別途指定されていない場合は、`Label` 属性の既定値です。

   追加できる属性 (省略可能) の一部を次に示します。

   `Label` - カテゴリのわかりやすい名前。

   `BasedOn`-現在の要素の `<Category/>` を継承する親カテゴリ。

   この要素の例では、`FailedTest` カテゴリは、`Stroke` カテゴリから `PassedTest` 属性を継承します。 「 [DGML ファイルを編集してコードマップをカスタマイズ](../modeling/customize-code-maps-by-editing-the-dgml-files.md)する」の「階層カテゴリを作成するには」を参照してください。

   カテゴリでは、マップに表示されるノードおよびリンクの外観を制御するいくつかの基本的なテンプレート動作も提供します。 「 [Customize code maps by editing the DGML files](../modeling/customize-code-maps-by-editing-the-dgml-files.md)」を参照してください。

   例:

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <DirectedGraph Title="DrivingTest" xmlns="http://schemas.microsoft.com/vs/2009/dgml">
     <Nodes>
        <Node Id="Driver" Label="Driver" Category="Person" />
        <Node Id="Car" Label="Car" Category="Automobile" />
        <Node Id="Truck" Label="Truck" Category="Automobile" />
        <Node Id="Passenger" Category="Person" />
     </Nodes>
     <Links>
        <Link Source="Driver" Target="Car" Label="Passed" Category="PassedTest" />
        <Link Source="Driver" Target="Truck" Label="Failed" Category="FailedTest" />
     </Links>
     <Categories>
        <Category Id="Person" Background="Orange" />
        <Category Id="Automobile" Background="Yellow"/>
        <Category Id="PassedTest" Label="Passed" Stroke="Black" Background="Green" />
        <Category Id="FailedTest" Label="Failed" BasedOn="PassedTest" Background="Red" />
     </Categories>
  </DirectedGraph>
  ```

- `<Properties></Properties>`

   この要素には、`<Property/>` 要素の一覧が含まれます。 詳細については、`<Property/>` 要素を参照してください。

   例:

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <DirectedGraph Title="DrivingTest" xmlns="http://schemas.microsoft.com/vs/2009/dgml">
     <Properties>
         <Property ... />
     </Properties>
  </DirectedGraph>
  ```

- `<Property/>`

   この要素は、カテゴリおよびその他のプロパティを含む任意の DGML 要素または属性に値を代入する際に使用できる `Property` 属性を定義します。

   この要素には、次の属性が必要です。

  - `Id`-個別の `Label` 属性が指定されていない場合に、プロパティの一意の名前と、`Label` 属性の既定値。

  - `DataType`-プロパティによって格納されるデータの型

    プロパティを **[プロパティ]** ウィンドウに表示する場合は、`Label` プロパティを使用して、プロパティの表示名を指定します。

    「[コード要素およびリンクにカテゴリを割り当てる」を](../modeling/customize-code-maps-by-editing-the-dgml-files.md#AssignCategories)参照してください。

    例:

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <DirectedGraph Title="DrivingTest" xmlns="http://schemas.microsoft.com/vs/2009/dgml">
     <Nodes>
        <Node Id="Driver" Label="Driver" Category="Person" DrivingAge="18"/>
        <Node Id="Car" Label="Car" Category="Automobile" />
        <Node Id="Truck" Label="Truck" Category="Automobile" />
        <Node Id="Passenger" Category="Person" />
     </Nodes>
     <Links>
        <Link Source="Driver" Target="Car" Label="Passed" Category="PassedTest" />
        <Link Source="Driver" Target="Truck" Label="Failed" Category="FailedTest" />
     </Links>
     <Categories>
        <Category Id="Person" Background="Orange" />
        <Category Id="Automobile" Background="Yellow"/>
        <Category Id="PassedTest" Label="Passed" Stroke="Black" Background="Green" />
        <Category Id="FailedTest" Label="Failed" BasedOn="PassedTest" Background="Red" />
     </Categories>
     <Properties>
         <Property Id="DrivingAge" Label="Driving Age" DataType="System.Int32" />
     </Properties>
  </DirectedGraph>
  ```

### <a name="AddAlias"></a>一般的に使用されるパスのエイリアス
 よく使用されるパスをエイリアスに置き換えると、.dgml ファイルのサイズを小さくして、ファイルの読み込みまたは保存に必要な時間を短縮することができます。 エイリアスを作成するには、.dgml ファイルの末尾に `<Paths></Paths>` セクションを追加します。 このセクションには、パスのエイリアスを定義する `<Path/>` 要素を追加します。

```xml
<Paths>
   <Path Id="MyPathAlias" Value="C:\...\..." />
</Paths>
```

 .Dgml ファイル内の要素からエイリアスを参照するには、\<Path/> 要素の `Id` をドル記号 ($) とかっこ (()) で囲みます。

```xml
<Nodes>
   <Node Id="MyNode" Reference="$(MyPathAlias)MyDocument.txt" />
</Nodes>
<Properties>
   <Property Id="Reference" Label="My Document" DataType="System.String" IsReference="True" />
</Properties>
```

## <a name="see-also"></a>参照
 [ソリューション間の依存関係のマッピング](../modeling/map-dependencies-across-your-solutions.md)[コードマップを使用してアプリケーションをデバッグする](../modeling/use-code-maps-to-debug-your-applications.md)[コードマップアナライザーを使用して潜在的な問題を検出](../modeling/find-potential-problems-using-code-map-analyzers.md)する
