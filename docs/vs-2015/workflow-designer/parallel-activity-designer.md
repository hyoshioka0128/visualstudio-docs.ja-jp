---
title: Parallel アクティビティデザイナー |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Parallel.UI
ms.assetid: 0306dc3b-075a-4091-ac3a-96486fbabed5
caps.latest.revision: 10
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: a46a340ccdeacacb8f04b962313db18975447a67
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72672634"
---
# <a name="parallel-activity-designer"></a>Parallel アクティビティ デザイナー
<xref:System.Activities.Statements.Parallel> アクティビティは、一連の子アクティビティを同時に実行するアクティビティです。

## <a name="the-parallel-activity"></a>Parallel アクティビティ
 <xref:System.Activities.Statements.Parallel> アクティビティは、子アクティビティを <xref:System.Activities.Statements.Parallel.Branches%2A> コレクションに格納します。 一部の子アクティビティがアイドル状態になる可能性がある場合は、<xref:System.Activities.Statements.Parallel> アクティビティの代わりに <xref:System.Activities.Statements.Sequence> アクティビティを使用してください。

 <xref:System.Activities.Statements.Parallel> アクティビティには、ユーザーによって指定された <xref:System.Activities.Statements.Parallel.CompletionCondition%2A> 式を保持する [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] プロパティがあります。 このプロパティは、各分岐の完了後に、<xref:System.Activities.Statements.Parallel> アクティビティによって評価されます。 **True**と評価された場合、 <xref:System.Activities.Statements.Parallel> アクティビティは他の分岐を実行せずに完了します。 が <xref:System.Activities.Statements.Parallel.CompletionCondition%2A> **True**と評価されない場合、 <xref:System.Activities.Statements.Parallel> そのすべての子アクティビティが完了すると、アクティビティが完了します。

### <a name="using-the-parallel-activity-designer"></a>Parallel アクティビティ デザイナーの使用
 **Parallel**アクティビティデザイナーは、[**ツールボックス**] の [**制御フロー** ] カテゴリにあります。このカテゴリにアクセスするには、の左側にある [**ツールボックス**] タブをクリックします [!INCLUDE[wfd2](../includes/wfd2-md.md)] (または、[**表示**] メニューの [**ツールバー** ] を選択するか、CTRL + ALT + X キーを押します)。

 **Parallel**アクティビティデザイナーは、[**ツールボックス**] からドラッグして、 [!INCLUDE[wfd2](../includes/wfd2-md.md)] アクティビティデザイナーを通常配置している画面の任意の場所 ( **Sequence**アクティビティデザイナー内など) にドロップできます。 にドロップすると [!INCLUDE[wfd2](../includes/wfd2-md.md)] 、アクティビティが作成さ <xref:System.Activities.Statements.Parallel> れます。このアクティビティには、既定で <xref:System.Activities.Activity.DisplayName%2A> **並列**のが含まれます。

 アクティビティを parallel アクティビティのコレクションに追加するには <xref:System.Activities.Statements.Parallel.Branches%2A> 、他のアクティビティデザイナーを [ **ツールボックス** ] からドラッグし、 **parallel** アクティビティデザイナー内の三角形にドロップします。 分岐に含まれるアクティビティのそばに三角形が配置されます。 この手順を繰り返すことによって、さらにアクティビティを追加できます。 アクティビティは、 **並列** アクティビティデザイナー内でドラッグアンドドロップすることで並べ替えることができます。

### <a name="parallel-activity-properties-in-the-workflow-designer"></a>ワークフロー デザイナーでの Parallel アクティビティのプロパティ
 次の表に、Parallel アクティビティのプロパティと、デザイナーでのその使用方法を示します。

|プロパティ名|必須|使用|
|-------------------|--------------|-----------|
|<xref:System.Activities.Activity.DisplayName%2A>|×|ヘッダーのアクティビティ デザイナーの表示名を指定します。 既定値は **Parallel**です。 この値は、必要に応じて、[ **プロパティ** ] グリッドで編集することも、アクティビティデザイナーのヘッダーで直接編集することもできます。|
|<xref:System.Activities.Statements.Parallel.Branches%2A>|○|実行される子アクティビティのコレクションが格納されます。|
|<xref:System.Activities.Statements.Parallel.CompletionCondition%2A>|×|分岐の完了後に評価されます。 **True**と評価された場合、スケジュールされた保留中の分岐は取り消されます。 このプロパティが設定されていない場合、または **False**に評価された場合、そのすべての子アクティビティが完了すると、アクティビティが完了します。 既定値は **null** です。|

## <a name="see-also"></a>参照
 [シーケンス](../workflow-designer/sequence-activity-designer.md) [parallelforeach \<T> ](../workflow-designer/parallelforeach-t-activity-designer.md) [制御フロー](../workflow-designer/control-flow-activity-designers.md)