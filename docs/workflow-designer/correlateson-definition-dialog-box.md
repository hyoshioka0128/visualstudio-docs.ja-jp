---
title: '[ワークフローデザイナー-[Correlateson の定義] ダイアログボックス'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CorrelatesOnDefinition.UI
ms.assetid: 8b2b627a-f236-4479-aa09-525df65e3413
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8d2db5bbfa4f34d86d3bf20cfe6bcc42b3dc00d0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "86876126"
---
# <a name="correlateson-definition-dialog-box"></a>[CorrelatesOn の定義] ダイアログ ボックス

[ **[Correlateson** ] ダイアログボックスは、アクティビティのプロパティを編集するためにワークフローデザイナーで使用され <xref:System.ServiceModel.Activities.Receive.CorrelatesOn%2A> <xref:System.ServiceModel.Activities.Receive> ます。 詳細については、「 [Receive アクティビティデザイナー](../workflow-designer/receive-activity-designer.md)」を参照してください。

<xref:System.ServiceModel.Activities.Receive> アクティビティの間の相関関係によって、ワークフロー内でさまざまなサービス操作が相互に接続される方法が指定されます。

次の表では、[ **[correlateson** ] ダイアログボックスのユーザーインターフェイス (UI) 要素について説明します。

|UI 要素|説明|
|-|-----------------|
|**CorrelatesWith**|適切なワークフロー インスタンスにメッセージをルーティングするために使用される <xref:System.ServiceModel.Activities.CorrelationHandle>。|
|**XPath クエリ**|受信メッセージから相関関係データを抽出するためのクエリを含む、キーと値のペア。 この値は、プロパティに対応 <xref:System.ServiceModel.Activities.Receive.CorrelatesOn%2A> しています。 XPath クエリは、<xref:System.ServiceModel.MessageQuerySet> オブジェクトに含まれます。|

## <a name="to-launch-the-correlateson-dialog-box"></a>[CorrelatesOn] ダイアログ ボックスを起動するには

**Receive**アクティビティデザイナーは、[**ツールボックス**] からドラッグして、アクティビティを通常配置している任意の場所でワークフローデザイナー画面にドロップできます。 アクティビティデザイナーを削除すると、Receive という <xref:System.ServiceModel.Activities.Receive> 既定のを持つアクティビティが作成さ <xref:System.Activities.Activity.DisplayName%2A> れます。 [[Correlateson の **定義** ] ダイアログボックスを開くには、 **Receive** アクティビティデザイナーを選択し、プロパティグリッドで、 **[correlateson** プロパティのコレクションテキストの横にある省略記号ボタンを選択します。

## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Activities.Receive>
- [[関連付け初期化子の追加] ダイアログ ボックス](../workflow-designer/add-correlationinitializers-dialog-box.md)
- [[関連付け初期化] ダイアログ ボックス](../workflow-designer/initialize-correlation-dialog-box.md)