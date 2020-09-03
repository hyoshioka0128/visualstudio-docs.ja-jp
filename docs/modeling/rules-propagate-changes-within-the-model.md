---
title: 規則によって変更内容がモデル内に反映される
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, programming domain models
- Domain-Specific Language, rules
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2050fe0ea2d1a9bb0bf278c13c2beb587412c643
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85542559"
---
# <a name="rules-propagate-changes-within-the-model"></a>規則によって変更内容がモデル内に反映される
ストアルールを作成して、視覚化およびモデリング SDK (VMSDK) で、ある要素から別の要素に変更を反映させることができます。 ストア内のいずれかの要素に変更が加えられると、通常、最も外側のトランザクションがコミットされるときに、規則が実行されるようにスケジュールされます。 要素の追加や削除など、さまざまな種類のイベントに対して異なる種類のルールがあります。 ルールは、特定の種類の要素、図形、または図に適用できます。 多くの組み込み機能がルールによって定義されています。たとえば、ルールによって、モデルが変更されたときにダイアグラムが更新されます。 独自の規則を追加することで、ドメイン固有言語をカスタマイズできます。

 ストアルールは、ストア内の変更 (モデル要素、リレーションシップ、図形、コネクタ、およびそれらのドメインプロパティの変更) を反映する場合に特に便利です。 ユーザーが [元に戻す] または [やり直し] コマンドを呼び出しても、規則は実行されません。 代わりに、トランザクションマネージャーによって、ストアの内容が正しい状態に復元されます。 ストアの外部のリソースに変更を反映する場合は、ストアイベントを使用します。 詳細については、「 [イベントハンドラーによって変更がモデル外に反映される](../modeling/event-handlers-propagate-changes-outside-the-model.md)」を参照してください。

 たとえば、ユーザー (またはコード) が型の型の新しい要素を作成するたびに、別の型の他の要素がモデルの別の部分に作成されるように指定するとします。 AddRule を記述して、それを例の Domainclass に関連付けることができます。 ルールにコードを記述して、追加の要素を作成します。

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using Microsoft.VisualStudio.Modeling;

namespace ExampleNamespace
{
 // Attribute associates the rule with a domain class:
 [RuleOn(typeof(ExampleDomainClass), FireTime=TimeToFire.TopLevelCommit)]
 // The rule is a class derived from one of the abstract rules:
 class MyAddRule : AddRule
 {
  // Override the abstract method:
  public override void ElementAdded(ElementAddedEventArgs e)
  {
    base.ElementAdded(e);
    ExampleDomainClass element = e.ModelElement;
    Store store = element.Store;
    // Ignore this call if we're currently loading a model:
    if (store.TransactionManager.CurrentTransaction.IsSerializing)
       return;

    // Code here propagates change as required - for example:
      AnotherDomainClass echo = new AnotherDomainClass(element.Partition);
      echo.Name = element.Name;
      echo.Parent = element.Parent;
    }
  }
 // The rule must be registered:
 public partial class ExampleDomainModel
 {
   protected override Type[] GetCustomDomainModelTypes()
   {
     List<Type> types = new List<Type>(base.GetCustomDomainModelTypes());
     types.Add(typeof(MyAddRule));
     // If you add more rules, list them here.
     return types.ToArray();
   }
 }
}
```

> [!NOTE]
> ルールのコードは、ストア内の要素の状態のみを変更する必要があります。つまり、ルールは、モデル要素、リレーションシップ、図形、コネクタ、図、またはそれらのプロパティのみを変更する必要があります。 ストアの外部のリソースに変更を反映する場合は、ストアイベントを定義します。 詳細については、「 [イベントハンドラーによって変更がモデル外に反映される](../modeling/event-handlers-propagate-changes-outside-the-model.md)」を参照してください。

### <a name="to-define-a-rule"></a>ルールを定義するには

1. 属性をプレフィックスとして付けるクラスとしてルールを定義し `RuleOn` ます。 属性は、ルールをドメインクラス、リレーションシップ、または図要素の1つに関連付けます。 規則は、このクラスのすべてのインスタンスに適用されます。抽象型である場合もあります。

2. ドメインモデルクラスのによって返されるセットに規則を追加して、規則を登録し `GetCustomDomainModelTypes()` ます。

3. いずれかの抽象規則クラスから規則クラスを派生させ、実行メソッドのコードを記述します。

   以降のセクションで、これらの手順について詳しく説明します。

### <a name="to-define-a-rule-on-a-domain-class"></a>ドメインクラスで規則を定義するには

- カスタムコードファイルで、クラスを定義し、属性でプレフィックスを付け <xref:Microsoft.VisualStudio.Modeling.RuleOnAttribute> ます。

    ```csharp
    [RuleOn(typeof(ExampleElement),
         // Usual value - but required, because it is not the default:
         FireTime = TimeToFire.TopLevelCommit)]
    class MyRule ...

    ```

- 最初のパラメーターのサブジェクトの種類には、ドメインクラス、ドメインリレーションシップ、図形、コネクタ、または図を使用できます。 通常は、ドメインクラスとリレーションシップに規則を適用します。

     `FireTime`通常、は `TopLevelCommit` です。 これにより、トランザクションのすべての主要な変更が行われた後にのみ、ルールが実行されるようになります。 代替手段はインラインであり、変更後すぐにルールが実行されます。および LocalCommit は、現在のトランザクションの最後 (最も外側ではない可能性があります) でルールを実行します。 ルールの優先度を設定して、キュー内での順序に影響を与えることもできますが、これは必要な結果を実現する信頼性の低い方法です。

- サブジェクトの種類として抽象クラスを指定できます。

- このルールは、subject クラスのすべてのインスタンスに適用されます。

- の既定値 `FireTime` は TimeToFire. TopLevelCommit です。 これにより、最も外側のトランザクションがコミットされるときにルールが実行されます。 別の方法として、TimeToFire があります。 これにより、トリガーイベントの直後にルールが実行されます。

### <a name="to-register-the-rule"></a>ルールを登録するには

- ドメインモデルでによって返される型の一覧に、規則クラスを追加し `GetCustomDomainModelTypes` ます。

    ```csharp
    public partial class ExampleDomainModel
     {
       protected override Type[] GetCustomDomainModelTypes()
       {
         List<Type> types = new List<Type>(base.GetCustomDomainModelTypes());
         types.Add(typeof(MyAddRule));
         // If you add more rules, list them here.
         return types.ToArray();
       }
     }

    ```

- ドメインモデルクラスの名前がわからない場合は、ファイルを検索してください。 (& **c** )。

- DSL プロジェクトのカスタムコードファイルにこのコードを記述します。

### <a name="to-write-the-code-of-the-rule"></a>ルールのコードを記述するには

- 次のいずれかの基底クラスから rule クラスを派生させます。

  | 基底クラス | トリガー |
  |-|-|
  | <xref:Microsoft.VisualStudio.Modeling.AddRule> | 要素、リンク、または図形が追加されます。<br /><br /> 新しい要素に加えて新しいリレーションシップを検出する場合に使用します。 |
  | <xref:Microsoft.VisualStudio.Modeling.ChangeRule> | ドメインプロパティの値が変更されます。 メソッドの引数は、古い値と新しい値を提供します。<br /><br /> 図形の場合、このルールは、図形が移動された場合に、組み込みプロパティが変更されたときにトリガーされ `AbsoluteBounds` ます。<br /><br /> 多くの場合、 `OnValueChanged` プロパティハンドラーでまたはをオーバーライドする方が便利です `OnValueChanging` 。 これらのメソッドは、変更の直前と直後に呼び出されます。 これに対し、ルールは通常、トランザクションの最後に実行されます。 詳細については、「 [ドメインプロパティ値の変更ハンドラー](../modeling/domain-property-value-change-handlers.md)」を参照してください。 **注:**  このルールは、リンクが作成または削除されたときにはトリガーされません。 代わりに、 `AddRule` ドメインリレーションシップに対してとを記述し `DeleteRule` ます。 |
  | <xref:Microsoft.VisualStudio.Modeling.DeletingRule> | 要素またはリンクが削除されようとしているときにトリガーされます。 ModelElement プロパティは、トランザクションが終了するまで true になります。 |
  | <xref:Microsoft.VisualStudio.Modeling.DeleteRule> | 要素またはリンクが削除されたときに実行されます。 このルールは、他のすべてのルールが実行された後 (Dele/Grを含む) に実行されます。 ModelElement が false で、ModelElement が true になっています。 後続の元に戻す操作を可能にするために、要素は実際にはメモリから削除されませんが、格納されている ElementDirectory からは削除されます。 |
  | <xref:Microsoft.VisualStudio.Modeling.MoveRule> | あるストアパーティションから別のストアパーティションに要素が移動されます。<br /><br /> (これは、図形のグラフィカルな位置には関係していないことに注意してください)。 |
  | <xref:Microsoft.VisualStudio.Modeling.RolePlayerChangeRule> | この規則はドメインリレーションシップにのみ適用されます。 モデル要素をリンクの末尾に明示的に割り当てると、トリガーされます。 |
  | <xref:Microsoft.VisualStudio.Modeling.RolePlayerPositionChangeRule> | リンクの MoveBefore または MoveToIndex メソッドを使用して、要素との間のリンクの順序が変更されたときにトリガーされます。 |
  | <xref:Microsoft.VisualStudio.Modeling.TransactionBeginningRule> | トランザクションが作成されるときに実行されます。 |
  | <xref:Microsoft.VisualStudio.Modeling.TransactionCommittingRule> | トランザクションがコミットされようとしているときに実行されます。 |
  | <xref:Microsoft.VisualStudio.Modeling.TransactionRollingBackRule> | トランザクションがロールバックされようとしているときに実行されます。 |

- 各クラスには、オーバーライドするメソッドがあります。 `override`クラスを入力して検出します。 このメソッドのパラメーターは、変更されている要素を識別します。

  ルールに関する次の点に注意してください。

1. トランザクション内の一連の変更によって、多くのルールがトリガーされることがあります。 通常、ルールは、最も外側のトランザクションがコミットされるときに実行されます。 これらは、指定されていない順序で実行されます。

2. ルールは、常にトランザクション内で実行されます。 したがって、変更を行うために新しいトランザクションを作成する必要はありません。

3. ルールは、トランザクションがロールバックされるとき、または元に戻す操作またはやり直し操作が実行されるときには実行されません。 これらの操作では、ストアのすべてのコンテンツが以前の状態にリセットされます。 そのため、ルールによってストアの外部にあるすべての状態が変更された場合、ストアのコンテンツと共に synchronism に保持されない可能性があります。 ストアの外部で状態を更新するには、イベントを使用することをお勧めします。 詳細については、「 [イベントハンドラーによって変更がモデル外に反映される](../modeling/event-handlers-propagate-changes-outside-the-model.md)」を参照してください。

4. 一部のルールは、モデルがファイルから読み込まれたときに実行されます。 読み込みまたは保存が進行中かどうかを判断するには、を使用し `store.TransactionManager.CurrentTransaction.IsSerializing` ます。

5. ルールのコードによってさらに多くのルールトリガーが作成された場合は、トリガーが起動リストの末尾に追加され、トランザクションが完了する前に実行されます。 DeletedRules は、他のすべてのルールの後に実行されます。 1つのルールを1回のトランザクションで何度も実行できます。

6. ルールとの間で情報をやり取りするには、に情報を格納し `TransactionContext` ます。 これは、トランザクション中に保持されるディクショナリにすぎません。 トランザクションの終了時に破棄されます。 各ルールのイベント引数を使用して、その引数にアクセスできます。 ルールは、予測可能な順序で実行されないことに注意してください。

7. 他の代替手段を検討した後、ルールを使用します。 たとえば、値が変更されたときにプロパティを更新する場合は、計算されたプロパティの使用を検討してください。 図形のサイズまたは位置を制限する場合は、を使用 `BoundsRule` します。 プロパティ値の変更に応答する場合は、 `OnValueChanged` プロパティにハンドラーを追加します。 詳細については、「 [変更に対する応答と反映](../modeling/responding-to-and-propagating-changes.md)」を参照してください。

## <a name="example"></a>例
 次の例では、2つの要素をリンクするためにドメインリレーションシップがインスタンス化されるときに、プロパティを更新します。 このルールは、ユーザーが図にリンクを作成したときだけでなく、プログラムコードがリンクを作成した場合にもトリガーされます。

 この例をテストするには、タスクフローソリューションテンプレートを使用して DSL を作成し、Dsl プロジェクト内のファイルに次のコードを挿入します。 ソリューションをビルドして実行し、デバッグプロジェクトでサンプルファイルを開きます。 コメント図形とフロー要素の間にコメントリンクを描画します。 コメント内のテキストは、最後に接続した要素に関するレポートに変更されます。

 実際には、各 AddRule の DeleteRule を作成します。

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Microsoft.VisualStudio.Modeling;

namespace Company.TaskRuleExample
{

  [RuleOn(typeof(CommentReferencesSubjects))]
  public class RoleRule : AddRule
  {

    public override void ElementAdded(ElementAddedEventArgs e)
    {
      base.ElementAdded(e);
      CommentReferencesSubjects link = e.ModelElement as CommentReferencesSubjects;
      Comment comment = link.Comment;
      FlowElement subject = link.Subject;
      Transaction current = link.Store.TransactionManager.CurrentTransaction;
      // Don't want to run when we're just loading from file:
      if (current.IsSerializing) return;
      comment.Text = "Flow has " + subject.FlowTo.Count + " outgoing connections";
    }

  }

  public partial class TaskRuleExampleDomainModel
  {
    protected override Type[] GetCustomDomainModelTypes()
    {
      List<Type> types = new List<Type>(base.GetCustomDomainModelTypes());
      types.Add(typeof(RoleRule));
      return types.ToArray();
    }
  }

}
```

## <a name="see-also"></a>関連項目

- [イベント ハンドラーによって変更内容がモデル外に反映される](../modeling/event-handlers-propagate-changes-outside-the-model.md)