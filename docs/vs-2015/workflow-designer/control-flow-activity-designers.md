---
title: 制御フローアクティビティデザイナー |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
ms.assetid: ba74af23-5398-4e62-bd90-c50612e3bfef
caps.latest.revision: 7
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 40f17913864f80e04c3e8b8e703f057094c9bdea
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72656922"
---
# <a name="control-flow-activity-designers"></a>制御フロー アクティビティ デザイナー
[!INCLUDE[wfd1](../includes/wfd1-md.md)] には、ワークフローを構築するときに使用できるシステム指定のアクティビティが多数含まれています。 このセクションでは、ワークフロー内のフローの制御を目的とした、システムによって提供されるアクティビティを紹介します。 次のトピックでは、これらのアクティビティについて説明し、その使用方法についてのガイドラインを示します。

## <a name="in-this-section"></a>このセクションの内容
 [Dowhile](../workflow-designer/dowhile-activity-designer.md) 指定された条件が **true**と評価されるまで、本文に含まれるアクティビティを少なくとも1回実行します。

 [ForEach \<T> ](foreach-t-activity-designer.md)指定したコレクション内の各項目について、本文に含まれるアクティビティを実行します。

 [If](../workflow-designer/if-activity-designer.md) 条件を評価し、その評価の結果に応じてアクティビティを実行します。

 [並列](../workflow-designer/parallel-activity-designer.md) 子アクティビティのコレクションを同時に実行します。

 [Parallelforeach \<T> ](../workflow-designer/parallelforeach-t-activity-designer.md)コレクションの要素を列挙し、コレクションの各要素に対して埋め込みステートメントを並列実行します。

 [選択](../workflow-designer/pick-activity-designer.md) イベントベースのフロー制御を提供する何らかのイベントに応答して、複数の分岐のいずれか1つを実行します。

 [分岐](../workflow-designer/pickbranch-activity-designer.md) の候補アクティビティ内の実行パスを提供 <xref:System.Activities.Statements.Pick> します。

 [シーケンス](../workflow-designer/sequence-activity-designer.md) 順序どおりに実行される子アクティビティの順序付けられたコレクションを格納します。

 [スイッチ \<T> ](switch-t-activity-designer.md)指定された式を評価し、関連付けられたキーが評価から取得した値と一致するアクティビティのコレクションからアクティビティを実行します。

 [しばらく](../workflow-designer/while-activity-designer.md) 指定した条件が **true**と評価されている間に、本文に含まれるアクティビティを実行します。

## <a name="reference"></a>関連項目
 <xref:System.Activities.Activity>

 <xref:System.Activities.Statements.DoWhile>

 <xref:System.Activities.Statements.ForEach%601>

 <xref:System.Activities.Statements.If>

 <xref:System.Activities.Statements.Parallel>

 <xref:System.Activities.Statements.ParallelForEach%601>

 <xref:System.Activities.Statements.Pick>

 <xref:System.Activities.Statements.PickBranch>

 <xref:System.Activities.Statements.Sequence>

 <xref:System.Activities.Statements.Switch%601>

 <xref:System.Activities.Statements.While>

## <a name="related-sections"></a>関連項目
 他の種類のアクティビティ デザイナーについては、次のトピックを参照してください。

 [アクティビティ デザイナーの使用](../workflow-designer/using-the-activity-designers.md)

 [フローチャート](../workflow-designer/flowchart-activity-designers.md)

 [メッセージング](../workflow-designer/messaging-activity-designers.md)

 [Runtime](../workflow-designer/runtime-activity-designers.md)

 [プリミティブ](../workflow-designer/primitives-activity-designers.md)

 [トランザクション](../workflow-designer/transaction-activity-designers.md)

 [コレクション](../workflow-designer/collection-activity-designers.md)

 [エラー処理](../workflow-designer/error-handling-activity-designers.md)

## <a name="external-resources"></a>外部リソース
 [アクティビティ デザイナーの使用](../workflow-designer/using-the-activity-designers.md)