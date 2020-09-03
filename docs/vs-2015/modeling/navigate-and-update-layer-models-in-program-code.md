---
title: プログラムコード内のレイヤーモデルのナビゲーションと更新 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- layer models, navigating in program code
- layer models, updating in program code
ms.assetid: c60edc87-33ee-4964-a954-40069f9febf3
caps.latest.revision: 22
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 88ab52f1b06e6a2da94d17225bdb26ecec358a6c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72668570"
---
# <a name="navigate-and-update-layer-models-in-program-code"></a>プログラム コードでレイヤー モデル内を移動し、レイヤー モデルを更新する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このトピックでは、プログラム コードを使ってナビゲートおよび更新できるレイヤー モデルの要素と関係について説明します。 ユーザーの視点から見たレイヤー図の詳細については、「 [レイヤー図: 参照](../modeling/layer-diagrams-reference.md) と [レイヤー図: ガイドライン](../modeling/layer-diagrams-guidelines.md)」を参照してください。

 このトピックで説明される `Microsoft.VisualStudio.ArchitectureTools.Extensibility.Layer` モデルは、より一般的な <xref:Microsoft.VisualStudio.GraphModel> モデルの入門となります。 [メニューコマンドまたはジェスチャ拡張機能](../modeling/add-commands-and-gestures-to-layer-diagrams.md)を作成する場合は、モデルを使用し `Layer` ます。 [レイヤー検証拡張機能](../modeling/add-custom-architecture-validation-to-layer-diagrams.md)を記述している場合は、を使用する方が簡単です `GraphModel` 。

## <a name="transactions"></a>トランザクション
 モデルを更新する場合、変更を `ILinkedUndoTransaction` で囲むことを検討します。 これにより変更が 1 つのトランザクションにグループ化されます。 いずれかの変更が失敗した場合、トランザクション全体がロールバックされます。 ユーザーが変更を元に戻した場合は、すべての変更がまとめて元に戻されます。

 詳細については、「 [トランザクションを使用した UML モデルの更新のリンク](../modeling/link-uml-model-updates-by-using-transactions.md)」を参照してください。

```
using (ILinkedUndoTransaction t =
        LinkedUndoContext.BeginTransaction("a name"))
{
    // Make changes here ....
    t.Commit(); // Don't forget this!
}
```

## <a name="containment"></a>Containment
 ![ILayer および ILayerModel は両方とも ILayer を含めることができます。](../modeling/media/layerapi-containment.png "LayerApi_Containment")

 レイヤー ([ILayer](/previous-versions/ff644251(v=vs.140))) とレイヤーモデル ([Ilayermodel](/previous-versions/ff643069(v=vs.140))) には、コメントとレイヤーを含めることができます。

 レイヤー (`ILayer`) は、レイヤー モデル (`ILayerModel`) に含めることも、別の `ILayer` に入れ子にすることもできます。

 コメントまたはレイヤーを作成するには、適切なコンテナーで作成メソッドを使用します。

## <a name="dependency-links"></a>依存関係リンク
 依存関係リンクはオブジェクトによって表されます。 どちらの方向にもナビゲートできます。

 ![ILayerDependencyLink は 2 つの ILayer を接続します。](../modeling/media/layerapi-dependency.png "LayerApi_Dependency")

 依存関係リンクを作成するには、`source.CreateDependencyLink(target)` を呼び出します。

## <a name="comments"></a>コメント
 コメントは、レイヤーまたはレイヤー モデルの中に含めることができ、任意のレイヤー要素にリンクすることもできます。

 ![任意のレイヤー要素にコメントを添付できます。](../modeling/media/layerapi-comments.png "LayerApi_Comments")

 コメントは任意の数の要素 (ゼロ個も可能) にリンクすることができます。

 レイヤー要素にアタッチしたコメントを取得するには、次のコードを使用します。

```csharp
ILayerModel model = diagram.GetLayerModel();
IEnumerable<ILayerComment> comments =
   model.Comments.Where(comment =>
      comment.Links.Any(link => link.Target == layerElement));

```

> [!CAUTION]
> `Comments` の `ILayer` プロパティは、`ILayer` に含まれるコメントを取得します。 そこにリンクされているコメントは取得しません。

 適切なコンテナーで `CreateComment()` を呼び出すことによってコメントを作成します。

 コメントで `CreateLink()` を使用してリンクを作成します。

## <a name="layer-elements"></a>レイヤー要素
 モデルに含めることのできるタイプの要素はすべてレイヤー要素です。

 ![レイヤー図のコンテンツは ILayerElement です。](../modeling/media/layerapi-layerelements.png "LayerApi_LayerElements")

## <a name="properties"></a>Properties
 各 `ILayerElement` には `Properties` という名前の文字列の辞書があります。 この辞書を使うと、任意の情報をレイヤー要素にアタッチできます。

## <a name="artifact-references"></a>成果物参照
 成果物参照 ([Ilayerartifactreference](/previous-versions/ff644536(v=vs.140))) は、レイヤーとプロジェクトアイテム (ファイル、クラス、フォルダーなど) との間のリンクを表します。 ユーザーが、ソリューション エクスプローラー、クラス ビュー、またはオブジェクト ブラウザーからレイヤー図にアイテムをドラッグしてレイヤーを作成または追加すると、成果物が作成されます。 成果物参照はいくつでもレイヤーにリンクできます。

 レイヤー エクスプローラーの各行には成果物参照が表示されます。 詳細については、「 [コードからレイヤー図を作成する](../modeling/create-layer-diagrams-from-your-code.md)」を参照してください。

 成果物参照に関係する主な型およびメソッドは次のとおりです。

 [Ilayerartifactreference](/previous-versions/ff644536(v=vs.140))。 カテゴリ プロパティは、参照される成果物の種類 (クラス、実行ファイル、アセンブリなど) を示します。 カテゴリは、対象となる成果物を識別子が特定する方法を決定します。

 [Artifactreferenceextensions。 CreateArtifactReferenceAsync](/previous-versions/ff695840(v=vs.140)) は、またはから成果物参照を作成します <xref:EnvDTE.Project> <xref:EnvDTE.ProjectItem> 。 これは非同期操作です。 そのため、作成が完了したときに呼び出すコールバックを通常は提供します。

 レイヤー成果物参照は、ユースケース図の成果物と混同してはなりません。

## <a name="shapes-and-diagrams"></a>図形と図
 レイヤーモデル内の各要素を表すために `ILayerElement` 、と [ishape](/previous-versions/ee806673(v=vs.140))の2つのオブジェクトが使用されます。 `IShape` は、図の位置と形のサイズを表します。 レイヤー モデルでは、すべての `ILayerElement` には 1 つの `IShape` があり、レイヤー図のすべての `IShape` には 1 つの `ILayerElement` があります。 `IShape` は UML モデルにも使用されます。 そのため、すべての `IShape` にレイヤー要素があるわけではありません。

 同様に、は `ILayerModel` 1 つの [idiagram](/previous-versions/ee789658(v=vs.140))に表示されます。

 カスタム コマンドまたはジェスチャ ハンドラーのコードでは、`DiagramContext` インポートから現在の図や現在の形の選択を取得できます。

```
public class ... {
[Import]
    public IDiagramContext DiagramContext { get; set; }
...
public void ... (...)
{ IDiagram diagram = this.DiagramContext.CurrentDiagram;
  ILayerModel model = diagram.GetLayerModel();
  if (model != null)
  { foreach (ILayer layer in model.Layers) { ... }}
  foreach (IShape selected in diagram.SelectedShapes)
  { ILayerElement element = selected.GetLayerElement();
    if (element != null) ... }}
```

 ![各 ILayerElement は IShape で表されます。](../modeling/media/layerapi-shapes.png)

 [Ishape](/previous-versions/ee806673(v=vs.140)) と [ISHAPE](/previous-versions/ee789658(v=vs.140)) は、UML モデルを表示するためにも使用されます。 詳細については、「 [図に UML モデルを表示する](../modeling/display-a-uml-model-on-diagrams.md)」を参照してください。

## <a name="see-also"></a>こちらもご覧ください

- [レイヤー図にコマンドおよびジェスチャを追加する](../modeling/add-commands-and-gestures-to-layer-diagrams.md)
- [カスタム アーキテクチャ検証をレイヤー図に追加する](../modeling/add-custom-architecture-validation-to-layer-diagrams.md)
- [レイヤー図へのカスタム プロパティの追加](../modeling/add-custom-properties-to-layer-diagrams.md)
- [レイヤー図: リファレンス](../modeling/layer-diagrams-reference.md)
- [レイヤー図: ガイドライン](../modeling/layer-diagrams-guidelines.md)
- [UML モデルと図の拡張](../modeling/extend-uml-models-and-diagrams.md)
