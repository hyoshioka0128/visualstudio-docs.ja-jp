---
title: ワークフローデザイナー-SendAndReceiveReply テンプレートデザイナー
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.ServiceModel.Activities.SendAndReceiveReply.UI
- System.ServiceModel.Activities.ReceiveReply.UI
ms.assetid: 818a8c84-6593-416d-b016-1d91b85ffb68
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 17512337b58fb394352ccaab153ca72badbb4652
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "86875905"
---
# <a name="sendandreceivereply-template-designer"></a>SendAndReceiveReply テンプレート デザイナー

**Sendandreceivereply**テンプレートは、事前に構成されたアクティビティとアクティビティのペアを作成するために使用され <xref:System.ServiceModel.Activities.Send> <xref:System.ServiceModel.Activities.ReceiveReply> ます。 アクティビティは、アクティビティの一部 <xref:System.Activities.Statements.Sequence> であり、クライアントでの要求/応答メッセージ交換パターンの一部として関連付けられています。

## <a name="the-sendandreceivereply-template"></a>SendAndReceiveReply テンプレート

**Sendandreceivereply**テンプレートを追加するには、アクティビティ内にアクティビティとアクティビティを作成する以外に、次の3つの操作を <xref:System.ServiceModel.Activities.Send> <xref:System.ServiceModel.Activities.ReceiveReply> <xref:System.Activities.Statements.Sequence> 行います。

- <xref:System.ServiceModel.Activities.Send.OperationName%2A> <xref:System.ServiceModel.Activities.Send.ServiceContractName%2A> アクティビティのプロパティおよびプロパティを構成し <xref:System.ServiceModel.Activities.Send> ます。

- <xref:System.ServiceModel.Activities.ReceiveReply.Request%2A> アクティビティの <xref:System.ServiceModel.Activities.ReceiveReply> プロパティを <xref:System.ServiceModel.Activities.Send> アクティビティにバインドする。

- 親アクティビティに、変数として <xref:System.ServiceModel.Activities.CorrelationHandle> を作成する。

### <a name="use-the-sendandreceivereply-template-designer"></a>SendAndReceiveReply テンプレートデザイナーを使用する

[**ツールボックス**] の [**メッセージング**] カテゴリにある**sendandreceivereply**アクティビティデザイナーにアクセスします。 **Sendandreceivereply**アクティビティデザイナーは、[**ツールボックス**] からドラッグして、アクティビティを通常配置している任意の場所でワークフローデザイナー画面にドロップできます。 アクティビティデザイナーを削除する <xref:System.ServiceModel.Activities.Send> と、 **send** アクティビティデザイナーで構成できるアクティビティと、 <xref:System.ServiceModel.Activities.ReceiveReply> **receivereplyforsend** デザイナーで構成できる相関が作成されます。

**送信**デザイナーを使用してアクティビティを構成する方法の詳細については <xref:System.ServiceModel.Activities.Send> 、「 [send](../workflow-designer/send-activity-designer.md)」を参照してください。

### <a name="properties-of-receivereply"></a>ReceiveReply のプロパティ

次の表は、 <xref:System.ServiceModel.Activities.ReceiveReply> プロパティと、デザイナーでのそれらの使用方法を示しています。 これらのプロパティは、プロパティグリッドで編集できます。また、ワークフローデザイナーサーフェイスで編集することもできます。

| プロパティ名 | 必須 | 使用法 |
|-|----------|-|
| <xref:System.Activities.Activity.DisplayName%2A> | × | <xref:System.ServiceModel.Activities.ReceiveReply> アクティビティの省略可能な表示名。 既定値は、ReceiveReplyForSend です。<br /><br /> フレンドリに既定値以外の値を使用 <xref:System.Activities.Activity.DisplayName%2A> することは、厳密には必須ではありませんが、このような値を使用することをお勧めします。 |
| <xref:System.ServiceModel.Activities.ReceiveReply.Request%2A> | ○ | この <xref:System.ServiceModel.Activities.Send> アクティビティと関連付けられる <xref:System.ServiceModel.Activities.ReceiveReply> アクティビティへの参照。 このプロパティを **null**にすることはできません。 <xref:System.ServiceModel.Activities.Send> と <xref:System.ServiceModel.Activities.ReceiveReply> アクティビティは、要求/応答のメッセージングパターンをモデル化するために、クライアントで一緒に使用されます。 このプロパティでは、関連付ける <xref:System.ServiceModel.Activities.Send> アクティビティを指定します。 デザイナーでは、アクティビティを作成したアクティビティに自動的にバインドされるため、このプロパティを編集することはできません <xref:System.ServiceModel.Activities.Send> <xref:System.ServiceModel.Activities.ReceiveReply> 。 |
| <xref:System.ServiceModel.Activities.ReceiveReply.Content%2A> | × | 受信するメッセージまたはパラメーターの内容を指定します。 <xref:System.ServiceModel.Activities.ReceiveMessageContent> アクティビティまたは <xref:System.ServiceModel.Activities.ReceiveParametersContent> アクティビティを指定できます。 このプロパティを編集するには、プロパティグリッドで**コンテンツ**フィールドの横にある省略記号ボタンをクリックするか、 **Receive**アクティビティデザイナー画面で [**コンテンツ**] ラベルの横にある [**定義**] をクリックします。 どちらの場合も、[ **コンテンツ定義** ] ダイアログボックスが表示されます。 このボックスの使用方法の詳細については、「[ [コンテンツ定義] ダイアログボックス](../workflow-designer/content-definition-dialog-box.md)」を参照してください。 |
| <xref:System.ServiceModel.Activities.ReceiveReply.CorrelationInitializers%2A> | × | ワークフロー内のこの <xref:System.ServiceModel.Activities.CorrelationInitializer> アクティビティを構成する複数の <xref:System.ServiceModel.Activities.CorrelationHandle> オブジェクトを初期化する <xref:System.ServiceModel.Activities.Receive> オブジェクトのコレクションを指定します。 プロパティグリッドでプロパティの横にある省略記号ボタンをクリックして <xref:System.ServiceModel.Activities.Receive.CorrelationInitializers%2A> 、[ **関連付け初期化子の追加** ] ダイアログボックスを開きます。 このボックスの使用方法の詳細については、「 [CorrelationInitializers の追加」ダイアログボックス](../workflow-designer/add-correlationinitializers-dialog-box.md)を参照してください。 |
| <xref:System.ServiceModel.Activities.ReceiveReply.Action%2A> | × | メッセージのアクション ヘッダーを指定します。 明示的に設定されていない場合、その値の既定値は次のようになります。<br /><br /> `https://tempuri.org/{service contract namespace}/{service contract name}/{operation name}`. |

## <a name="see-also"></a>関連項目

- [CorrelationScope](../workflow-designer/correlationscope-activity-designer.md)
- [InitializeCorrelation](../workflow-designer/initializecorrelation-activity-designer.md)
- [受け取れ](../workflow-designer/receive-activity-designer.md)
- [ReceiveAndSendReply](../workflow-designer/receiveandsendreply-template-designer.md)
- [送信](../workflow-designer/send-activity-designer.md)
- [TransactedReceiveScope](../workflow-designer/transactedreceivescope-activity-designer.md)