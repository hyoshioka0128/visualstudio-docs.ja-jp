---
title: '[関連付けの初期化] ダイアログボックス |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- InitializeCorrelation.UI
ms.assetid: 2a0a1cd3-7b9e-493e-9264-fcf85289ffcf
caps.latest.revision: 6
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 3ab913027a6a992494dad609b98ab11dbc6ae61c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72659051"
---
# <a name="initialize-correlation-dialog-box"></a>[関連付け初期化] ダイアログ ボックス
[ **関連付けの初期化** ] ダイアログボックスは、 [!INCLUDE[wfd1](../includes/wfd1-md.md)] アクティビティのプロパティを編集するために、で使用され <xref:System.ServiceModel.Activities.InitializeCorrelation.CorrelationData%2A> <xref:System.ServiceModel.Activities.InitializeCorrelation> ます。 [!INCLUDE[crdefault](../includes/crdefault-md.md)][InitializeCorrelation](../workflow-designer/initializecorrelation-activity-designer.md)トピックを参照してください。

 次の表では、[ **関連付けの初期化** ] ダイアログボックスのユーザーインターフェイス (UI) 要素について説明します。

|UI 要素|説明|
|----------------|-----------------|
|**Correlation (関連付け)** |初期化する関連付けの <xref:System.ServiceModel.Activities.CorrelationHandle>。|
|**初期化**|初期化するデータが格納されているキー/値ペア。 これは、<xref:System.ServiceModel.Activities.InitializeCorrelation.CorrelationData%2A> プロパティに対応します。 有効なキー/値ペアには、"OrderID" という名前のキーと、OrderID という名前の変数のペアなどがあります。|

## <a name="to-launch-the-initialize-correlation-dialog-box"></a>[関連付け初期化] ダイアログ ボックスを開くには

- **InitializeCorrelation**アクティビティデザイナーで [**表示**] をクリックするか、でアクティビティを選択し、 <xref:System.ServiceModel.Activities.InitializeCorrelation> [!INCLUDE[wfd2](../includes/wfd2-md.md)] プロパティグリッドでプロパティの横にある省略記号ボタンをクリックし <xref:System.ServiceModel.Activities.InitializeCorrelation.CorrelationData%2A> ます。

## <a name="see-also"></a>参照
 [InitializeCorrelation](../workflow-designer/initializecorrelation-activity-designer.md)