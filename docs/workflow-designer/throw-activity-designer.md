---
title: ワークフローデザイナー-Throw アクティビティデザイナー
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Throw.UI
ms.assetid: 5e97c947-be39-4a1f-af04-000e2e09528a
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 650082ab0e4f8576b7028b8011c88bf5d93b2afd
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "75593097"
---
# <a name="throw-activity-designer"></a>Throw アクティビティ デザイナー

**Throw**アクティビティデザイナーは、アクティビティを作成および構成するために使用され <xref:System.Activities.Statements.Throw> ます。

## <a name="the-throw-activity"></a>Throw アクティビティ

<xref:System.Activities.Statements.Throw> アクティビティによって例外がスローされます。

### <a name="using-the-throw-activity-designer"></a>Throw アクティビティ デザイナーの使用

[**ツールボックス**] の [**エラー処理**] カテゴリで、 **Throw**アクティビティデザイナーにアクセスします。

**Throw**アクティビティデザイナーは、[**ツールボックス**] からドラッグして、アクティビティを通常配置している任意の場所 (内など) にワークフローデザイナー画面にドロップできます <xref:System.Activities.Statements.Sequence> 。 これ <xref:System.Activities.Statements.Throw> により、Throw という既定の **DisplayName** を持つアクティビティが作成されます。 この <xref:System.Activities.Activity.DisplayName%2A> 値は、 **Throw** アクティビティデザイナーのヘッダー、またはプロパティグリッドの [ **DisplayName** ] ボックスで編集できます。 この <xref:System.Activities.Statements.Throw.Exception%2A> プロパティは、プロパティ グリッドで編集する必要があります。

### <a name="the-throw-properties"></a>Throw プロパティ

次の表に、<xref:System.Activities.Statements.Throw> のプロパティと、デザイナーでのその使用方法を示します。

|プロパティ名|必須|使用|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|×|<xref:System.Activities.Statements.Throw> アクティビティの表示名を指定します (省略可能)。 既定値は Throw です。|
|<xref:System.Activities.Statements.Throw.Exception%2A>|○|スローされる例外。 この例外は、<xref:System.Exception> から派生していることが必要です。 例外を指定するには、プロパティ グリッドで Visual Basic の式を入力します。|

## <a name="see-also"></a>こちらもご覧ください

- [コレクション](../workflow-designer/collection-activity-designers.md)
- [Rethrow](../workflow-designer/rethrow-activity-designer.md)
- [Throw アクティビティ デザイナー](../workflow-designer/throw-activity-designer.md)
- [TryCatch](../workflow-designer/trycatch-activity-designer.md)
