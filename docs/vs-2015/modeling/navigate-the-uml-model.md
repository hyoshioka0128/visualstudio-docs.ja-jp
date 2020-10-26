---
title: UML モデルのナビゲーション |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- UML API
ms.assetid: 6d789b6d-2aa9-4ceb-92c4-84a300065a76
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 23f87c81e43b2dfafb1c9c78c3135faff809bb9f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "74289856"
---
# <a name="navigate-the-uml-model"></a>UML モデル内を移動する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ここでは、主要な UML モデルの種類について説明します。

## <a name="the-model-elements-model-and-model-store"></a>モデル要素、モデル、およびモデル ストア
 アセンブリ **Microsoft.VisualStudio.Uml.Interfaces.dll** 定義されている型は、UML 仕様で定義されている型に対応しています。 [バージョン 2.1.2](https://www.omg.org/spec/UML/2.1.2/Superstructure/PDF/)。

 UML 仕様の型は、Visual Studio においてインターフェイスとして実現されます。 それぞれの型の前には、"I" という文字が付加されています。 例: [Ielement](/previous-versions/dd516035(v=vs.140))、 [IClass](/previous-versions/dd523539%28v%3dvs.140%29)、 [ielement](/previous-versions/dd481186(v=vs.140))。

 IElement 以外のすべての型は、1 つ以上のスーパータイプのプロパティを継承します。

- モデルの種類の概要については、「 [UML モデル要素の型](../modeling/uml-model-element-types.md)」を参照してください。

- API の詳細については、「 [UML モデリング機能拡張の Api リファレンス](../modeling/api-reference-for-uml-modeling-extensibility.md)」を参照してください。

### <a name="relationships"></a>リレーションシップ
 UML 仕様に定義されているプロパティおよび関係は、.NET プロパティとして実装されます。

 ほとんどの関係では、両方向への移動が可能です。 関係はプロパティのペアであり、各端の型の 1 つのプロパティどうしを結び付けるものです。 たとえば、プロパティ `IElement.Owner` および `IElement.OwnedElements` が関係の両端を表します。 したがって、次の式は常に true と評価されます。

 `IElement c; ...  c.OwnedElements.All(x => x.Owner == c)`

 IAssociation など、多くの関係は、固有のプロパティを指定できるオブジェクトによっても表されます。

 モデルの要素を削除すると、その要素が参加する関係が自動的に削除され、もう一方の端のプロパティが更新されます。

 UML 仕様で 0..1 の多重度がプロパティに割り当てられている場合、その値は `null` になることがあります。 最大値が1を超える多重度は、.NET プロパティの型がであることを意味 `IEnumerable<` *Type* `>` します。

 リレーションシップの走査の詳細については、「 [UML API を使用したリレーションシップのナビゲート](../modeling/navigate-relationships-with-the-uml-api.md)」を参照してください。

### <a name="the-ownership-tree"></a>所有権ツリー
 モデルには、 [Ielement](/previous-versions/dd516035(v=vs.140)) オブジェクトのツリーが含まれています。 どの要素にもプロパティ `OwnedElements` および `Owner` があります。

 ほとんどの場合、`Owner` プロパティおよび `OwnedElements` プロパティの対象は、より具体的な名前を持つ他のプロパティでも参照されます。 たとえば、UML 操作は、いずれも UML クラスによって所有されます。 したがっ [て、ioperation](/previous-versions/dd481186(v=vs.140)) には、 [ioperation クラス](/previous-versions/dd473473%28v%3dvs.140%29)という名前のプロパティと、すべての [ioperation](/previous-versions/dd481186(v=vs.140)) オブジェクトのが含ま `Class == Owner` れます。

 ツリーの最上位要素には所有者がいませんが、 `AuxiliaryConstructs.IModel` です。 IModel は、 `IModelStore` [Imodelstore. Root](/previous-versions/ee789368(v=vs.140))という内に含まれています。

 すべてのモデル要素には、作成時に Owner を指定します。 詳細については、「 [UML モデルでの要素とリレーションシップの作成](../modeling/create-elements-and-relationships-in-uml-models.md)」を参照してください。

 ![クラス ダイアグラム: モデル、ダイアグラム、図形、および要素](../modeling/media/uml-mm1.png)

## <a name="shapes-and-diagrams"></a>図形と図
 UML モデル内の要素を図で表示することができます。 IElement のサブタイプをそれぞれ異なる種類の図に表示できます。

 場合によっては、1 つの要素を複数の図に表示できます。 たとえば、IUseCase 要素には複数の IShapes を追加でき、それらの IShapes を 1 つの図または複数の種類の図に表示できます。

 図形はツリー内に位置付けられます。 ツリーの各端は、ParentShape プロパティと ChildShapes プロパティで表されます。 図は、親のない唯一の図形です。 図のサーフェイス上の図形は、より小さなパートで構成されます。 たとえば、クラスの図形には、属性と操作のコンパートメントがあります。

 図形の詳細については、「 [図に UML モデルを表示する](../modeling/display-a-uml-model-on-diagrams.md)」を参照してください。

## <a name="access-to-the-model-in-extensions"></a>拡張機能でのモデルへのアクセス
 MEF コンポーネントとして定義される [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 拡張機能では、拡張機能が実行されるコンテキストから情報をインポートするプロパティを宣言できます。

|属性の型|アクセスを提供する対象|説明|
|--------------------|----------------------------------|----------------------|
|Microsoft.VisualStudio.ArchitectureTools.Extensibility.Presentation<br /><br /> .IDiagramContext<br /><br /> (Microsoft.VisualStudio.ArchitectureTools.Extensibility.dll 内)|現在のフォーカス図。|[モデリング図にメニュー コマンドを定義する](../modeling/define-a-menu-command-on-a-modeling-diagram.md)|
|Microsoft.VisualStudio.Modeling.ExtensionEnablement<br /><br /> .ILinkedUndoContext<br /><br /> (Microsoft.VisualStudio.Modeling.Sdk.[バージョン].dll 内)|一連の変更をトランザクションにグループ化できます。|[トランザクションを使用して UML モデルの更新をリンクする](../modeling/link-uml-model-updates-by-using-transactions.md)|
|Microsoft.VisualStudio.Shell .SVsServiceProvider<br /><br /> (Microsoft.VisualStudio.Shell.Immutable.[バージョン].dll 内)|ホスト [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]。 ここから、ファイル、プロジェクト、および他の側面にアクセスできます。|[Visual Studio API を使用して UML モデルを開く](../modeling/open-a-uml-model-by-using-the-visual-studio-api.md)|

### <a name="to-get-the-context"></a>コンテキストを取得するには
 次に示すインターフェイスのいずれか一方または両方を拡張機能クラス内で宣言します。

```
[Import] public IDiagramContext DiagramContext { get; set; }

```

 MEF (Managed Extensibility Framework) によりこれらのインターフェイスが定義にバインドされ、これから現在の図、モデル ストア、ルート オブジェクトなどを取得できるようになります。

```
IDiagram diagram = this.DiagramContext.CurrentDiagram;
IClassDiagram classDiagram = diagram as IClassDiagram;
       // or diagrams of other types
IModelStore modelStore = diagram.ModelStore;
IModel model = modelStore.Root;
foreach (IDiagram diagram in modelStore.Diagrams) {...}
foreach (IElement element in modelStore.AllInstances<IUseCase>) {...}
```

### <a name="to-get-the-current-selection"></a>現在の選択項目を取得するには

```
// All selected shapes and their elements
foreach (IShape shape in diagram.SelectedShapes)
{
   IDiagram selectedDiagram = shape as IDiagram;
   if (selectedDiagram != null)
   { // no shape selected - user right-clicked the diagram
     ... Context.CurrentDiagram ...
   }
   else
   {
     IElement selectedElement = shape.Element;
   ...}
// All selected shapes that display a specfic type of element
foreach (IShape<IInterface> in
   diagram.GetSelectedShapes<IInterface>())
{...}
```

## <a name="accessing-another-model-or-diagrams"></a>別のモデルまたは図へのアクセス
 次の操作を行います。

- [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] Modelbus を使用し、さまざまなモデルの要素間のリンクを生成します。 詳細については、「 [UML モデルを他のモデルおよびツールと統合](../modeling/integrate-uml-models-with-other-models-and-tools.md)する」を参照してください。

- モデリング プロジェクトと図を [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ユーザー インターフェイスに表示させず、読み取り専用で読み込みます。 詳細については、「 [プログラムコードで UML モデルを読み取る](../modeling/read-a-uml-model-in-program-code.md)」を参照してください。

- [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] でモデリング プロジェクトと図を開き、コンテンツにアクセスします。 詳細については、「 [Visual STUDIO API を使用して UML モデルを開く](../modeling/open-a-uml-model-by-using-the-visual-studio-api.md)」を参照してください。

## <a name="see-also"></a>こちらもご覧ください

- [UML モデルと図の拡張](../modeling/extend-uml-models-and-diagrams.md)
- [UML API を使用したプログラミング](../modeling/programming-with-the-uml-api.md)
