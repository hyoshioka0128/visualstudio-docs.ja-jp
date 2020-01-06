---
title: プロパティ ウィンドウのカスタマイズ
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, Properties window
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b2cd7d4598040721d3c5b6acb7844f668c72ea09
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75589696"
---
# <a name="customize-the-properties-window"></a>プロパティウィンドウをカスタマイズする

Visual Studio のドメイン固有言語 (DSL) で、[プロパティ] ウィンドウの外観と動作をカスタマイズできます。 DSL 定義では、各ドメインクラスのドメインプロパティを定義します。 既定では、図またはモデルエクスプローラーでクラスのインスタンスを選択すると、すべてのドメインプロパティが [プロパティ] ウィンドウに一覧表示されます。 これにより、ダイアグラムの図形フィールドにマップしていない場合でも、ドメインプロパティの値を表示および編集できます。

## <a name="names-descriptions-and-categories"></a>名前、説明、およびカテゴリ

**名前と表示名**。 ドメインプロパティの定義では、プロパティの表示名は、実行時に [プロパティ] ウィンドウに表示される名前です。 これに対し、この名前は、プロパティを更新するプログラムコードを記述するときに使用されます。 名前は正しい CLR 英数字名にする必要がありますが、表示名にスペースを含めることができます。

DSL 定義でプロパティの名前を設定すると、その表示名が自動的に名前のコピーに設定されます。 "Futex" のような Pascal 形式の名前を記述した場合、表示名には自動的にスペース "燃料ゲージ" が含まれます。 ただし、表示名を明示的に別の値に設定することもできます。

**説明**です。 ドメインプロパティの説明は、次の2つの場所に表示されます。

- ユーザーがプロパティを選択したときに、[プロパティ] ウィンドウの下部に表示されます。 これを使用すると、プロパティが表す内容をユーザーに説明することができます。

- 生成されたプログラムコード内。 ドキュメント機能を使用して API ドキュメントを抽出すると、api のこのプロパティの説明として表示されます。

**カテゴリ**。 カテゴリは、プロパティウィンドウの見出しです。

## <a name="expose-style-features"></a>スタイル機能の公開

グラフィカル要素の動的機能の一部は、ドメインプロパティとして表現したり*公開*したりすることができます。 このように公開されている機能は、ユーザーが更新することができ、プログラムコードによってより簡単に更新できます。

DSL 定義でシェイプクラスを右クリックし、 **[公開の追加]** をポイントして、機能を選択します。

図形では、 **FillColor**、 **OutlineColor**、 **textcolor**、 **OutlineDashStyle**、 **OutlineThickness** 、および**FillGradientMode**の各プロパティを公開できます。 コネクタでは、 **Textcolor**、**ダッシュスタイル**、および**太さ**の各プロパティ`,`**色**を公開できます。 ダイアグラムでは、 **FillColor**プロパティと**textcolor**プロパティを公開できます。

## <a name="forwarding-display-properties-of-related-elements"></a>転送: 関連する要素のプロパティを表示します。

DSL のユーザーがモデル内の要素を選択すると、その要素のプロパティが [プロパティ] ウィンドウに表示されます。 ただし、指定された関連要素のプロパティを表示することもできます。 これは、連携して動作する要素のグループを定義している場合に便利です。 たとえば、main 要素とオプションのプラグイン要素を定義することができます。 メイン要素が図形にマップされていて、もう一方が図形でない場合は、すべてのプロパティを1つの要素上にあるかのように表示すると便利です。

この効果は*プロパティ転送*と呼ばれ、いくつかのケースで自動的に発生します。 それ以外の場合は、ドメイン型記述子を定義することで、プロパティの転送を実現できます。

### <a name="default-property-forwarding-cases"></a>既定のプロパティ転送ケース

ユーザーが図形またはコネクタ、またはエクスプローラーで要素を選択すると、次のプロパティがプロパティウィンドウに表示されます。

- モデル要素のドメインクラスで定義されているドメインプロパティ。基本クラスで定義されているものも含まれます。 例外として、`False`に**参照できるように設定し**たドメインプロパティがあります。

- 多重度が 0 ..1 のリレーションシップによってリンクされる要素の名前。 これにより、リレーションシップのコネクタマッピングが定義されていない場合でも、必要に応じてリンクされた要素を表示するための便利な方法が提供されます。

- 要素をターゲットとする埋め込みリレーションシップのドメインプロパティ。 埋め込みリレーションシップは通常、明示的に表示されないため、ユーザーはプロパティを表示できます。

- 選択された図形またはコネクタで定義されているドメインプロパティ。

### <a name="add-property-forwarding"></a>プロパティ転送の追加

プロパティを転送するには、ドメイン型記述子を定義します。 2つのドメインクラス間にドメインリレーションシップがある場合は、ドメイン型記述子を使用して、最初のクラスのドメインプロパティを2番目のドメインクラスのドメインプロパティの値に設定できます。 たとえば、**書籍**ドメインクラスと**作成者**ドメインクラスとの間にリレーションシップがある場合、ドメイン型記述子を使用して、ユーザーが本を選択したときに本の**著者**の**Name**プロパティをプロパティウィンドウに表示させることができます。

> [!NOTE]
> プロパティ転送は、ユーザーがモデルを編集している場合にのみプロパティウィンドウに影響します。 受信側クラスのドメインプロパティは定義されません。 DSL 定義またはプログラムコードの他の部分で転送されたドメインプロパティにアクセスするには、転送する要素にアクセスする必要があります。

次の手順では、DSL を作成済みであることを前提としています。 最初のいくつかの手順では、前提条件の概要を説明します。

#### <a name="forward-a-property-from-another-element"></a>別の要素からプロパティを転送する

1. 少なくとも2つのクラスを含む [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] ソリューションを作成します。この例では、 **Book**と**Author**と呼ばれています。 **本**と**著者**の間には、どちらの種類のリレーションシップもあります。

    各**ブック**に1つの**作成者**が含まれるように、ソースロール (**書籍**側のロール) の多重度は 0 ..1 または 1 ..1 にする必要があります。

2. **DSL エクスプローラー**で、 **[Book]** domain クラスを右クリックし、 **[Add New domaintypedescriptor]** をクリックします。

    カスタム**プロパティ記述子のパス**という名前のノードが、**カスタム型記述子**ノードの下に表示されます。

3. **[カスタム型記述子]** ノードを右クリックし、 **[Add New PropertyPath]** をクリックします。

    新しいプロパティパスは、 **[カスタムプロパティ記述子のパス]** ノードの下に表示されます。

4. 新しいプロパティパスを選択し、 **[プロパティ]** ウィンドウで、 **[path to property]** を適切なモデル要素のパスに設定します。

    このプロパティの右側にある下矢印をクリックすると、ツリービューでパスを編集できます。 ドメインパスの詳細については、「[ドメインパス構文](../modeling/domain-path-syntax.md)」を参照してください。 編集が完了したら、パスは "ブック名の**作成者/!" に似ています。作成者**。

5. **プロパティ**を**作成者**の**名前**ドメインプロパティに設定します。

6. **表示名**を "**作成者名**" に設定します。

7. すべてのテンプレートを変換し、DSL を構築して実行します。

8. モデル図では、作成者というブックを作成し、参照関係を使用してリンクします。 Book 要素を選択すると、プロパティウィンドウブックのプロパティに加えて作成者名が表示されます。 リンクされた作成者の名前を変更するか、別の作成者にブックをリンクして、ブックの作成者名が変更されていることを確認します。

## <a name="custom-property-editors"></a>カスタムプロパティエディター

[プロパティ] ウィンドウには、各ドメインプロパティの型に対する適切な既定の編集エクスペリエンスが用意されています。 たとえば、列挙型の場合、ユーザーにはドロップダウンリストが表示され、数値プロパティの場合、ユーザーは数字を入力できます。 これは、組み込み型の場合にのみ当てはまります。 外部型を指定した場合、ユーザーはプロパティの値を表示できますが、編集することはできません。

ただし、次のエディターと種類を指定できます。

1. 標準型で使用される別のエディター。 たとえば、文字列プロパティのファイルパスエディターを指定できます。

2. ドメインプロパティの外部型と、その型のエディター。

3. ファイルパスエディターなどの .NET エディター、または独自のカスタムプロパティエディターを作成することができます。

   既定のエディターを持つ、外部型と型の間の変換 (文字列など)。

   DSL では、*外部型*は、単純型 (ブール値や Int32 型など) または文字列ではない任意の型です。

### <a name="define-a-domain-property-that-has-an-external-type"></a>外部型を持つドメインプロパティを定義する

1. **ソリューションエクスプローラー**で、 **Dsl**プロジェクトの外部型を含むアセンブリ (DLL) への参照を追加します。

    アセンブリには、.NET アセンブリまたはユーザーが指定したアセンブリを使用できます。

2. **[ドメインの種類]** ボックスの一覧に型を追加します (まだ作成していない場合)。

   1. DslDefinition を開きます。 **Dsl エクスプローラー**で、ルートノードを右クリックし、 **[新しい外部型の追加]** をクリックします。

        **[ドメインの種類]** ノードの下に新しいエントリが表示されます。

       > [!WARNING]
       > メニュー項目は、 **[ドメインの種類]** ノードではなく、DSL のルートノードにあります。

   2. プロパティウィンドウで、新しい型の名前と名前空間を設定します。

3. 通常の方法でドメインクラスにドメインプロパティを追加します。

    プロパティウィンドウの **[種類]** フィールドで、ドロップダウンリストから外部の種類を選択します。

   この段階では、ユーザーはプロパティの値を表示できますが、編集することはできません。 表示される値は `ToString()` 関数から取得されます。 コマンドやルールなどのプロパティの値を設定するプログラムコードを記述することもできます。

### <a name="set-a-property-editor"></a>プロパティエディターの設定

次の形式で、CLR 属性をドメインプロパティに追加します。

```csharp
[System.ComponentModel.Editor (
   typeof(AnEditor),
   typeof(System.Drawing.Design.UITypeEditor))]
```

プロパティの属性を設定するには、プロパティウィンドウの**カスタム属性**エントリを使用します。

`AnEditor` の型は、2番目のパラメーターで指定した型から派生している必要があります。 2番目のパラメーターは <xref:System.Drawing.Design.UITypeEditor> または <xref:System.ComponentModel.ComponentEditor>のいずれかである必要があります。 詳細については、「 <xref:System.ComponentModel.EditorAttribute>」を参照してください。

独自のエディターまたは .NET エディター (<xref:System.Windows.Forms.Design.FileNameEditor> や <xref:System.Drawing.Design.ImageEditor>など) を指定できます。 たとえば、次の手順を使用して、ユーザーがファイル名を入力できるプロパティを設定します。

#### <a name="define-a-file-name-domain-property"></a>ファイル名ドメインプロパティの定義

1. DSL 定義のドメインクラスにドメインプロパティを追加します。

2. 新しいプロパティを選択します。 プロパティウィンドウの **[カスタム属性]** フィールドに、次の属性を入力します。 この属性を入力するには、省略記号 **[...]** をクリックし、属性名とパラメーターを個別に入力します。

    ```csharp
    [System.ComponentModel.Editor (
       typeof(System.Windows.Forms.Design.FileNameEditor)
       , typeof(System.Drawing.Design.UITypeEditor))]

    ```

3. ドメインプロパティの型は、既定の**文字列**の設定でそのままにします。

4. エディターをテストするには、ユーザーがファイル名エディターを開いてドメインのプロパティを編集できることを確認します。

    1. CTRL キーを押しながら F5 キーを押すか、F5 キーを押します。 デバッグソリューションで、テストファイルを開きます。 ドメインクラスの要素を作成し、それを選択します。

    2. プロパティウィンドウで、ドメイン プロパティを選択します。 [値] フィールドは、省略記号を示しています **[...]** 。

    3. 省略記号をクリックします。 ファイルのダイアログボックスが表示されます。 ファイルを選択して、ダイアログボックスを閉じます。 これで、ファイルパスがドメインプロパティの値になりました。

### <a name="define-your-own-property-editor"></a>独自のプロパティエディターを定義する

独自のエディターを定義できます。 これは、ユーザーが定義した型を編集できるようにするか、標準型を特別な方法で編集するために行います。 たとえば、式を表す文字列をユーザーが入力できるようにすることができます。

<xref:System.Drawing.Design.UITypeEditor>から派生したクラスを記述することによって、エディターを定義します。 クラスは次をオーバーライドする必要があります。

- <xref:System.Drawing.Design.UITypeEditor.EditValue%2A>、ユーザーと対話し、プロパティ値を更新します。

- <xref:System.Drawing.Design.UITypeEditor.GetEditStyle%2A>、エディターでダイアログを開くか、ドロップダウンメニューを提供するかを指定します。

プロパティグリッドに表示されるプロパティの値をグラフィカルに表示することもできます。 これを行うには、`GetPaintValueSupported`をオーバーライドし、`PaintValue`します。  詳細については、「 <xref:System.Drawing.Design.UITypeEditor>」を参照してください。

> [!NOTE]
> **Dsl**プロジェクト内の別のコードファイルにコードを追加します。

例:

```csharp
internal class TextFileNameEditor : System.Windows.Forms.Design.FileNameEditor
{
  protected override void InitializeDialog(System.Windows.Forms.OpenFileDialog openFileDialog)
  {
    base.InitializeDialog(openFileDialog);
    openFileDialog.Filter = "Text files(*.txt)|*.txt|All files (*.*)|*.*";
    openFileDialog.Title = "Select a text file";
  }
}
```

このエディターを使用するには、ドメインプロパティの**カスタム属性**を次のように設定します。

```csharp
[System.ComponentModel.Editor (
   typeof(MyNamespace.TextFileNameEditor)
   , typeof(System.Drawing.Design.UITypeEditor))]
```

詳細については、「 <xref:System.Drawing.Design.UITypeEditor>」を参照してください。

## <a name="provide-a-drop-down-list-of-values"></a>値のドロップダウンリストを指定する

ユーザーが選択できる値の一覧を指定できます。

> [!NOTE]
> この手法では、実行時に変更される可能性がある値の一覧を提供します。 変更されないリストを提供する場合は、代わりに、ドメインプロパティの型として列挙型を使用することを検討してください。

標準値のリストを定義するには、次の形式の CLR 属性をドメインプロパティに追加します。

```csharp
[System.ComponentModel.TypeConverter
(typeof(MyTypeConverter))]
```

<xref:System.ComponentModel.TypeConverter> から派生するクラスを定義します。 **Dsl**プロジェクトの別のファイルにコードを追加します。 例:

```csharp
/// <summary>
/// Type converter that provides a list of values
/// to be displayed in the property grid.
/// </summary>
/// <remarks>This type converter returns a list
/// of the names of all "ExampleElements" in the
/// current store.</remarks>
public class MyTypeConverter : System.ComponentModel.TypeConverter
{
  /// <summary>
  /// Return true to indicate that we return a list of values to choose from
  /// </summary>
  /// <param name="context"></param>
  public override bool GetStandardValuesSupported
    (System.ComponentModel.ITypeDescriptorContext context)
  {
    return true;
  }

  /// <summary>
  /// Returns true to indicate that the user has
  /// to select a value from the list
  /// </summary>
  /// <param name="context"></param>
  /// <returns>If we returned false, the user would
  /// be able to either select a value from
  /// the list or type in a value that is not in the list.</returns>
  public override bool GetStandardValuesExclusive
      (System.ComponentModel.ITypeDescriptorContext context)
  {
    return true;
  }

  /// <summary>
  /// Return a list of the values to display in the grid
  /// </summary>
  /// <param name="context"></param>
  /// <returns>A list of values the user can choose from</returns>
  public override StandardValuesCollection GetStandardValues
      (System.ComponentModel.ITypeDescriptorContext context)
  {
    // Try to get a store from the current context
    // "context.Instance"  returns the element(s) that
    // are currently selected i.e. whose values are being
    // shown in the property grid.
    // Note that the user could have selected multiple objects,
    // in which case context.Instance will be an array.
    Store store = GetStore(context.Instance);

    List<string> values = new List<string>();

    if (store != null)
    {
      values.AddRange(store.ElementDirectory
        .FindElements<ExampleElement>()
        .Select<ExampleElement, string>(e =>
      {
        return e.Name;
      }));
    }
    return new StandardValuesCollection(values);
  }

  /// <summary>
  /// Attempts to get to a store from the currently selected object(s)
  /// in the property grid.
  /// </summary>
  private Store GetStore(object gridSelection)
  {
    // We assume that "instance" will either be a single model element, or
    // an array of model elements (if multiple items are selected).

    ModelElement currentElement = null;

    object[] objects = gridSelection as object[];
    if (objects != null && objects.Length > 0)
    {
      currentElement = objects[0] as ModelElement;
    }
    else
    {
        currentElement = gridSelection as ModelElement;
    }

    return (currentElement == null) ? null : currentElement.Store;
  }

}
```

## <a name="see-also"></a>関連項目

- [プログラム コードにおけるモデル内の移動およびモデルの更新](../modeling/navigating-and-updating-a-model-in-program-code.md)
