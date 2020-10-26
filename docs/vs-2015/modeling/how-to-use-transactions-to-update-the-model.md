---
title: '方法: トランザクションを使用してモデルを更新する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
ms.assetid: e24436a5-7f97-401b-bc83-20d188d10d5b
caps.latest.revision: 9
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: cd66c62d74bfe63d8376b5520b42cb20c8c0a3a7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72651605"
---
# <a name="how-to-use-transactions-to-update-the-model"></a>方法: トランザクションを使用してモデルを更新する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

トランザクションでは、ストアに加えられた変更がグループとして扱われるようにします。 グループ化された変更は、1つの単位としてコミットまたはロールバックできます。

 プログラムコードによって、視覚化およびモデリング SDK のストアの要素が変更、追加、または削除されるたびに [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 、トランザクション内でこの操作を行う必要があります。 <xref:Microsoft.VisualStudio.Modeling.Transaction>変更が発生したときに、ストアに関連付けられているのアクティブなインスタンスが存在している必要があります。 これは、すべてのモデル要素、リレーションシップ、図形、図、およびそれらのプロパティに適用されます。

 トランザクションメカニズムは、一貫性のない状態を回避するのに役立ちます。 トランザクションの実行中にエラーが発生した場合は、すべての変更がロールバックされます。 ユーザーが元に戻すコマンドを実行した場合、最近の各トランザクションは1つのステップとして扱われます。 ユーザーは、明示的に別のトランザクションに配置していない限り、最近の変更の一部を元に戻すことはできません。

## <a name="opening-a-transaction"></a>トランザクションを開く
 トランザクションを管理する最も便利な方法は、ステートメントでステートメントを使用することです `using` `try...catch` 。

```
Store store; ...
try
{
  using (Transaction transaction =
    store.TransactionManager.BeginTransaction("update model"))
    // Outermost transaction must always have a name.
  {
    // Make several changes in Store:
    Person p = new Person(store);
    p.FamilyTreeModel = familyTree;
    p.Name = "Edward VI";
    // end of changes to Store

    transaction.Commit(); // Don't forget this!
  } // transaction disposed here
}
catch (Exception ex)
{
  // If an exception occurs, the Store will be
  // rolled back to its previous state.
}
```

 変更中に最終処理を妨げる例外が発生した場合 `Commit()` 、ストアは以前の状態にリセットされます。 これにより、エラーによってモデルが不整合な状態にならないようにすることができます。

 1つのトランザクション内で任意の数の変更を行うことができます。 アクティブなトランザクション内で新しいトランザクションを開くことができます。 入れ子になったトランザクションは、親トランザクションが終了する前にコミットまたはロールバックする必要があります。 詳細については、プロパティの例を参照してください <xref:Microsoft.VisualStudio.Modeling.Transaction.TransactionDepth%2A> 。

 変更を永続的なものにするには、 `Commit` トランザクションが破棄される前にトランザクションを実行する必要があります。 トランザクション内でキャッチされない例外が発生した場合、ストアは変更前の状態にリセットされます。

## <a name="rolling-back-a-transaction"></a>トランザクションのロールバック
 ストアをトランザクションの前の状態に保つには、次のいずれかの方法を使用できます。

1. トランザクションのスコープ内でキャッチされない例外を発生させます。

2. トランザクションを明示的にロールバックします。

    ```
    this.Store.TransactionManager.CurrentTransaction.Rollback();
    ```

## <a name="transactions-do-not-affect-non-store-objects"></a>トランザクションは、ストア以外のオブジェクトには影響しません。
 トランザクションでは、ストアの状態のみが制御されます。 ファイル、データベース、または DSL 定義の外部で通常の型で宣言したオブジェクトなど、外部アイテムに対して行われた部分的な変更を元に戻すことはできません。

 例外によってそのような変更がストアと矛盾する可能性がある場合は、例外ハンドラーでその可能性を処理する必要があります。 外部リソースがストアオブジェクトと確実に同期されるようにする方法の1つは、イベントハンドラーを使用して、各外部オブジェクトをストア内の要素に結合することです。 詳細については、「 [イベントハンドラーによって変更がモデル外に反映される](../modeling/event-handlers-propagate-changes-outside-the-model.md)」を参照してください。

## <a name="rules-fire-at-the-end-of-a-transaction"></a>ルールはトランザクションの終了時に起動されます
 トランザクションの最後に、トランザクションが破棄される前に、ストア内の要素に関連付けられているルールが起動されます。 各ルールは、変更されたモデル要素に適用されるメソッドです。 たとえば、モデル要素が変更されたときに図形の状態を更新し、モデル要素の作成時に図形を作成する "修正" ルールがあります。 指定された起動順序がありません。 ルールによって行われた変更によって、別のルールが起動される場合があります。

 独自の規則を定義できます。 ルールの詳細については、「 [変更に対する応答と反映](../modeling/responding-to-and-propagating-changes.md)」を参照してください。

 元に戻す、やり直し、またはロールバックコマンドを実行しても、ルールは起動されません。

## <a name="transaction-context"></a>トランザクション コンテキスト
 各トランザクションには、必要なすべての情報を格納できるディクショナリがあります。

 `store.TransactionManager`

 `.CurrentTransaction.TopLevelTransaction`

 `.Context.Add(aKey, aValue);`

 これは、ルール間で情報を転送する場合に特に便利です。

## <a name="transaction-state"></a>トランザクションの状態
 場合によっては、トランザクションの取り消しまたは再処理によって変更が発生した場合に、変更が反映されないようにする必要があります。 これは、たとえば、ストア内の別の値を更新できるプロパティ値ハンドラーを記述した場合に発生する可能性があります。 元に戻す操作では、ストア内のすべての値が以前の状態にリセットされるので、更新された値を計算する必要はありません。 次のコードを使用します。

```
if (!this.Store.InUndoRedoOrRollback) {...}
```

 ルールは、ストアが最初にファイルから読み込まれたときに発生する可能性があります。 これらの変更に対する応答を回避するには、次のように使用します。

```
if (!this.Store.InSerializationTransaction) {...}

```
