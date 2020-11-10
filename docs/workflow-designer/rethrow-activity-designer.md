---
title: ワークフローデザイナー-再スローアクティビティデザイナー
description: 再スローアクティビティについて、および再スローアクティビティデザイナーを使用して再スローアクティビティを作成および構成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Rethrow.UI
ms.assetid: 9cfa2eda-395f-4cf3-9154-83fadd4f7452
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9195fc95ac905213b048aa16882ea6584adacd33
ms.sourcegitcommit: ed26b6e313b766c4d92764c303954e2385c6693e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/10/2020
ms.locfileid: "94434117"
---
# <a name="rethrow-activity-designer"></a>Rethrow アクティビティ デザイナー

再 **スロー** アクティビティデザイナーは、アクティビティを作成および構成するために使用され <xref:System.Activities.Statements.Rethrow> ます。

## <a name="the-rethrow-activity"></a>再スローアクティビティ

<xref:System.Activities.Statements.Rethrow> アクティビティでは、以前にスローされた例外をスローします。 このアクティビティは、<xref:System.Activities.Statements.Catch> アクティビティの <xref:System.Activities.Statements.TryCatch> ハンドラーでのみ使用できます。

### <a name="use-the-rethrow-activity-designer"></a>再スローアクティビティデザイナーの使用

**ツールボックス** の **エラー処理** カテゴリの再 **スロー** アクティビティデザイナーにアクセスします。 再 **スロー** アクティビティデザイナーは、[ **ツールボックス** ] からドラッグして、アクティビティを通常配置している任意の場所 (内など) にワークフローデザイナー画面にドロップできます <xref:System.Activities.Statements.Sequence> 。 アクティビティデザイナーを削除すると、Throw という <xref:System.Activities.Statements.Rethrow> 既定の **DisplayName** を持つアクティビティが作成されます。 値は、再 <xref:System.Activities.Activity.DisplayName%2A> **スロー** アクティビティデザイナーのヘッダー、またはプロパティグリッドの [ **DisplayName** ] ボックスで編集できます。

### <a name="the-rethrow-properties"></a>再スロープロパティ

次の表に、 <xref:System.Activities.Statements.Rethrow> プロパティを示し、デザイナーでのそれらの使用方法について説明します。

|プロパティ名|必須|使用法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|×|<xref:System.Activities.Statements.Rethrow> アクティビティの表示名を指定します (省略可能)。 既定値は Rethrow です。|

## <a name="see-also"></a>関連項目

- [コレクション](../workflow-designer/collection-activity-designers.md)
- [Throw](../workflow-designer/throw-activity-designer.md)
- [TryCatch](../workflow-designer/trycatch-activity-designer.md)
