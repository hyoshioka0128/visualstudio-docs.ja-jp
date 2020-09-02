---
title: ドメイン プロパティ値変更ハンドラー
ms.date: 03/22/2018
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, overriding event handlers
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2f23984d6c4723b020b361e1da30363442966ea7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "75594709"
---
# <a name="domain-property-value-change-handlers"></a>ドメインプロパティ値の変更ハンドラー

Visual Studio ドメイン固有言語では、ドメインプロパティの値が変更されると、 `OnValueChanging()` `OnValueChanged()` ドメインプロパティハンドラーでメソッドとメソッドが呼び出されます。 変更に応答するために、これらのメソッドをオーバーライドできます。

## <a name="override-the-property-handler-methods"></a>プロパティハンドラーメソッドのオーバーライド

ドメイン固有言語の各ドメイン プロパティは親のドメイン クラス内で入れ子になっているクラスにより処理されます。 その名前は、 *PropertyName*propertyhandler という形式に従います。 このプロパティハンドラークラスを検査するには、ファイルを **生成**します。 このクラスで、`OnValueChanging()` は値が変更される直前に呼び出され、`OnValueChanged()` は値が変更された直後に呼び出されます。

たとえば、という名前の `Comment` 文字列ドメインプロパティとという名前の整数プロパティを持つという名前のドメインクラスがあるとし `Text` `TextLengthCount` ます。 `TextLengthCount`常に文字列の長さが含まれるようにするには `Text` 、Dsl プロジェクト内の別のファイルに次のコードを記述します。

```csharp
// Domain Class "Comment":
public partial class Comment
{
  // Domain Property "Text":
  partial class TextPropertyHandler
  {
    protected override void OnValueChanging(CommentBase element, string oldValue, string newValue)
    {
      base.OnValueChanging(element, oldValue, newValue);

      // To update values outside the Store, write code here.

      // Let the transaction manager handle undo:
      Store store = element.Store;
      if (store.InUndoRedoOrRollback || store.InSerializationTransaction) return;

      // Update values in the Store:
      this.TextLengthCount = newValue.Length;
    }
  }
}
```

プロパティ ハンドラーについては次の点に注意してください。

- プロパティ ハンドラー メソッドは、ユーザーがドメイン プロパティに変更を加えたときと、プログラム コードがプロパティに別の値を割り当てたときの両方で呼び出されます。

- メソッドは値が実際に変更された時点でのみ呼び出されます。 プログラム コードにより現在の値に等しい値が代入された場合、ハンドラーは呼び出されません。

- 計算されるドメイン プロパティおよびカスタム ストレージ ドメイン プロパティには OnValueChanged メソッドおよび OnValueChanging メソッドがありません。

- 変更ハンドラーを使用して新しい値を変更することはできません。 たとえば、値を特定の範囲に制限する場合などは、`ChangeRule` を定義します。

- リレーションシップのロールを表すプロパティに変更ハンドラーを追加することはできません。 その代わり、リレーションシップ クラス上で `AddRule` および `DeleteRule` を定義します。 これらの規則は、リンクが作成または変更されるとトリガーされます。 詳細については、「 [ルールによってモデル内の変更が反映される](../modeling/rules-propagate-changes-within-the-model.md)」を参照してください。

### <a name="changes-in-and-out-of-the-store"></a>ストア内外の変更

プロパティ ハンドラー メソッドは変更を開始したトランザクションの内部で呼び出されます。 したがって、新しいトランザクションを開かずに、ストア内でより多くの変更を加えることができます。 変更により追加のハンドラーが呼び出される場合があります。

トランザクションが元に戻されている場合、再実行されている場合、またはロールバックされている場合は、ストア内に変更を加えること、つまり、モデル要素、リレーションシップ、図形、コネクタ、図、またはそれらのプロパティに変更を加えることはできません。

さらに、モデルがファイルから読み込まれているときは、通常、値を更新しません。

したがって、モデルに対する変更は次のようなテストで保護する必要があります。

```csharp
if (!store.InUndoRedoOrRollback && !store. InSerializationTransaction)
{
   this.TextLength = ...; // in-store changes
}
```

対照的に、プロパティ ハンドラーが、たとえばファイル、データベース、またはストア以外の変数など、ストアの外側に変更を伝達する場合、ユーザーが元に戻したり、やり直したりするときに、外部の値が更新されるように、それらの変更を常に実行する必要があります。

### <a name="cancel-a-change"></a>変更の取り消し

変更を防ぐ場合、現在のトランザクションをロールバックできます。 たとえば、プロパティが常に特定の範囲内になるようにすることが望ましい場合があるかもしれません。

```csharp
if (newValue > 10)
{
   store.TransactionManager.CurrentTransaction.Rollback();
   System.Windows.Forms.MessageBox.Show("Value must be less than 10");
}
```

### <a name="alternative-technique-calculated-properties"></a>代替手法: 計算されるプロパティ

前述の例は OnValueChanged() を使用して、あるドメイン プロパティから別のドメイン プロパティへ値を伝達する方法を示しています。 各プロパティは独自の格納値を持っています。

代わりに、派生したプロパティを Calculated property として定義することを検討できます。 その場合、プロパティは独自のストレージを持たず、値が必要になるときに常に関数が評価されることを定義しています。 詳細については、「 [計算済みおよびカスタムストレージのプロパティ](../modeling/calculated-and-custom-storage-properties.md)」を参照してください。

前の例の代わりに、 **Kind** `TextLengthCount` DSL 定義で**計算**されるの Kind フィールドを設定できます。 このドメインプロパティに対して独自の **Get** メソッドを指定します。 **Get**メソッドは、文字列の現在の長さを返し `Text` ます。

ただし、計算されるプロパティの潜在的な欠点は、値が使用されるたびに式が評価されるため、パフォーマンスの問題が生じる可能性があることです。 また、計算されるプロパティに OnValueChanging() および OnValueChanged() はありません。

### <a name="alternative-technique-change-rules"></a>代替手法: 変更規則

変更を定義すると、プロパティの値が変更されるトランザクションの最後に実行されます。  詳細については、「 [ルールによってモデル内の変更が反映される](../modeling/rules-propagate-changes-within-the-model.md)」を参照してください。

1 つのトランザクション内で複数の変更があった場合、ChangeRule はそれらすべてが完了したときに実行されます。 これに対して、OnValue...メソッドは、一部の変更が実行されていない場合に実行されます。 目的に応じて、ChangeRule が適切である場合があります。

また、変更を使用して、プロパティの新しい値を調整し、特定の範囲内に維持することもできます。

> [!WARNING]
> ある規則がストア コンテンツに対して変更を加えた場合、他の規則とプロパティ ハンドラーがトリガーされることがあります。 規則がそれ自体をトリガーしたプロパティを変更した場合、その規則は再度呼び出されることになります。 終わりのないトリガーにならないように注意して規則を定義してください。

```csharp
using Microsoft.VisualStudio.Modeling;
...
// Change rule on the domain class Comment:
[RuleOn(typeof(Comment), FireTime = TimeToFire.TopLevelCommit)]
class MyCommentTrimRule : ChangeRule
{
  public override void
    ElementPropertyChanged(ElementPropertyChangedEventArgs e)
  {
    base.ElementPropertyChanged(e);
    Comment comment = e.ModelElement as Comment;

    if (comment.Text.StartsWith(" ") || comment.Text.EndsWith(" "))
      comment.Text = comment.Text.Trim();
    // If changed, rule will trigger again.
  }
}

// Register the rule:
public partial class MyDomainModel
{
 protected override Type[] GetCustomDomainModelTypes()
 { return new Type[] { typeof(MyCommentTrimRule) };
 }
}
```

## <a name="example"></a>例

### <a name="description"></a>説明

以下の例はドメイン プロパティのプロパティ ハンドラーをオーバーライドし、`ExampleElement` ドメイン クラスのプロパティが変更された場合、ユーザーに通知します。

### <a name="code"></a>コード

```csharp
using DslModeling = global::Microsoft.VisualStudio.Modeling;
using DslDesign = global::Microsoft.VisualStudio.Modeling.Design;

namespace msft.FieldChangeSample
{
  public partial class ExampleElement
  {
    internal sealed partial class NamePropertyHandler
    {
      protected override void OnValueChanged(ExampleElement element,
         string oldValue, string newValue)
      {
        if (!this.Store.InUndoRedoOrRollback)
        {
           // make in-store changes here...
        }
        // This part is called even in undo:
        System.Windows.Forms.MessageBox.Show("Value Has Changed");
        base.OnValueChanged(element, oldValue, newValue);
      }
    }
  }
}
```
