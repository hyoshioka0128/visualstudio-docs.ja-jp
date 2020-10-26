---
title: 'ワークフローデザイナー-方法: ワークフローにコメントを追加する'
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- System.Activities.Presentation.Annotations.Annotation.UI
- Annotation
ms.assetid: 9aa0e8d6-8129-4438-8389-d460611581a7
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
author: TerryGLee
ms.openlocfilehash: 77fb43671a45d5d53d2fe23fa3e4e7a9a98c4373
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85815501"
---
# <a name="how-to-add-comments-to-a-workflow-in-the-workflow-designer"></a>ワークフロー デザイナーでワークフローにコメントを追加する方法

より大規模で複雑なワークフローの作成を容易にするために、.NET Framework 4.5 では、開発者はデザイナーで次の種類のアイテムに注釈を追加できます。

- <xref:System.Activities.Activity>

- <xref:System.Activities.Statements.State>

- <xref:System.Activities.Statements.Transition>

- クラス (派生) <xref:System.Activities.Statements.FlowNode>

- <xref:System.Activities.Variable>

- <xref:System.Activities.Argument>

> [!IMPORTANT]
> 注釈の内容はワーク フローに関連付けられた XAML ファイルにテキスト形式で保存され、他のユーザーに読み取られる可能性があります。 注釈に機密情報を入力する場合は注意してください。

## <a name="adding-an-annotation-to-an-activity-in-the-designer"></a>デザイナーのアクティビティへの注釈の追加

1. ワークフローデザイナーで、ワークフローデザイナーの項目を右クリックし、[ **注釈**]、[ **注釈の追加**] の順に選択します。

1. 注釈のテキストを提供された領域に追加します。

   項目には注釈アイコンが表示されます。 注釈アイコンの上にカーソルを合わせると、注釈のテキストが表示されます。

## <a name="displaying-an-annotation-in-an-activitys-designer"></a>アクティビティのデザイナーへの注釈の表示

1. アクティビティの外側に注釈が表示されているアクティビティデザイナーで、注釈の装飾の **ピン** アイコンをクリックします。

   注釈がアクティビティデザイナーに表示されます。 次のスクリーンショットでは、「ワーク フローのアクティビティを開始する」という注釈がアクティビティ デザイナーに表示されています。

   ![注釈がアクティビティ デザイナーに表示されている](../workflow-designer/media/annotationindesigner.png)

2. アクティビティのデザイナーの外側に注釈を表示するには、アクティビティのデザイナーの注釈領域の上にマウスポインターを移動し、[ **ピン留めを外す** ] アイコンをクリックします。

   ![アクティビティのデザイナーの外側に表示される注釈](../workflow-designer/media/annotationoutsidedesigner.png)

## <a name="showing-or-hiding-all-annotations"></a>すべての注釈の表示または非表示

1. 注釈を持つアクティビティを右クリックします。 **注釈**を選択し、**すべての注釈を表示**します。

   すべての注釈は、アクティビティのデザイナーに表示されます。

1. アクティビティのデザイナーの外側にあるすべての注釈を表示するには、アクティビティを右クリックし、[ **注釈**] を選択して、 **すべての注釈を非表示**にします。

## <a name="editing-or-deleting-an-annotation-for-an-activity"></a>アクティビティの注釈の編集または削除

1. 注釈を持つアクティビティを右クリックします。

1. **注釈**の選択、注釈の**編集**、または**注釈の削除**を行います。

   編集または削除するために注釈が開かれています。

1. すべての注釈を一度に削除するには、ワークフローデザイナーを右クリックし、[ **注釈**]、[ **すべての注釈を削除**] の順に選択します。

## <a name="adding-editing-and-deleting-an-annotation-for-a-variable-or-argument"></a>変数または引数の注釈の追加、編集、削除

1. 変数または引数を右クリックし、[注釈の追加] をクリックします。

1. 注釈のテキストを入力します。 変数または引数には、注釈アイコンが表示されます。

1. 注釈を持つ変数または引数を右クリックします。 [注釈の編集] をクリックします。

   編集するために注釈が開かれています。

1. 注釈を持つ変数または引数を右クリックします。 [注釈の削除] をクリックします。

   注釈が削除されます。
