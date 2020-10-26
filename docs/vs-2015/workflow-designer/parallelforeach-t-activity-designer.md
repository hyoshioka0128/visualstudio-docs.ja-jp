---
title: ParallelForEach &lt; T &gt; アクティビティデザイナー |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Activities.Statements.ParallelForEach`1.UI
ms.assetid: e93a4843-aef2-4d3e-9a0a-a2d3d1411aa7
caps.latest.revision: 9
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 4c659e941a8503a0d5ff601fea23fcec69b2bbcf
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72672612"
---
# <a name="parallelforeachlttgt-activity-designer"></a>ParallelForEach &lt; T &gt; アクティビティデザイナー
<xref:System.Activities.Statements.ParallelForEach%601> アクティビティでは、コレクションの要素を列挙し、コレクションの各要素に対して埋め込みステートメントを並列的に (同じスレッドで非同期的に) 実行します。 このフロー制御アクティビティは、その子アクティビティがアイドル状態になると予想される場合に、<xref:System.Activities.Statements.Sequence> アクティビティの代わりに使用します。

 <xref:System.Activities.Statements.ParallelForEach%601> アクティビティには、ユーザーによって指定された <xref:System.Activities.Statements.ParallelForEach%601.CompletionCondition%2A> 式を保持する [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] プロパティがあります。 このプロパティは、各分岐の完了後に、<xref:System.Activities.Statements.ParallelForEach%601> アクティビティによって評価されます。 **True**と評価された場合、 <xref:System.Activities.Statements.ParallelForEach%601> アクティビティは他の分岐を実行せずに完了します。 が <xref:System.Activities.Statements.ParallelForEach%601.CompletionCondition%2A> **true**と評価されない場合、 <xref:System.Activities.Statements.ParallelForEach%601> そのすべての子アクティビティが完了すると、アクティビティが完了します。

## <a name="the-parallelforeacht-activity"></a>ParallelForEach \<T> アクティビティ
 <xref:System.Activities.Statements.ParallelForEach%601> 値を列挙し、列挙される <xref:System.Activities.Statements.ParallelForEach%601.Body%2A> すべての値のをスケジュールします。 スケジュールされるのは <xref:System.Activities.Statements.ParallelForEach%601.Body%2A> のみです。 本文の実行方法は、<xref:System.Activities.Statements.ParallelForEach%601.Body%2A> がアイドル状態になるかどうかによって異なります。

 <xref:System.Activities.Statements.ParallelForEach%601.Body%2A> がアイドル状態にならない場合は、スケジュールされたアクティビティがスタックとして扱われるため、逆の順序で実行されます。つまり、最後にスケジュールされたアクティビティが最初に実行されます。 たとえば、内ののコレクションがあり、 {1,2,3,4} <xref:System.Activities.Statements.ParallelForEach%601> **WriteLine** を本文として使用して値を書き込む場合などです。コンソールには、4、3、2、1が出力されています。 これは、 **writeline** がアイドル状態にならず、4つの **writeline** アクティビティがスケジュールされた後で、スタック動作 (最初は最後の出力) を使用して実行されたためです。

 ただし、<xref:System.Activities.Statements.ParallelForEach%601.Body%2A> アクティビティや <xref:System.ServiceModel.Activities.Receive> アクティビティのように、アイドル状態になる可能性のあるアクティビティが <xref:System.Activities.Statements.Delay> に含まれている場合は、 それぞれのアクティビティが完了するまで待機する必要はありません。 <xref:System.Activities.Statements.ParallelForEach%601> は、スケジュールされている次の本文アクティビティに進み、実行を試みます。 そのアクティビティもアイドル状態になる場合は、<xref:System.Activities.Statements.ParallelForEach%601> が、さらに次の本文アクティビティに進みます。

### <a name="using-the-parallelforeacht-activity-designer"></a>ParallelForEach \<T> アクティビティデザイナーの使用
 **Parallelforeach \<T> **アクティビティデザイナーは、[**ツールボックス**] の [**制御フロー** ] カテゴリにあります。このカテゴリにアクセスするには、の左側にある [**ツールボックス**] タブをクリックします [!INCLUDE[wfd2](../includes/wfd2-md.md)] (または、[**表示**] メニューの [**ツールバー** ] を選択するか、CTRL + ALT + X キーを押します)。

 **Parallelforeach \<T> **アクティビティデザイナーは、[**ツールボックス**] からドラッグして、 [!INCLUDE[wfd2](../includes/wfd2-md.md)] アクティビティデザイナーを通常配置している画面の任意の場所 ( **Sequence**アクティビティデザイナー内など) にドロップできます。 にドロップすると [!INCLUDE[wfd2](../includes/wfd2-md.md)] 、アクティビティが作成され <xref:System.Activities.Statements.ParallelForEach%601> ます。このアクティビティには、既定で <xref:System.Activities.Activity.DisplayName%2A> parallelforeach のが含まれ ** \<Int32> ます。**

### <a name="parallelforeacht-properties-in-the-workflow-designer"></a>\<T>ワークフローデザイナーの ParallelForEach プロパティ
 次の表に、最も役に立つ <xref:System.Activities.Statements.ParallelForEach%601> アクティビティのプロパティと、デザイナーでのその使用方法を示します。

|プロパティ名|必須|使用|
|-------------------|--------------|-----------|
|<xref:System.Activities.Activity.DisplayName%2A>|×|ヘッダーのアクティビティ デザイナーの表示名を指定します。 既定値は**Parallelforeach \<Int32> **です。 この値は、必要に応じて、[ **プロパティ** ] グリッドで編集することも、アクティビティデザイナーのヘッダーで直接編集することもできます。|
|<xref:System.Activities.Statements.ParallelForEach%601.Body%2A>|×|コレクション内の各項目に対して実行するアクティビティ。 アクティビティを追加するには <xref:System.Activities.Statements.ParallelForEach%601.Body%2A> 、"ここにアクティビティをドロップします" というヒントテキストが表示された**parallelforeach \<T> **アクティビティデザイナーの [**本文**] ボックスに、[ツールボックス] からアクティビティをドロップします。|
|**TypeArgument**|○|<xref:System.Activities.Statements.ParallelForEach%601.Values%2A>ジェネリックパラメーター *T*によって指定されたコレクション内の項目の型。既定では、 **Typeargument**は**Int32**に設定されています。 **Parallelforeach \<T> **アクティビティデザイナーで T 型を変更するには、プロパティグリッドの**typeargument**コンボボックスの値を変更します。|
|<xref:System.Activities.Statements.ParallelForEach%601.Values%2A>|○|反復処理を行う項目のコレクション。 を設定するには <xref:System.Activities.Statements.ParallelForEach%601.Values%2A> 、 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] **ForEach \<T> **アクティビティデザイナーの [**値**] ボックスに、"VB の式を入力してください" または [**プロパティ**] ウィンドウの [**値**] ボックスに式を入力します。|
|<xref:System.Activities.Statements.ParallelForEach%601.CompletionCondition%2A>||各イテレーションの完了後に評価されます。 true であると評価する場合、スケジュールされた保留イテレーションはキャンセルされます。 このプロパティが設定されていない場合、スケジュールされたすべてのステートメントは、完了するまで実行されます。|

 既定では、ループ反復子には、item という名前が付けられます。 反復子変数の名前は、 **parallelforeach \<T> **アクティビティデザイナーの [ **ForEach** ] ボックスで変更できます。 ループ反復子は、<xref:System.Activities.Statements.ParallelForEach%601> アクティビティの子の式で使用できます。

## <a name="see-also"></a>参照
 [シーケンス](../workflow-designer/sequence-activity-designer.md)の[並列](../workflow-designer/parallel-activity-designer.md)[制御フロー](../workflow-designer/control-flow-activity-designers.md)