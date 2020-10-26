---
title: ワークフローデザイナー-[関連付けの初期化] ダイアログボックス
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- InitializeCorrelation.UI
ms.assetid: 2a0a1cd3-7b9e-493e-9264-fcf85289ffcf
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 04f0a3bb70dbab31e0faa5c38caac9b54c6154fe
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "76114779"
---
# <a name="initialize-correlation-dialog-box"></a>[関連付け初期化] ダイアログ ボックス

[ **関連付けの初期化** ] ダイアログボックスは、アクティビティのプロパティを編集するためにワークフローデザイナーで使用され <xref:System.ServiceModel.Activities.InitializeCorrelation.CorrelationData%2A> <xref:System.ServiceModel.Activities.InitializeCorrelation> ます。 詳細については、「 [InitializeCorrelation](../workflow-designer/initializecorrelation-activity-designer.md)」を参照してください。

次の表では、[ **関連付けの初期化** ] ダイアログボックスのユーザーインターフェイス (UI) 要素について説明します。

|UI 要素|説明|
|-|-----------------|
|**Correlation (関連付け)** |初期化する関連付けの <xref:System.ServiceModel.Activities.CorrelationHandle>。|
|**初期化**|初期化するデータが格納されているキー/値ペア。 この値は、プロパティに対応 <xref:System.ServiceModel.Activities.InitializeCorrelation.CorrelationData%2A> しています。 有効なキーと値のペアの例としては、OrderID という名前の変数と組み合わせた "OrderID" という名前のキーがあります。|

## <a name="to-launch-the-initialize-correlation-dialog-box"></a>[関連付け初期化] ダイアログ ボックスを開くには

**InitializeCorrelation**アクティビティデザイナーで [**表示**] をクリックするか、 <xref:System.ServiceModel.Activities.InitializeCorrelation> ワークフローデザイナーでアクティビティを選択します。 次に、プロパティグリッドでプロパティの横にある省略記号ボタンをクリックし <xref:System.ServiceModel.Activities.InitializeCorrelation.CorrelationData%2A> ます。

## <a name="see-also"></a>関連項目

- [InitializeCorrelation](../workflow-designer/initializecorrelation-activity-designer.md)
