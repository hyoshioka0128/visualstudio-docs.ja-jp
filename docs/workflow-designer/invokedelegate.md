---
title: ワークフローデザイナー-InvokeDelegate
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- InvokeDelegate Designer
- System.Activities.Statements.InvokeDelegate.UI
ms.assetid: 289a7498-5127-453f-beb5-05f05b80d26f
author: TerryGLee
ms.author: tglee
ms.workload:
- multiple
ms.openlocfilehash: 9e63fb7a766b79467749cc5181a575e0d35a07b8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "86876074"
---
# <a name="invokedelegate"></a>InvokeDelegate

**Invokedelegate**デザイナーは、アクティビティを作成および構成するために使用され <xref:System.Activities.Statements.InvokeDelegate> ます。

## <a name="the-invokedelegate-activity"></a>InvokeDelegate アクティビティ

<xref:System.Activities.Statements.InvokeDelegate> はパブリック デリゲートを呼び出します。

### <a name="use-the-invokedelegate-activity-designer"></a>InvokeDelegate アクティビティデザイナーの使用

**ツールボックス**の [**プリミティブ**] カテゴリで、 **invokedelegate**アクティビティデザイナーにアクセスします。 **Invokedelegate**アクティビティデザイナーは、[**ツールボックス**] からドラッグして、アクティビティが通常配置されているワークフローデザイナー画面 (内など) にドロップできます <xref:System.Activities.Statements.Sequence> 。 アクティビティデザイナーを削除 <xref:System.Activities.Statements.InvokeDelegate> すると、既定の InvokeDelegate を持つアクティビティが作成さ <xref:System.Activities.Activity.DisplayName%2A> れます。 は、 <xref:System.Activities.Activity.DisplayName%2A> **invokedelegate** アクティビティデザイナーのヘッダー、またはプロパティグリッドの [ **DisplayName** ] ボックスで編集できます。

### <a name="the-invokedelegate-properties"></a>InvokeDelegate プロパティ

次の表に、<xref:System.Activities.Statements.InvokeDelegate> のプロパティと、デザイナーでのその使用方法を示します。 これらのプロパティは、プロパティグリッドで編集できます。また、ワークフローデザイナーサーフェイスで編集することもできます。

|プロパティ名|必須|使用法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|×|<xref:System.Activities.Statements.InvokeDelegate> アクティビティの表示名。 既定値は InvokeDelegate です。<br /><br /> は <xref:System.Activities.Activity.DisplayName%2A> 厳密には必須ではありませんが、1つを使用することをお勧めします。|
|<xref:System.Activities.Statements.InvokeDelegate.Delegate%2A>|○|アクティビティの実行時に呼び出す <xref:System.Activities.ActivityDelegate> の名前。 このプロパティは、デザイナー画面で編集でき、必須です。|
|<xref:System.Activities.Statements.InvokeDelegate.DelegateArguments%2A>|×|呼び出されたデリゲートの引数コレクション。 キーは、のパラメーターオブジェクトの名前です <xref:System.Activities.ActivityDelegate> 。値は、式が評価され、対応するパラメーターオブジェクトに割り当てられる引数です。 このプロパティを設定できる [ **DelegateArguments** ] ダイアログボックスを表示するには、プロパティグリッドの **DelegateArguments** フィールドで、省略記号ボタンをクリックします。 引数を追加するには、[ **引数の作成** ] フィールドをクリックします。|

## <a name="see-also"></a>関連項目

- [ワークフロー デザイナーでアクティビティ デリゲートを定義および使用する方法](../workflow-designer/how-to-define-and-consume-activity-delegates-in-the-workflow-designer.md)