---
title: ワークフローデザイナー ReceiveAndSendReply テンプレートデザイナー
description: ReceiveAndSendReply テンプレートを使用して、事前に構成された Receive アクティビティと SendReply アクティビティのペアを作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.ServiceModel.Activities.ReceiveAndSendReply.UI
- System.ServiceModel.Activities.SendReply.UI
ms.assetid: d1d9a058-df7e-48f5-a2e7-3caeeba7eaa6
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3b66b403fb5df98bc4a23131b6062b2d06f95719
ms.sourcegitcommit: ed26b6e313b766c4d92764c303954e2385c6693e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/10/2020
ms.locfileid: "94434169"
---
# <a name="receiveandsendreply-template-designer"></a>ReceiveAndSendReply テンプレート デザイナー

**Receiveandsendreply** テンプレートは、事前に構成されたアクティビティとアクティビティのペアを作成するために使用され <xref:System.ServiceModel.Activities.Receive> <xref:System.ServiceModel.Activities.SendReply> ます。 アクティビティは、アクティビティの一部であり、 <xref:System.Activities.Statements.Sequence> サーバー上の要求/応答メッセージ交換パターンの一部として関連付けられています。

## <a name="the-receiveandsendreply-template"></a>ReceiveAndSendReply テンプレート

**Receiveandsendreply** テンプレートを追加すると、アクティビティを含むアクティビティとアクティビティを作成する以外に、次の3つの処理が行われ <xref:System.ServiceModel.Activities.Receive> <xref:System.ServiceModel.Activities.SendReply> <xref:System.Activities.Statements.Sequence> ます。

- <xref:System.ServiceModel.Activities.Receive.OperationName%2A> <xref:System.ServiceModel.Activities.Receive.ServiceContractName%2A> アクティビティのプロパティおよびプロパティを構成し <xref:System.ServiceModel.Activities.Receive> ます。

- <xref:System.ServiceModel.Activities.SendReply.Request%2A> アクティビティの <xref:System.ServiceModel.Activities.Receive> プロパティを <xref:System.ServiceModel.Activities.Send> アクティビティにバインドする。

- 親アクティビティに、変数として <xref:System.ServiceModel.Activities.CorrelationHandle> を作成する。

### <a name="use-the-receiveandsendreply-template-designer"></a>ReceiveAndSendReply テンプレートデザイナーを使用する

[ **ツールボックス** ] の [ **メッセージング** ] カテゴリで、 **receiveandsendreply** アクティビティデザイナーにアクセスします。 **Receiveandsendreply** アクティビティデザイナーは、[ **ツールボックス** ] からドラッグして、アクティビティを通常配置している任意の場所でワークフローデザイナー画面にドロップできます。 アクティビティデザイナーを削除する <xref:System.ServiceModel.Activities.Receive> と、 **Send** アクティビティデザイナーで構成できるアクティビティと、 <xref:System.ServiceModel.Activities.SendReply> SendReplyToReceive デザイナーで構成できる相関が作成されます。

**Receive** designer を使用してアクティビティを構成する方法の詳細について <xref:System.ServiceModel.Activities.Receive> は、「 [receive アクティビティデザイナー](../workflow-designer/receive-activity-designer.md)」を参照してください。

### <a name="properties-of-sendreply"></a>SendReply のプロパティ

次の表に、<xref:System.ServiceModel.Activities.SendReply> のプロパティと、デザイナーでのその使用方法を示します。 これらのプロパティは、[プロパティ] グリッドで編集できます。また、一部のプロパティは、ワークフローデザイナー画面で編集できます。

| プロパティ名 | 必須 | 使用法 |
|-|----------|-|
| <xref:System.Activities.Activity.DisplayName%2A> | × | <xref:System.ServiceModel.Activities.SendReply> アクティビティの省略可能な表示名。 既定値は SendReplyToReceive です。<br /><br /> フレンドリに既定値以外の値を使用 <xref:System.Activities.Activity.DisplayName%2A> することは、厳密には必須ではありませんが、このような値を使用することをお勧めします。 |
| <xref:System.ServiceModel.Activities.SendReply.Request%2A> | ○ | この <xref:System.ServiceModel.Activities.Receive> アクティビティと関連付けられる <xref:System.ServiceModel.Activities.SendReply> アクティビティへの参照。 このプロパティを **null** にすることはできません。 <xref:System.ServiceModel.Activities.Receive> と <xref:System.ServiceModel.Activities.SendReply> アクティビティは、要求/応答メッセージングパターンをモデル化するために、サーバー上で一緒に使用されます。 このプロパティでは、関連付ける <xref:System.ServiceModel.Activities.Send> アクティビティを指定します。 デザイナーでは、アクティビティを作成したアクティビティに自動的にバインドされるため、このプロパティを編集することはできません <xref:System.ServiceModel.Activities.Send> <xref:System.ServiceModel.Activities.SendReply> 。 |
| <xref:System.ServiceModel.Activities.SendReply.Content%2A> | × | 受信するメッセージまたはパラメーターの内容を指定します。 <xref:System.ServiceModel.Activities.ReceiveMessageContent> アクティビティまたは <xref:System.ServiceModel.Activities.ReceiveParametersContent> アクティビティを指定できます。 このプロパティを編集するには、プロパティグリッドで **コンテンツ** フィールドの横にある省略記号ボタンをクリックするか、 **Receive** アクティビティデザイナー画面で [ **コンテンツ** ] ラベルの横にある [ **定義** ] ボタンをクリックします。 どちらの場合も、[ **コンテンツ定義** ] ダイアログボックスが表示されます。 このボックスの使用方法の詳細については、「[ [コンテンツ定義] ダイアログボックス](../workflow-designer/content-definition-dialog-box.md) 」を参照してください。 |
| <xref:System.ServiceModel.Activities.SendReply.CorrelationInitializers%2A> | × | ワークフロー内のこの <xref:System.ServiceModel.Activities.CorrelationInitializer> アクティビティを構成する複数の <xref:System.ServiceModel.Activities.CorrelationHandle> オブジェクトを初期化する <xref:System.ServiceModel.Activities.Receive> オブジェクトのコレクションを指定します。 プロパティグリッドでプロパティの横にある省略記号ボタンをクリックして <xref:System.ServiceModel.Activities.SendReply.CorrelationInitializers%2A> 、[ **関連付け初期化子の追加** ] ダイアログボックスを開きます。 このボックスの使用方法の詳細については、「[ [CorrelationInitializers の追加] ダイアログボックス](../workflow-designer/add-correlationinitializers-dialog-box.md) 」を参照してください。 |
| <xref:System.ServiceModel.Activities.SendReply.Action%2A> | × | メッセージのアクション ヘッダーを指定します。 明示的に設定されていない場合、その値の既定値は次のようになります。<br /><br /> `https://tempuri.org/{service contract namespace}/{service contract name}/{operation name}` |
| <xref:System.ServiceModel.Activities.SendReply.PersistBeforeSend%2A> | × | 応答メッセージを送信する前にワークフロー サービス インスタンスを永続化するかどうかを指定します。 既定値は **false** です。 |

## <a name="see-also"></a>関連項目

- [CorrelationScope](../workflow-designer/correlationscope-activity-designer.md)
- [InitializeCorrelation](../workflow-designer/initializecorrelation-activity-designer.md)
- [受け取れ](../workflow-designer/receive-activity-designer.md)
- [Send](../workflow-designer/send-activity-designer.md)
- [SendAndReceiveReply](../workflow-designer/sendandreceivereply-template-designer.md)
- [TransactedReceiveScope](../workflow-designer/transactedreceivescope-activity-designer.md)