---
title: '方法: ワークフローデザイナーのワークフローにコメントを追加する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Activities.Presentation.Annotations.Annotation.UI
- Annotation
ms.assetid: 9aa0e8d6-8129-4438-8389-d460611581a7
caps.latest.revision: 7
author: steved0x
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: d775c79cc7abdf6a66b1174ae625ca468f0764fc
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72663451"
---
# <a name="how-to-add-comments-to-a-workflow-in-the-workflow-designer"></a>ワークフロー デザイナーでワークフローにコメントを追加する方法
より大きく複雑なワーク フローを簡単に作成するため、[!INCLUDE[net_v45](../includes/net-v45-md.md)] では開発者がデザイナーで次の種類の項目に注釈を追加できます。

- <xref:System.Activities.Activity>

- <xref:System.Activities.Statements.State>

- <xref:System.Activities.Statements.Transition>

- クラス (派生) <xref:System.Activities.Statements.FlowNode>

- <xref:System.Activities.Variable>

- <xref:System.Activities.Argument>

> [!IMPORTANT]
> 注釈の内容はワーク フローに関連付けられた XAML ファイルにテキスト形式で保存され、他のユーザーに読み取られる可能性があります。 注釈に機密情報を入力する場合は注意してください。

### <a name="adding-an-annotation-to-an-activity-in-the-designer"></a>デザイナーのアクティビティへの注釈の追加

1. ワークフローデザイナーで、ワークフローデザイナーの項目を右クリックし、[ **注釈**]、[ **注釈の追加**] の順に選択します。

2. 注釈のテキストを提供された領域に追加します。

3. 項目に注釈アイコンが表示されます。 注釈アイコン上にカーソルを置くと、注釈のテキストが表示されます。

     ![Sequence アクティビティで注釈を表示している](../workflow-designer/media/annotation.png "Annotation")

### <a name="displaying-an-annotation-in-an-activitys-designer"></a>アクティビティのデザイナーへの注釈の表示

1. アクティビティの外側に注釈が表示されているアクティビティデザイナーで、注釈の装飾の **ピン** アイコンをクリックします。

2. 注釈がアクティビティ デザイナーに表示されます。 次のスクリーンショットでは、「ワーク フローのアクティビティを開始する」という注釈がアクティビティ デザイナーに表示されています。

     ![注釈がアクティビティ デザイナーに表示されている](../workflow-designer/media/annotationindesigner.png "AnnotationInDesigner")

3. アクティビティのデザイナーの外側に注釈を表示するには、アクティビティのデザイナーの注釈領域の上にマウスポインターを移動し、[ **ピン留めを外す** ] アイコンをクリックします。

     ![注釈がアクティビティ デザイナーの外部に表示されている](../workflow-designer/media/annotationoutsidedesigner.png "AnnotationOutsideDesigner")

### <a name="showing-or-hiding-all-annotations"></a>すべての注釈の表示または非表示

1. 注釈を持つアクティビティを右クリックします。 **注釈**を選択し、**すべての注釈を表示**します。

2. すべての注釈がアクティビティのデザイナーに表示されます。

3. アクティビティのデザイナーの外側にあるすべての注釈を表示するには、アクティビティを右クリックし、[ **注釈**] を選択して、 **すべての注釈を非表示**にします。

### <a name="editing-or-deleting-an-annotation-for-an-activity"></a>アクティビティの注釈の編集または削除

1. 注釈を持つアクティビティを右クリックします。

2. **注釈**の選択、注釈の**編集**、または**注釈の削除**を行います。

3. 編集または削除用に注釈が開きます。

4. すべての注釈を一度に削除するには、ワークフローデザイナーを右クリックし、[ **注釈**]、[ **すべての注釈を削除**] の順に選択します。

### <a name="adding-editing-and-deleting-an-annotation-for-a-variable-or-argument"></a>変数または引数の注釈の追加、編集、削除

1. 変数または引数を右クリックし、[注釈の追加] をクリックします。

2. 注釈のテキストを入力します。 変数または引数に注釈アイコンが表示されます。

3. 注釈を持つ変数または引数を右クリックします。 [注釈の編集] をクリックします。

4. 編集用に注釈が開きます。

5. 注釈を持つ変数または引数を右クリックします。 [注釈の削除] をクリックします。

6. 注釈が削除されます。