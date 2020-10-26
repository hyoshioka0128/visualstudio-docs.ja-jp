---
title: シェイプおよびコネクタの更新とモデルへの反映
ms.date: 11/04/2016
ms.topic: conceptual
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 83a43e8570ea65373b8cac0bd3e3e7a8dc1f5791
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "76115024"
---
# <a name="update-shapes-and-connectors-to-reflect-the-model"></a>シェイプおよびコネクタを更新してモデルに反映する

Visual Studio のドメイン固有言語では、図形の外観に基になるモデルの状態を反映させることができます。

このトピックのコード例は、プロジェクトのファイルに追加する必要があり `.cs` `Dsl` ます。 各ファイルには、次のディレクティブが必要です。

```csharp
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.Diagrams;
```

## <a name="set-shape-map-properties-to-control-the-visibility-of-a-decorator"></a>図形マップのプロパティを設定してデコレータの表示を制御する

DSL 定義の図形とドメインクラス間のマッピングを構成することにより、プログラムコードを記述せずにデコレータの可視性を制御できます。 詳細については、「 [ドメイン固有言語を定義する方法](../modeling/how-to-define-a-domain-specific-language.md)」を参照してください。

## <a name="expose-the-color-and-style-of-a-shape-as-properties"></a>図形の色とスタイルをプロパティとして公開する

DSL 定義で、shape クラスを右クリックし、[公開の **追加**] をポイントして、[ **塗りつぶしの色**] などの項目のいずれかをクリックします。

これで、図形には、プログラムコードまたはユーザーとして設定できるドメインプロパティが設定されました。 たとえば、コマンドまたはルールのプログラムコードで設定するには、次のように記述します。

`shape.FillColor = System.Drawing.Color.Red;`

ユーザーではなく、プログラムの制御下でプロパティ変数を作成する場合は、DSL 定義図の [ **塗りつぶしの色** ] などの新しいドメインプロパティを選択します。 次に、プロパティウィンドウで、set **が** 参照可能になる `false` か、または **UI が読み取り専用** に設定され `true` ます。

## <a name="define-change-rules-to-make-color-style-or-location-depend-on-model-element-properties"></a>色、スタイル、または場所をモデル要素のプロパティに依存するように変更規則を定義する
 モデルの他の部分に依存する図形の外観を更新する規則を定義できます。 たとえば、モデル要素のプロパティに応じて図形の色を更新するように、モデル要素に対して変更規則を定義できます。 変更規則の詳細については、「 [規則によってモデル内の変更が反映される](../modeling/rules-propagate-changes-within-the-model.md)」を参照してください。

 ルールは、元に戻すコマンドを実行したときには呼び出されないため、ストア内で保持されているプロパティを更新する場合にのみ使用してください。 これには、図形のサイズや可視性などの一部のグラフィック機能は含まれません。 図形の機能を更新するには、「 [非ストアのグラフィカル機能の更新](#OnAssociatedProperty)」を参照してください。

 次の例では、前の `FillColor` セクションで説明したように、ドメインプロパティとして公開されていることを前提としています。

```csharp
[RuleOn(typeof(ExampleElement))]
  class ExampleElementPropertyRule : ChangeRule
  {
    public override void ElementPropertyChanged(ElementPropertyChangedEventArgs e)
    {
      base.ElementPropertyChanged(e);
      ExampleElement element = e.ModelElement as ExampleElement;
      // The rule is called for every property that is updated.
      // Therefore, verify which property changed:
      if (e.DomainProperty.Id == ExampleElement.NameDomainPropertyId)
      {
        // There is usually only one shape:
        foreach (PresentationElement pel in PresentationViewsSubject.GetPresentation(element))
        {
          ExampleShape shape = pel as ExampleShape;
          // Replace this with a useful condition:
          shape.FillColor = element.Name.EndsWith("3")
                     ? System.Drawing.Color.Red : System.Drawing.Color.Green;
        }
      }
    }
  }
  // The rule must be registered:
  public partial class OnAssociatedPropertyExptDomainModel
  {
    protected override Type[] GetCustomDomainModelTypes()
    {
      List<Type> types = new List<Type>(base.GetCustomDomainModelTypes());
      types.Add(typeof(ExampleElementPropertyRule));
      // If you add more rules, list them here.
      return types.ToArray();
    }
  }
```

## <a name="use-onchildconfigured-to-initialize-a-shapes-properties"></a>OnChildConfigured を使用して図形のプロパティを初期化する

図形の最初の作成時に図形のプロパティを設定するには、 `OnChildConfigured()` ダイアグラムクラスの部分定義でオーバーライドします。 図クラスは DSL 定義で指定されており、生成されたコードは、生成されたコードに含まれて**います。** 次に例を示します。

```csharp
partial class MyLanguageDiagram
{
  protected override void OnChildConfigured(ShapeElement child, bool childWasPlaced, bool createdDuringViewFixup)
  {
    base.OnChildConfigured(child, childWasPlaced, createdDuringViewFixup);
    ExampleShape shape = child as ExampleShape;
    if (shape != null)
    {
      if (!createdDuringViewFixup) return; // Ignore load from file.
      ExampleElement element = shape.ModelElement as ExampleElement;
      // Replace with a useful condition:
      shape.FillColor = element.Name.EndsWith("3")
          ? System.Drawing.Color.Red : System.Drawing.Color.Green;
    }
    // else deal with other types of shapes and connectors.
  }
}
```

このメソッドは、ドメインプロパティと非ストア機能 (図形のサイズなど) の両方に使用できます。

## <a name="use-associatevaluewith-to-update-other-features-of-a-shape"></a><a name="OnAssociatedProperty"></a> AssociateValueWith () を使用して図形のその他の機能を更新する

図形の一部の機能 (影があるかどうかなど)、またはコネクタの矢印のスタイルでは、機能をドメインプロパティとして公開するための組み込みメソッドはありません。  このような機能に対する変更は、トランザクションシステムの制御下にありません。 そのため、ユーザーが Undo コマンドを実行したときにルールが呼び出されないため、ルールを使用してそれらを更新するのは適切ではありません。

代わりに、を使用して、このような機能を更新でき <xref:Microsoft.VisualStudio.Modeling.Diagrams.ShapeElement.OnAssociatedPropertyChanged%2A> ます。 次の例では、コネクタの矢印スタイルは、コネクタによって表示されるリレーションシップのドメインプロパティの値によって制御されています。

```csharp
public partial class ArrowConnector // My connector class.
{
    /// <summary>
    /// Called whenever a registered property changes in the associated model element.
    /// </summary>
    /// <param name="e"></param>
    protected override void OnAssociatedPropertyChanged(VisualStudio.Modeling.Diagrams.PropertyChangedEventArgs e)
    {
      base.OnAssociatedPropertyChanged(e);
      // Can be called for any property change. Therefore,
      // Verify that this is the property we're interested in:
      if ("IsDirected".Equals(e.PropertyName))
      {
        if (e.NewValue.Equals(true))
        { // Update the shape's built-in Decorator feature:
          this.DecoratorTo = LinkDecorator.DecoratorEmptyArrow;
        }
        else
        {
          this.DecoratorTo = null; // No arrowhead.
        }
      }
    }

    // OnAssociatedPropertyChanged is called only for properties
    // that have been registered using AssociateValueWith().
    // InitializeResources is a convenient place to call this.
    // This method is invoked only once per class, even though
    // it is an instance method.
    protected override void InitializeResources(StyleSet classStyleSet)
    {
      base.InitializeResources(classStyleSet);
      AssociateValueWith(this.Store, Wire.IsDirectedDomainPropertyId);
      // Add other properties here.
    }
}
```

`AssociateValueWith()` は、登録する各ドメインプロパティに対して1回呼び出される必要があります。 呼び出された後、指定したプロパティに対する変更は、 `OnAssociatedPropertyChanged()` プロパティのモデル要素を表すすべての図形で呼び出されます。

各インスタンスに対してを呼び出す必要はありません `AssociateValueWith()` 。 InitializeResources はインスタンスメソッドですが、図形クラスごとに1回だけ呼び出されます。
