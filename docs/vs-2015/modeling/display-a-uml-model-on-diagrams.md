---
title: ダイアグラムに UML モデルを表示する |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- UML API
ms.assetid: adf1f1f2-2ad9-4ade-82de-c6a5194ab471
caps.latest.revision: 25
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 06a22161068dd7604fe7bb4153e322c0954b89d2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85533019"
---
# <a name="display-a-uml-model-on-diagrams"></a>図に UML モデルを表示する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio に対する拡張機能のプログラム コードでは、モデル要素が図上でどのように表示されるかを制御できます。 UML モデルをサポートする Visual Studio のバージョンを確認するには、「 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)」を参照してください。

このトピックの内容:
- [図の要素を表示するには](#Display)

- [要素を表す図形へのアクセス](#GetShapes)

- [図形の移動とサイズ変更](#Moving)

- [ダイアグラムから図形を削除するには](#Removing)

- [ダイアグラムのオープン処理と作成](#Opening)

- [例: 図形を整列させるためのコマンド](#AlignCommand)

## <a name="to-display-an-element-on-a-diagram"></a><a name="Display"></a> 図に要素を表示するには
 ユース ケースやアクションなどの要素を作成すると、ユーザーはそれらを UML モデル エクスプ ローラーで表示できるようになりますが、いつも自動的に図に表示されるわけではありません。 場合によっては、それを表示するコードを記述する必要があります。 次の表に代替手段を示します。

|要素の型|次に例を示します。|表示するためのコード|
|---------------------|-----------------|-------------------------------------|
|分類子|`Class`<br /><br /> `Component`<br /><br /> `Actor`<br /><br /> `Use Case`|指定した図に関連付けられた図形を作成します。 分類子ごとに任意の数の図形を作成することができます。<br /><br /> `diagram.Display<modelElementType>`<br /><br /> `(modelElement, parentShape,`<br /><br /> `xPosition , yPosition);`<br /><br /> 図の最上位の図形については、`parentShape` を `null` に設定します。<br /><br /> 1 つの図形を別の図形の中に表示するには、次のようにします。<br /><br /> `IShape<IUseCase> usecaseShape =`<br /><br /> `useCaseDiagram.Display`<br /><br /> `(useCase,`<br /><br /> `subsystemShape,`<br /><br /> `subsystemShape.XPosition + 5,`<br /><br /> `subsystemShape.YPosition + 5);`**注:** **Ilinて undo**トランザクション内で表示を実行した場合、メソッドは no を返すことがあり `IShape` ます。 ただし、図形は正しく作成され、`IElement.Shapes().` を使用してアクセスすることはできます。|
|分類子の子|属性、操作、<br /><br /> パート、ポート|自動 - コード不要です。<br /><br /> 親の一部として表示されます。|
|動作|相互作用 (シーケンス)、<br /><br /> アクティビティ|適切な図に動作をバインドします。<br /><br /> 各動作は、一度に最大で 1 つの図にバインドできます。<br /><br /> 次に例を示します。<br /><br /> `sequenceDiagram.Bind(interaction);`<br /><br /> `activityDiagram.Bind(activity);`|
|動作の子|生存線、メッセージ、操作、オブジェクト ノード|自動 - コード不要です。<br /><br /> 親が図にバインドされている場合に表示されます。|
|リレーションシップ|関連、汎化、フロー、依存関係|自動 - コード不要です。<br /><br /> 両端が表示されるすべての図に表示されます。|

## <a name="accessing-the-shapes-that-represent-an-element"></a><a name="GetShapes"></a> 要素を表す図形へのアクセス
 要素を表す図形は、次の型に属します。

 `IShape`

 `IShape<` *ElementType* `>`

 ここで、 *ElementType* は、やなどのモデル要素の型です `IClass` `IUseCase` 。

|構文|説明|
|-|-|
|`anElement.Shapes ()`|開いている図でこの要素を表すすべての `IShapes`。|
|`anElement.Shapes(aDiagram)`|特定の図でこの要素を表すすべての `IShapes`。|
|`anIShape.GetElement()`|図形が表す `IElement`。 通常は、これを IElement のサブクラスにキャストします。|
|`anIShape.Diagram`|図形を格納している `IDiagram`。|
|`anIShape.ParentShape`|`anIShape` を格納している図形。 たとえば、ポート シェイプは、コンポーネント図形内に格納されます。|
|`anIShape.ChildShapes`|`IShape` または `IDiagram` に格納されている図形。|
|`anIShape.GetChildShapes<IUseCase>()`|`IShape` など指定された型の要素を表す、`IDiagram` または `IUseCase` に格納されている図形。|
|`IShape iShape = ...;`<br /><br /> `IShape<IClass> classShape = iShape.ToIShape<IClass>();`<br /><br /> `IClass aClass = classShape.Element;`|ジェネリック `IShape` を厳密に型指定された `IShape<IElement>` にキャストします。|
|`IShape<IClassifier> classifierShape;`<br /><br /> `IShape<IUseCase> usecaseShape =`<br /><br /> `classifierShape.ToIShape<IUseCase>();`|図形をパラメーター化された 1 つの図形型から別の型にキャストします。|

## <a name="moving-and-resizing-shapes"></a><a name="Moving"></a> 図形の移動とサイズ変更

|構文|説明|
|-|-|
|`anIShape.Move(x, y, [width], [height])`|図形を移動またはサイズ変更します。|
|`IDiagram.EnsureVisible( IEnumerable<IShape> shapes, bool zoomToFit = false)`|ウィンドウをアクティブ化し、所定のすべての図形が図に表示されるようにスクロールします。 すべての図形が図に配置されている必要があります。 `zoomToFit` が True の場合、すべての図形が表示されるように、必要に応じて図が拡大縮小されます。|

 例については、「 [アラインメントコマンドの定義](#AlignCommand)」を参照してください。

## <a name="to-remove-a-shape-from-a-diagram"></a><a name="Removing"></a> 図形を図から削除するには
 一部の種類の要素の図形は、要素を削除せずに削除できます。

|モデル要素|図形を削除するには|
|-------------------|-------------------------|
|分類子: クラス、インターフェイス、列挙、アクター、ユース ケース、またはコンポーネント|`shape.Delete();`|
|動作: 相互作用またはアクティビティ|図をプロジェクトから削除できます。 `IDiagram.FileName` を使用してパスを取得します。<br /><br /> これによってモデルから動作が削除されることはありません。|
|その他のすべての図形|図から他の図形を明示的に削除することはできません。 モデルから要素が削除される、または図から親シェイプが削除されると、図形は自動的に削除されます。|

## <a name="opening-and-creating-diagrams"></a><a name="Opening"></a> ダイアグラムを開いて作成する

### <a name="to-access-the-users-current-diagram-from-a-command-or-gesture-extension"></a>コマンドまたはジェスチャ拡張機能から、ユーザーの現在のダイアグラムにアクセスするには
 このインポートされたプロパティをクラスで宣言します。

 `[Import]`

 `IDiagramContext Context { get; set; }`

 メソッドで、ダイアグラムにアクセスします。

 `IClassDiagram classDiagram =`

 `Context.CurrentDiagram as IClassDiagram;`

> [!NOTE]
> `IDiagram` のインスタンス (および、`IClassDiagram` など、そのサブタイプ) は、処理中のコマンド内でのみ有効です。 ユーザーにコントロールが戻されている間は、持続する変数に `IDiagram` オブジェクトを保持することは推奨されません。

 詳細については、「 [モデリング図のメニューコマンドの定義](../modeling/define-a-menu-command-on-a-modeling-diagram.md)」を参照してください。

### <a name="to-obtain-a-list-of-open-diagrams"></a>開いている図の一覧を取得するには
 プロジェクトで現在開いている図の一覧:

```
Context.CurrentDiagram.ModelStore.Diagrams()
```

## <a name="to-access-the-diagrams-in-a-project"></a>プロジェクト内の図にアクセスするには
 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] API を使用すると、モデリング プロジェクトおよび図を開いたり作成したりすることができます。

 `EnvDTE.ProjectItem` から `IDiagramContext` へのキャストに注目してください。

```

      using EnvDTE; // Visual Studio API
...
[Import]
public IServiceProvider ServiceProvider { get; set; }
...
// Get Visual Studio API
DTE dte = ServiceProvider.GetService(typeof(DTE)) as DTE;
// Get current Visual Studio project
Project project = dte.ActiveDocument.ProjectItem.ContainingProject;
// Open and process every diagram in the project.
foreach (ProjectItem item in project.ProjectItems)
{
  // Cast ProjectItem to IDiagramContext
  IDiagramContext context = item as IDiagramContext;
  if (context == null)
  {
     // This is not a diagram file.
     continue;
  }
  // Open the file and give the window the focus.
  if (!item.IsOpen)
  {
      item.Open().Activate();
  }
  // Get the diagram.
  IDiagram diagram = context.CurrentDiagram;
  // Deal with specific diagram types.
  ISequenceDiagram seqDiagram = diagram as ISequenceDiagram;
  if (seqDiagram != null)
  { ... } } }
```

 `IDiagram` のインスタンスおよびそのサブタイプは、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] にコントロールを戻した後は有効ではありません。

 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] プロジェクトからモデル ストアを取得することもできます。

```

      Project project = ...;
IModelStore modelStore = (project as IModelingProject).Store;
```

## <a name="example-command-for-aligning-shapes"></a><a name="AlignCommand"></a> 例: 図形を整列するためのコマンド
 次のコードは、図形を適切に揃えるメニュー コマンドを実装します。 ユーザーはまず、2 つ以上の図形を、垂直方向または水平方向のおよその場所に配置する必要があります。 その後、整列のコマンドを使用して中心を揃えることができます。

 このコマンドを使用できるようにするには、このコードをメニュー コマンド プロジェクトに追加し、結果として得られる拡張機能をユーザーに配置します。 詳細については、「 [モデリング図のメニューコマンドの定義](../modeling/define-a-menu-command-on-a-modeling-diagram.md)」を参照してください。

```csharp
using System;
using System.Collections.Generic;
using System.ComponentModel.Composition;
using System.Linq;
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Presentation;
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml;
using Microsoft.VisualStudio.Modeling.ExtensionEnablement;

namespace AlignCommand
{
  // Implements a command to align shapes in a UML class diagram.
  // The user first selects shapes that are roughly aligned either vertically or horizontally.
  // This command will straighten them up.

  // Place this file in a menu command extension project.
  // See https://msdn.microsoft.com/library/ee329481.aspx

  [Export(typeof(ICommandExtension))]
  [ClassDesignerExtension] // TODO: Add other diagram types if needed
  class CommandExtension : ICommandExtension
  {
    /// <summary>
    /// See https://msdn.microsoft.com/library/ee329481.aspx
    /// </summary>
    [Import]
    IDiagramContext context { get; set; }

    /// <summary>
    /// Transaction context.
    /// See https://msdn.microsoft.com/library/ee330926.aspx
    /// </summary>
    [Import]
    ILinkedUndoContext linkedUndo { get; set; }

    /// <summary>
    /// Called when the user selects the command.
    /// </summary>
    /// <param name="command"></param>
    public void Execute(IMenuCommand command)
    {
      Align(context.CurrentDiagram.SelectedShapes);
    }

    /// <summary>
    /// Called when the user right-clicks on the diagram.
    /// Determines whether the command is enabled.
    /// </summary>
    /// <param name="command"></param>
    public void QueryStatus(IMenuCommand command)
    {
      IEnumerable<IShape> currentSelection = context.CurrentDiagram.SelectedShapes;
      // Make it visible if there are shapes selected:
      command.Visible = currentSelection.Count() > 0 && !(currentSelection.FirstOrDefault() is IDiagram);

      // Make it enabled if there are two or more shapes that are roughly in line:
      command.Enabled = currentSelection.Count() > 1
        && (HorizontalAlignCenter(currentSelection) > 0.0
        || VerticalAlignCenter(currentSelection) > 0.0);

    }

    /// <summary>
    /// Title of the menu command.
    /// </summary>
    public string Text
    {
      get { return "Align Shapes"; }
    }

    /// <summary>
    /// Find a horizontal line that goes through a list of shapes.
    /// </summary>
    /// <param name="shapes"></param>
    /// <returns></returns>
    private static double HorizontalAlignCenter(IEnumerable<IShape> shapes)
    {
      double Y = -1.0;
      double top = 0.0, bottom = shapes.First().Bottom();
      foreach (IShape shape in shapes)
      {
        top = Math.Max(top, shape.Top());
        bottom = Math.Min(bottom, shape.Bottom());
      }
      if (bottom > top) Y = (bottom + top) / 2.0;
      return Y;
    }

    /// <summary>
    /// Find a vertical line that goes through a list of shapes.
    /// </summary>
    /// <param name="shapes"></param>
    /// <returns></returns>
    private static double VerticalAlignCenter(IEnumerable<IShape> shapes)
    {
      double X = -1.0;
      double left = 0.0, right = shapes.First().Right();
      foreach (IShape shape in shapes)
      {
        left = Math.Max(left, shape.Left());
        right = Math.Min(right, shape.Right());
      }
      if (right > left) X = (right + left) / 2.0;
      return X;
    }

    /// <summary>
    /// Line up those shapes that are roughly aligned.
    /// </summary>
    /// <param name="shapes"></param>
    private void Align(IEnumerable<IShape> shapes)
    {
      if (shapes.Count() > 1)
      {
        // The shapes must all overlap either horizontally or vertically.
        // Find a horizontal line that is covered by all the shapes:
        double Y = HorizontalAlignCenter(shapes);
        if (Y > 0.0) // Negative if they don't overlap.
        {
          // Adjust all the shape positions in one transaction:
          using (ILinkedUndoTransaction t = linkedUndo.BeginTransaction("align"))
          {
            foreach (IShape shape in shapes)
            {
              shape.AlignYCenter(Y);
            }
            t.Commit();
          }
        }
        else
        {
          // Find a vertical line that is covered by all the shapes:
          double X = VerticalAlignCenter(shapes);
          if (X > 0.0) // Negative if they don't overlap.
          {
            // Adjust all the shape positions in one transaction:
            using (ILinkedUndoTransaction t = linkedUndo.BeginTransaction("align"))
            {
              foreach (IShape shape in shapes)
              {
                shape.AlignXCenter(X);
              }
              t.Commit();
            }
          }
        }
      }
    }
  }

  /// <summary>
  /// Convenience extensions for IShape.
  /// </summary>
  public static class IShapeExtension
  {
    public static double Bottom(this IShape shape)
    {
      return shape.YPosition + shape.Height;
    }

    public static double Top(this IShape shape)
    {
      return shape.YPosition;
    }

    public static double Left(this IShape shape)
    {
      return shape.XPosition;
    }

    public static double Right(this IShape shape)
    {
      return shape.XPosition + shape.Width;
    }

    public static void AlignYCenter(this IShape shape, double Y)
    {
      shape.Move(shape.XPosition, Y - shape.YCenter());
    }

    public static void AlignXCenter(this IShape shape, double X)
    {
      shape.Move(X - shape.XCenter(), shape.YPosition);
    }

    /// <summary>
    /// We can adjust what bit of the shape we want to be aligned.
    /// The default is the center of the shape.
    /// </summary>
    /// <param name="shape"></param>
    /// <returns></returns>
    public static double YCenter(this IShape shape)
    {
        return shape.Height / 2.0;
    }

    /// <summary>
    /// We can adjust what bit of the shape we want to be aligned.
    /// The default is the center of the shape.
    /// </summary>
    /// <param name="shape"></param>
    /// <returns></returns>
    public static double XCenter(this IShape shape)
    {
        return shape.Width / 2.0;
    }
  }
}

```

## <a name="see-also"></a>参照
 [Uml モデルとダイアグラムの拡張](../modeling/extend-uml-models-and-diagrams.md) [uml モデルへの移動](../modeling/navigate-the-uml-model.md)
 