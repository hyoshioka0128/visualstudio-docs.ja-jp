---
title: ワークフローデザイナー-[CorrelationInitializers の追加] ダイアログボックス
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- AddCorrelationInitializers.UI
ms.assetid: c0517467-d54a-4ee6-aef0-c19b96b6f395
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9d2a0b0f7c76b392d5d2d0135c3ab6e370f8678e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "76114303"
---
# <a name="add-correlationinitializers-dialog-box"></a>[関連付け初期化子の追加] ダイアログ ボックス

[ **関連付け初期化子の追加** ] ダイアログボックスは、、、、およびの各アクティビティの **correlationinitializers** プロパティを構成するためにワークフローデザイナーで使用され <xref:System.ServiceModel.Activities.Send> <xref:System.ServiceModel.Activities.Receive> <xref:System.ServiceModel.Activities.SendReply> <xref:System.ServiceModel.Activities.ReceiveReply> ます。 このボックスを使用するアクティビティデザイナーの詳細については、「 [Send](../workflow-designer/send-activity-designer.md)、 [Receive](../workflow-designer/receive-activity-designer.md)、 [Receiveandsendreply](../workflow-designer/receiveandsendreply-template-designer.md)、および [sendandreceivereply](../workflow-designer/sendandreceivereply-template-designer.md) 」のトピックを参照してください。

このダイアログボックスで指定したコレクション内の関連付け初期化子は、メッセージングアクティビティ間の次の相関関係を初期化できます。

- クエリベース
- context
- コールバックコンテキスト
- 要求-応答

次の表では、[ **関連付け初期化子の追加** ] ダイアログボックスのユーザーインターフェイス (UI) 要素について説明します。

|UI 要素|説明|
|-|-----------------|
|**初期化子の追加**|[ **初期化の追加** ] ボックスをクリックして、追加の初期化子をコレクションに追加します。|
|**[関連付けの種類]**|関連付け初期化子の種類を指定します。 次の 4 種類から選択できます。<br /><br /> 1. を指定するコールバック関連付け初期化子 <xref:System.ServiceModel.Activities.CallbackCorrelationInitializer> 。<br />2. を指定するコンテキスト関連付け初期化子 <xref:System.ServiceModel.Activities.CorrelationInitializer> 。<br />3. を指定するための要求と応答の関連付け初期化子 <xref:System.ServiceModel.Activities.RequestReplyCorrelationInitializer> 。<br />4. を指定するためのクエリ関連付け初期化子 <xref:System.ServiceModel.Activities.QueryCorrelationInitializer> 。<br /><br /> **Correlationtype**を編集するには<br /><br /> 1. [ **初期化子の追加** ] DataGrid の特定の行にタブを追加します。<br />2. **correlationtypecombobox**にフォーカスを設定するには、 **ctrl** + **tab**キーを押します。<br />3. Alt + ↓キーを押して、 **コンボボックス** をポップアップ表示して編集します。|
|**XPath クエリ**|送受信メッセージから相関関係データを抽出するためのクエリを含む、キーと値のペア。 このリストは、<xref:System.ServiceModel.Activities.QueryCorrelationInitializer> 型を使用している場合にのみ有効です。|

## <a name="to-launch-the-add-correlation-initializers-dialog-box"></a>[関連付け初期化子の追加] ダイアログ ボックスを開くには

 [ **関連付け初期化子の追加** ] ダイアログボックスは、 **Send**、 **Receive**、 **Receiveandsendreply**、および **sendandreceivereply** の各デザイナーによって使用されます。 これらにアクセスすることは、それぞれのケースで似ています。ここでは、この手順を説明するために、 **受信** デザイナーに関係するケースを使用します。

 **Receive**アクティビティデザイナーは、[**ツールボックス**] からドラッグして、アクティビティが配置されている任意の場所のワークフローデザイナー画面にドロップできます。 **Receive**アクティビティデザイナーを削除すると、receive という <xref:System.ServiceModel.Activities.Receive> 既定のを持つアクティビティが作成さ <xref:System.Activities.Activity.DisplayName%2A> れます。 **Receive**アクティビティデザイナーを選択し、[**関連付け初期化子の追加**] ダイアログボックスのプロパティグリッドで、 **Correlationinitializers**プロパティの (コレクション) テキストの横にある省略記号ボタンをクリックします。

## <a name="see-also"></a>関連項目

- [[関連付け初期化] ダイアログ ボックス](../workflow-designer/initialize-correlation-dialog-box.md)
