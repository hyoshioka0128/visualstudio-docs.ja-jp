---
title: アクティビティデザイナーの再スロー |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Rethrow.UI
ms.assetid: 9cfa2eda-395f-4cf3-9154-83fadd4f7452
caps.latest.revision: 5
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: c65469242a60c64d6f31bfaea4fdbbf2d5251a34
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72663369"
---
# <a name="rethrow-activity-designer"></a>Rethrow アクティビティ デザイナー
再 **スロー** アクティビティデザイナーは、アクティビティを作成および構成するために使用され <xref:System.Activities.Statements.Rethrow> ます。

## <a name="the-rethrow-activity"></a>Rethrow アクティビティ
 <xref:System.Activities.Statements.Rethrow> アクティビティでは、以前にスローされた例外をスローします。 このアクティビティは、<xref:System.Activities.Statements.Catch> アクティビティの <xref:System.Activities.Statements.TryCatch> ハンドラーでのみ使用できます。

### <a name="using-the-rethrow-activity-designer"></a>ReThrow アクティビティ デザイナーの使用
 再**スロー**アクティビティデザイナーは、[**ツールボックス**] の [**エラー処理**] カテゴリにあります。このカテゴリにアクセスするには、の左側にある [**ツールボックス**] タブをクリックします [!INCLUDE[wfd2](../includes/wfd2-md.md)] (または、[**表示**] メニューの [**ツールバー** ] を選択するか、CTRL + ALT + X キーを押します)。

 再 **スロー** アクティビティデザイナーは、[ **ツールボックス** ] からドラッグして、 [!INCLUDE[wfd2](../includes/wfd2-md.md)] アクティビティを通常配置している画面の任意の場所 (内など) にドロップできます <xref:System.Activities.Statements.Sequence> 。 これ <xref:System.Activities.Statements.Rethrow> により、Throw という既定の **DisplayName** を持つアクティビティが作成されます。 値は、再 <xref:System.Activities.Activity.DisplayName%2A> **スロー** アクティビティデザイナーのヘッダー、またはプロパティグリッドの [ **DisplayName** ] ボックスで編集できます。

### <a name="the-rethrow-properties"></a>Rethrow のプロパティ
 次の表に、<xref:System.Activities.Statements.Rethrow> のプロパティと、デザイナーでのその使用方法を示します。

|プロパティ名|必須|使用|
|-------------------|--------------|-----------|
|<xref:System.Activities.Activity.DisplayName%2A>|×|<xref:System.Activities.Statements.Rethrow> アクティビティの表示名を指定します (省略可能)。 既定値は Rethrow です。|

## <a name="see-also"></a>参照
 [コレクション](../workflow-designer/collection-activity-designers.md)[スロー](../workflow-designer/throw-activity-designer.md) [TryCatch](../workflow-designer/trycatch-activity-designer.md)