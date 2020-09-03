---
title: Throw アクティビティデザイナー |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Throw.UI
ms.assetid: 5e97c947-be39-4a1f-af04-000e2e09528a
caps.latest.revision: 4
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 1855daa5016241fb6eb04f05d7218e02083fc0a8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72655158"
---
# <a name="throw-activity-designer"></a>Throw アクティビティ デザイナー
**Throw**アクティビティデザイナーは、アクティビティを作成および構成するために使用され <xref:System.Activities.Statements.Throw> ます。

## <a name="the-throw-activity"></a>Throw アクティビティ
 <xref:System.Activities.Statements.Throw> アクティビティによって例外がスローされます。

### <a name="using-the-throw-activity-designer"></a>Throw アクティビティ デザイナーの使用
 **Throw**アクティビティデザイナーは、[**ツールボックス**] の [**エラー処理**] カテゴリにあります。このカテゴリにアクセスするには、の左側にある [**ツールボックス**] タブをクリックします [!INCLUDE[wfd2](../includes/wfd2-md.md)] (または、[**表示**] メニューの [**ツールバー** ] を選択するか、CTRL + ALT + X キーを押します)。

 **Throw**アクティビティデザイナーは、[**ツールボックス**] からドラッグして、 [!INCLUDE[wfd2](../includes/wfd2-md.md)] アクティビティを通常配置している画面の任意の場所 (内など) にドロップできます <xref:System.Activities.Statements.Sequence> 。 これ <xref:System.Activities.Statements.Throw> により、Throw という既定の **DisplayName** を持つアクティビティが作成されます。 この <xref:System.Activities.Activity.DisplayName%2A> 値は、 **Throw** アクティビティデザイナーのヘッダー、またはプロパティグリッドの [ **DisplayName** ] ボックスで編集できます。 この <xref:System.Activities.Statements.Throw.Exception%2A> プロパティは、プロパティ グリッドで編集する必要があります。

### <a name="the-throw-properties"></a>Throw プロパティ
 次の表に、<xref:System.Activities.Statements.Throw> のプロパティと、デザイナーでのその使用方法を示します。

|プロパティ名|必須|使用法|
|-------------------|--------------|-----------|
|<xref:System.Activities.Activity.DisplayName%2A>|×|<xref:System.Activities.Statements.Throw> アクティビティの表示名を指定します (省略可能)。 既定値は Throw です。|
|<xref:System.Activities.Statements.Throw.Exception%2A>|True|スローされる例外。 この例外は、<xref:System.Exception> から派生していることが必要です。 例外を指定するには、プロパティ グリッドで Visual Basic の式を入力します。|

## <a name="see-also"></a>参照
 [コレクション](../workflow-designer/collection-activity-designers.md)[再スロー](../workflow-designer/rethrow-activity-designer.md) [スローアクティビティデザイナー](../workflow-designer/throw-activity-designer.md) [TryCatch](../workflow-designer/trycatch-activity-designer.md)