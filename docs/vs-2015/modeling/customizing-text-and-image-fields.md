---
title: テキストフィールドとイメージフィールドをカスタマイズする |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
ms.assetid: a7259fc0-5afa-4356-b27e-5641e01628a9
caps.latest.revision: 4
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: d6baaa9ceba8f40aa5ad7888384027131e0ffe94
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72654982"
---
# <a name="customizing-text-and-image-fields"></a>テキストおよびイメージ フィールドのカスタマイズ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

図形にテキストデコレータを定義すると、その図形はテキストフィールドで表されます。 TextFields およびその他の図形フィールドの初期化の例については、DSL ソリューションでのを調べてください。

 TextField は、ラベルに割り当てられた領域など、図形内の領域を管理するオブジェクトです。 1つの TextField インスタンスは、同じクラスの多くの図形間で共有されます。 TextField インスタンスは、インスタンスごとにラベルのテキストを個別に格納しません。代わりに、 `GetDisplayText(ShapeElement)` メソッドは図形をパラメーターとして受け取り、図形とそのモデル要素の現在の状態に依存するテキストを検索できます。

## <a name="how-the-appearance-of-a-text-field-is-determined"></a>テキストフィールドの外観を決定する方法
 `DoPaint()`メソッドが呼び出され、画面にフィールドが表示されます。 既定値をオーバーライドすることも、 `DoPaint(),` 呼び出すメソッドの一部をオーバーライドすることもできます。 既定のメソッドの次の簡略化されたバージョンは、既定の動作をオーバーライドする方法を理解するのに役立ちます。

```
// Simplified version:
public override void DoPaint(DiagramPaintEventArgs e, ShapeElement parentShape)
{
  string text = GetDisplayText(shape);
  StringFormat format = GetStringFormat(parentShape);
  Brush brush = GetTextBrush(e.View, shape);
  using (Font font = GetFont(shape))
  {
    e.Graphics.DrawString(text, font, brush, format);
  }
}
// StringFormat determines whether the string is centered etc.
// To customize statically for all instances of this shape field,
// assign to DefaultStringFormat.
// To customize dynamically or per shape, override this:
public virtual StringFormat GetStringFormat(ShapeElement shape)
{ return DefaultStringFormat; }

// Override to customize the displayed string:
public virtual string GetDisplayText(ShapeElement shape)
{ return this.GetValue(shape).ToString(); }

// Brush determines the text color.
// To change the brush for every field, change the shape’s styleset.
// To customize to a brush in the style set, override GetTextBrushId.
// To change the brush to non-standard color, override this.
// Should take account of whether selected.
public virtual Brush GetTextBrush(DiagramClientView view, ShapeElement shape)
{ return shape.StyleSet.GetBrush(this.GetTextBrushId(view, shape)); }

// Brush ID selects a brush from a StyleSet.
// Either return a member of DiagramBrushes
// or add your own brush to the shape or application’s styleset.
// Override this to change dynamically or per instance.
// To change statically, just assign to default values.
public virtual StyleSetResourceId GetTextBrushId(DiagramClientView view, ShapeElement shape)
{ return IsSelected(view, shape) ? (view.Focused ? DefaultSelectedTextBrushId
: DefaultInactiveSelectedTextBrushId ) : DefaultTextBrushId ;
}

// Font determines the shape and size of the text.
// To change the font for every field, change the shape’s styleset.
// To customize to a font in the style set, override GetFontId.
// To change the font to a non-standard font, override this.
public virtual Font GetFont(ShapeElement shape)
{ return shape.StyleSet.GetFont(GetFontId(shape)); }

// Selects a font from a styleset.
// Either return a member of DiagramFonts or
// add your own font to the shape or application’s styleset.
// To change statically for all instances of this field,
// assign to DefaultFontId.
// To change per shape or dynamically, override this.
public virtual StyleSetResourceId GetFontId(ShapeElement parentShape)
{ return DefaultFontId; }

```

 メソッドとプロパティには、他にもいくつかのペアがあり `Get` `Default` `DefaultMultipleLine/GetMultipleLine()` ます。 既定のプロパティに値を割り当てて、図形フィールドのすべてのインスタンスの値を変更することができます。 値がある図形インスタンスから別のインスタンスに変化するようにする場合、または図形またはモデル要素の状態に依存する場合は、メソッドをオーバーライドし `Get` ます。

## <a name="static-customizations"></a>静的カスタマイズ
 この図形フィールドのすべてのインスタンスを変更する場合は、まず DSL 定義でプロパティを設定できるかどうかを確認します。 たとえば、プロパティウィンドウでフォントサイズとスタイルを設定できます。

 それ以外の場合は、 `InitializeShapeFields` shape クラスのメソッドをオーバーライドし、テキストフィールドの適切なプロパティに値を割り当て `Default...` ます。

> [!WARNING]
> をオーバーライドするには、 `InitializeShapeFields()` DSL 定義で、shape クラスの **Double 派生** プロパティの生成をに設定する必要があり `true` ます。

 この例では、ユーザーのコメントに使用されるテキストフィールドが図形に含まれています。 標準のコメントフォントを使用します。 スタイルセットの標準フォントであるため、既定のフォント id を設定できます。

```

 partial class ExampleShape
{   protected override void InitializeShapeFields(IList<ShapeField> shapeFields)
    {
      // Fields set up according to DSL Definition:
      base.InitializeShapeFields(shapeFields);
      // Find and update comment field:
      TextField commentField = ShapeElement.FindShapeField(shapeFields, "CommentDecorator") as TextField;
      // Use the standard font for comments:
      commentField.DefaultFontId = DiagramFonts.CommentText;

```

## <a name="dynamic-customizations"></a>動的なカスタマイズ
 形状またはモデル要素の状態に応じて外観が変化するようにするには、の独自のサブクラスを派生させ、 `TextField` 1 つ以上のメソッドをオーバーライドし `Get...` ます。 また、図形の InitializeShapeFields メソッドをオーバーライドし、TextField のインスタンスを独自のクラスのインスタンスに置き換える必要があります。

 次の例では、テキストフィールドのフォントを、図形のモデル要素のブール型ドメインプロパティの状態に依存します。

 このコード例を実行するには、[最小言語] テンプレートを使用して新しい DSL ソリューションを作成します。 ブール型ドメインプロパティを例 `AlternateState` の要素ドメインクラスに追加します。 ExampleShape クラスにアイコンデコレータを追加し、そのイメージをビットマップファイルに設定します。 [ **すべてのテンプレートの変換**] をクリックします。 DSL プロジェクトに新しいコードファイルを追加し、次のコードを挿入します。

 コードをテストするには、F5 キーを押し、デバッグソリューションでサンプルダイアグラムを開きます。 アイコンの既定の状態が表示されます。 図形を選択し、プロパティウィンドウで **Alternatestate** プロパティの値を変更します。 要素名のフォントが変更されます。

```
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.Diagrams;
...

  partial class ExampleShape
  {
    /// <summary>
    /// Compose a list of the fields in this shape.
    /// Called once for each shape class.
    /// </summary>
    protected override void InitializeShapeFields(IList<ShapeField> shapeFields)
    {
      // Fields set up according to DSL Definition:
      base.InitializeShapeFields(shapeFields);
      // Replace the text field for NameDecorator:
      TextField oldField = ShapeElement.FindShapeField(shapeFields, "NameDecorator") as TextField;
      shapeFields.Remove(oldField);
      // Replace with my text field based on DSL Definition values:
      MyTextField newField = new MyTextField(oldField);
      shapeFields.Add(newField);
    }
  }
  /// <summary>
  /// Dynamic font depends on state of model element.
  /// </summary>
  public class MyTextField : TextField
  {
    public MyTextField(TextField prototype)
      : base(prototype.Name)
    {
      DefaultText = prototype.DefaultText;
      DefaultFocusable = prototype.DefaultFocusable;
      DefaultAutoSize = prototype.DefaultAutoSize;
      AnchoringBehavior.MinimumHeightInLines = prototype.AnchoringBehavior.MinimumHeightInLines;
      AnchoringBehavior.MinimumWidthInCharacters = prototype.AnchoringBehavior.MinimumWidthInCharacters;
      DefaultAccessibleState = prototype.DefaultAccessibleState;
    }

    public override System.Drawing.Font GetFont(ShapeElement parentShape)
    {
      // Access the Boolean domain property of the model element:
      if ((parentShape.ModelElement as ExampleElement).AlternateState)
        return new System.Drawing.Font("Callisto", 14.0f,
               System.Drawing.FontStyle.Italic |
               System.Drawing.FontStyle.Bold);
      else
        return base.GetFont(parentShape);
    }

  }

```

## <a name="style-sets"></a>スタイルセット
 前の例は、テキストフィールドを、使用可能な任意のフォントに変更する方法を示しています。 ただし、この方法は、図形またはアプリケーションに関連付けられている一連のスタイルのいずれかに変更することをお勧めします。 これを行うには、 <xref:Microsoft.VisualStudio.Modeling.Diagrams.TextField.GetFontId%2A> または GetTextBrushId () をオーバーライドします。

 または、をオーバーライドして、図形のスタイルセットを変更することを検討してください <xref:Microsoft.VisualStudio.Modeling.Diagrams.ShapeElement.InitializeResources%2A> 。 これには、すべての図形フィールドのフォントとブラシを変更した場合の効果があります。

## <a name="customizing-image-fields"></a>イメージフィールドのカスタマイズ
 図形でイメージデコレータを定義するときに、イメージ図形を定義すると、図形が表示される領域は ImageField によって管理されます。 ImageFields とその他の図形フィールドの初期化の例については、DSL ソリューションでの作成された Code/cs を検査してください。

 ImageField は、デコレータに割り当てられた領域など、図形内の領域を管理するオブジェクトです。 1つの ImageField インスタンスは、同じ shape クラスの多くの図形間で共有されます。 ImageField インスタンスには、図形ごとに個別のイメージが格納されていません。代わりに、 `GetDisplayImage(ShapeElement)` メソッドは図形をパラメーターとして受け取り、図形とそのモデル要素の現在の状態に応じてイメージを検索できます。

 変数イメージなどの特殊な動作が必要な場合は、ImageField から派生した独自のクラスを作成できます。

#### <a name="to-create-a-subclass-of-imagefield"></a>ImageField のサブクラスを作成するには

1. DSL 定義で親図形クラスの **Double 派生** プロパティを生成するように設定します。

2. `InitializeShapeFields`Shape クラスのメソッドをオーバーライドします。

    - DSL プロジェクトに新しいコードファイルを作成し、shape クラスの部分クラス定義を記述します。 メソッド定義をオーバーライドします。

3. のコードを調べ `InitializeShapeFields` ます (& d)。

     オーバーライドメソッドで、基本メソッドを呼び出し、独自のイメージフィールドクラスのインスタンスを作成します。 リスト内の通常の画像フィールドを置き換える場合に使用し `shapeFields` ます。

## <a name="dynamic-icons"></a>動的アイコン
 この例では、図形のモデル要素の状態に応じてアイコンの変更を行います。

> [!WARNING]
> この例では、動的イメージデコレータを作成する方法を示します。 ただし、モデル変数の状態に応じて1つまたは2つのイメージを切り替えるだけの場合は、複数のイメージデコレーターを作成して、図形上の同じ位置に配置し、モデル変数の特定の値に依存するように表示フィルターを設定する方が簡単です。 このフィルターを設定するには、DSL 定義でシェイプマップを選択し、DSL の詳細ウィンドウを開いて、[デコレーター] タブをクリックします。

 このコード例を実行するには、[最小言語] テンプレートを使用して新しい DSL ソリューションを作成します。 ブール型ドメインプロパティを例 `AlternateState` の要素ドメインクラスに追加します。 ExampleShape クラスにアイコンデコレータを追加し、そのイメージをビットマップファイルに設定します。 [ **すべてのテンプレートの変換**] をクリックします。 DSL プロジェクトに新しいコードファイルを追加し、次のコードを挿入します。

 コードをテストするには、F5 キーを押し、デバッグソリューションでサンプルダイアグラムを開きます。 アイコンの既定の状態が表示されます。 図形を選択し、プロパティウィンドウで **Alternatestate** プロパティの値を変更します。 このアイコンは、その図形に対して90度回転して表示されます。

```csharp
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.Diagrams;
...
partial class ExampleShape
{
    /// <summary>
    /// Compose a list of the fields in this shape.
    /// Called once for each shape class.
    /// </summary>
    /// <param name="shapeFields"></param>
    protected override void InitializeShapeFields(IList<ShapeField> shapeFields)
    {
      // Fields set up according to DSL Definition:
      base.InitializeShapeFields(shapeFields);

      // Replace the image field:
      ShapeField oldField = ShapeElement.FindShapeField(shapeFields, "IconDecorator");
      shapeFields.Remove(oldField);
      // Must keep the same name:
      MyImageField newField = new MyImageField(oldField.Name);
      shapeFields.Add(newField);
      newField.DefaultImage = (oldField as ImageField).DefaultImage.Clone() as System.Drawing.Image;
    }
  }

  public class MyImageField : ImageField
  {
    public MyImageField(string tag) : base(tag) { }

    /// <summary>
    /// Get the image for this field in the given shape.
    /// </summary>
    public override System.Drawing.Image GetDisplayImage(ShapeElement parentShape)
    {
      ExampleElement element = parentShape.ModelElement as ExampleElement;
      if (element.AlternateState == true)
        return AlternateImage;
      else
        return base.GetDisplayImage(parentShape);
    }

    private System.Drawing.Image alternateImage;
    public System.Drawing.Image AlternateImage
    {
      get
      {
        if (alternateImage == null)
        {
          // Alternate image is a copy of the default, rotated by 90 degrees:
          alternateImage = this.DefaultImage.Clone() as System.Drawing.Image;
          alternateImage.RotateFlip(System.Drawing.RotateFlipType.Rotate90FlipNone);
        }
        return alternateImage;
      }
    }
  }
}

```

## <a name="see-also"></a>参照
 [図形とコネクタの定義](../modeling/defining-shapes-and-connectors.md)[図の背景画像の設定](../modeling/setting-a-background-image-on-a-diagram.md)[プログラムコードでのモデルの移動および更新コードの](../modeling/navigating-and-updating-a-model-in-program-code.md)[記述ドメイン固有言語のカスタマイズ](../modeling/writing-code-to-customise-a-domain-specific-language.md)
