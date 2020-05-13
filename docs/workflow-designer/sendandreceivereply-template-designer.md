---
title: ワークフロー デザイナー - 送受信返信テンプレート デザイナー
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.ServiceModel.Activities.SendAndReceiveReply.UI
- System.ServiceModel.Activities.ReceiveReply.UI
ms.assetid: 818a8c84-6593-416d-b016-1d91b85ffb68
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2067ee92883d0c4ad3003f23032a88f5da3fa710
ms.sourcegitcommit: d6828e7422c8d74ec1e99146fedf0a05f757245f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/30/2020
ms.locfileid: "80395239"
---
# <a name="sendandreceivereply-template-designer"></a>SendAndReceiveReply テンプレート デザイナー

**SendAndReceiveReply**テンプレートは、構成済<xref:System.ServiceModel.Activities.Send>みと<xref:System.ServiceModel.Activities.ReceiveReply>アクティビティのペアを作成するために使用されます。 アクティビティは<xref:System.Activities.Statements.Sequence>アクティビティの一部であり、クライアント上の要求/応答メッセージ交換パターンの一部として関連付けられます。

## <a name="the-sendandreceivereply-template"></a>テンプレートを送信して受信します。

**SendAndReceiveReply**テンプレートを追加すると、アクティビティ内で<xref:System.ServiceModel.Activities.Send><xref:System.ServiceModel.Activities.ReceiveReply>と アクティビティ<xref:System.Activities.Statements.Sequence>を作成する以外に、次の 3 つの処理が実行されます。

- アクティビティの<xref:System.ServiceModel.Activities.Send.OperationName%2A>プロパティ<xref:System.ServiceModel.Activities.Send.ServiceContractName%2A>と プロパティ<xref:System.ServiceModel.Activities.Send>を構成します。

- <xref:System.ServiceModel.Activities.ReceiveReply.Request%2A> アクティビティの <xref:System.ServiceModel.Activities.ReceiveReply> プロパティを <xref:System.ServiceModel.Activities.Send> アクティビティにバインドする。

- 親アクティビティに、変数として <xref:System.ServiceModel.Activities.CorrelationHandle> を作成する。

### <a name="use-the-sendandreceivereply-template-designer"></a>送信および受信返信テンプレート デザイナーを使用する

**ツールボックス**の**メッセージング**カテゴリにある**SendAndReceiveReply**アクティビティ デザイナーにアクセスします。 **SendAndReceiveReply**アクティビティ デザイナーは **、ツールボックス**からドラッグして、アクティビティが通常配置されているワークフロー デザイナー画面にドロップできます。 アクティビティ デザイナーを削除すると<xref:System.ServiceModel.Activities.Send>**、Send**アクティビティ デザイナーで構成できるアクティビティと<xref:System.ServiceModel.Activities.ReceiveReply>**、ReceiveReplyForSend**デザイナーで構成できる関連付けが作成されます。

**Send**デザイナーを使用して<xref:System.ServiceModel.Activities.Send>アクティビティを構成する方法の詳細については、「[送信](../workflow-designer/send-activity-designer.md)」を参照してください。

### <a name="properties-of-receivereply"></a>ReceiveReply のプロパティ

次の表に、<xref:System.ServiceModel.Activities.ReceiveReply>プロパティと、デザイナーでのプロパティの使用方法を示します。 これらのプロパティはプロパティ グリッドで編集でき、一部はワークフロー デザイナー画面で編集できます。

| プロパティ名 | 必須 | 使用法 |
|-|----------|-|
| <xref:System.Activities.Activity.DisplayName%2A> | False | <xref:System.ServiceModel.Activities.ReceiveReply> アクティビティの省略可能な表示名。 既定値は、ReceiveReplyForSend です。<br /><br /> フレンドリ<xref:System.Activities.Activity.DisplayName%2A>に対してデフォルト以外の値を使用する必要はありませんが、そのような値を使用することをお勧めします。 |
| <xref:System.ServiceModel.Activities.ReceiveReply.Request%2A> | True | この <xref:System.ServiceModel.Activities.Send> アクティビティと関連付けられる <xref:System.ServiceModel.Activities.ReceiveReply> アクティビティへの参照。 このプロパティは**null**にすることはできません。 <xref:System.ServiceModel.Activities.Send>と<xref:System.ServiceModel.Activities.ReceiveReply>アクティビティは、要求/応答メッセージング パターンをモデル化するためにクライアント上で一緒に使用されます。 このプロパティでは、関連付ける <xref:System.ServiceModel.Activities.Send> アクティビティを指定します。 デザイナーでは、このプロパティは、<xref:System.ServiceModel.Activities.Send><xref:System.ServiceModel.Activities.ReceiveReply>アクティビティの作成元アクティビティに自動的にバインドされるため、編集できません。 |
| <xref:System.ServiceModel.Activities.ReceiveReply.Content%2A> | False | 受信するメッセージまたはパラメーターの内容を指定します。 <xref:System.ServiceModel.Activities.ReceiveMessageContent> アクティビティまたは <xref:System.ServiceModel.Activities.ReceiveParametersContent> アクティビティを指定できます。 このプロパティを編集するには、プロパティ グリッドの **[コンテンツ]** フィールドの横にある省略記号ボタンをクリックするか、**または Receive**アクティビティ デザイナー画面の **[コンテンツ]** ラベルの横にある [**定義**] ボタンをクリックします。 両方とも **[コンテンツ定義]ダイアログボックス**を表示します。 このボックスの使用方法の詳細については、「 [[コンテンツ定義] ダイアログ ボックス](../workflow-designer/content-definition-dialog-box.md)」を参照してください。 |
| <xref:System.ServiceModel.Activities.ReceiveReply.CorrelationInitializers%2A> | False | ワークフロー内のこの <xref:System.ServiceModel.Activities.CorrelationInitializer> アクティビティを構成する複数の <xref:System.ServiceModel.Activities.CorrelationHandle> オブジェクトを初期化する <xref:System.ServiceModel.Activities.Receive> オブジェクトのコレクションを指定します。 プロパティ グリッドで<xref:System.ServiceModel.Activities.Receive.CorrelationInitializers%2A>プロパティの横にある省略記号ボタンをクリックして、[**相互関係初期化子の追加**] ダイアログ ボックスを開きます。 このボックスの使用の詳細については、「 [[相互関係初期化子の追加] ダイアログ ボックス](../workflow-designer/add-correlationinitializers-dialog-box.md)」を参照してください。 |
| <xref:System.ServiceModel.Activities.ReceiveReply.Action%2A> | False | メッセージのアクション ヘッダーを指定します。 明示的に設定されていない場合、その値はデフォルトで次のようになります。<br /><br /> `https://tempuri.org/{service contract namespace}/{service contract name}/{operation name}`. |

## <a name="see-also"></a>関連項目

- [CorrelationScope](../workflow-designer/correlationscope-activity-designer.md)
- [InitializeCorrelation](../workflow-designer/initializecorrelation-activity-designer.md)
- [受信](../workflow-designer/receive-activity-designer.md)
- [ReceiveAndSendReply](../workflow-designer/receiveandsendreply-template-designer.md)
- [送信](../workflow-designer/send-activity-designer.md)
- [TransactedReceiveScope](../workflow-designer/transactedreceivescope-activity-designer.md)