---
title: ワークフロー デザイナー - 受信送受信返信テンプレート デザイナー
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.ServiceModel.Activities.ReceiveAndSendReply.UI
- System.ServiceModel.Activities.SendReply.UI
ms.assetid: d1d9a058-df7e-48f5-a2e7-3caeeba7eaa6
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 042032efe745a9cb38bbf4e362cb5ad8440129ba
ms.sourcegitcommit: d6828e7422c8d74ec1e99146fedf0a05f757245f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/30/2020
ms.locfileid: "80395296"
---
# <a name="receiveandsendreply-template-designer"></a>ReceiveAndSendReply テンプレート デザイナー

**受信送受信応答**テンプレートは、事前構成<xref:System.ServiceModel.Activities.Receive>済みおよび<xref:System.ServiceModel.Activities.SendReply>アクティビティのペアを作成するために使用されます。 アクティビティは<xref:System.Activities.Statements.Sequence>アクティビティの一部であり、サーバー上の要求/応答メッセージ交換パターンの一部として関連付けられます。

## <a name="the-receiveandsendreply-template"></a>受信と送信返信テンプレート

**ReceiveAndSendReply**テンプレートを追加すると、アクティビティを使用<xref:System.ServiceModel.Activities.Receive>して<xref:System.ServiceModel.Activities.SendReply>と<xref:System.Activities.Statements.Sequence>アクティビティを作成する以外に、次の 3 つの処理が行われます。

- アクティビティの<xref:System.ServiceModel.Activities.Receive.OperationName%2A>プロパティ<xref:System.ServiceModel.Activities.Receive.ServiceContractName%2A>と プロパティ<xref:System.ServiceModel.Activities.Receive>を構成します。

- <xref:System.ServiceModel.Activities.SendReply.Request%2A> アクティビティの <xref:System.ServiceModel.Activities.Receive> プロパティを <xref:System.ServiceModel.Activities.Send> アクティビティにバインドする。

- 親アクティビティに、変数として <xref:System.ServiceModel.Activities.CorrelationHandle> を作成する。

### <a name="use-the-receiveandsendreply-template-designer"></a>テンプレート デザイナーを使用する

**ツールボックス**の**メッセージング**カテゴリにある**ReceiveAndSendReply**アクティビティ デザイナーにアクセスします。 **ReceiveAndSendReply**アクティビティ デザイナーは **、ツールボックス**からドラッグして、アクティビティが通常配置されているワークフロー デザイナー画面にドロップできます。 アクティビティ デザイナーを削除すると<xref:System.ServiceModel.Activities.Receive>**、Send**アクティビティ デザイナーで構成できるアクティビティと、SendReplyToReceive デザイナーで構成できる関連付け<xref:System.ServiceModel.Activities.SendReply>が作成されます。

Receive デザイナーを使用して<xref:System.ServiceModel.Activities.Receive>アクティビティを構成する方法の詳細については[、「Receive アクティビティ デザイナー](../workflow-designer/receive-activity-designer.md)」を参照してください。 **Receive**

### <a name="properties-of-sendreply"></a>SendReply のプロパティ

次の表に、<xref:System.ServiceModel.Activities.SendReply> のプロパティと、デザイナーでのその使用方法を示します。 これらのプロパティはプロパティ グリッドで編集でき、一部はワークフロー デザイナー画面で編集できます。

| プロパティ名 | 必須 | 使用法 |
|-|----------|-|
| <xref:System.Activities.Activity.DisplayName%2A> | False | <xref:System.ServiceModel.Activities.SendReply> アクティビティの省略可能な表示名。 既定値は SendReplyToReceive です。<br /><br /> フレンドリ<xref:System.Activities.Activity.DisplayName%2A>に対してデフォルト以外の値を使用する必要はありませんが、そのような値を使用することをお勧めします。 |
| <xref:System.ServiceModel.Activities.SendReply.Request%2A> | True | この <xref:System.ServiceModel.Activities.Receive> アクティビティと関連付けられる <xref:System.ServiceModel.Activities.SendReply> アクティビティへの参照。 このプロパティは**null**にすることはできません。 <xref:System.ServiceModel.Activities.Receive>アクティビティ<xref:System.ServiceModel.Activities.SendReply>は、要求/応答メッセージング パターンをモデル化するために、サーバー上で一緒に使用されます。 このプロパティでは、関連付ける <xref:System.ServiceModel.Activities.Send> アクティビティを指定します。 デザイナーでは、このプロパティは、<xref:System.ServiceModel.Activities.Send><xref:System.ServiceModel.Activities.SendReply>アクティビティの作成元アクティビティに自動的にバインドされるため、編集できません。 |
| <xref:System.ServiceModel.Activities.SendReply.Content%2A> | False | 受信するメッセージまたはパラメーターの内容を指定します。 <xref:System.ServiceModel.Activities.ReceiveMessageContent> アクティビティまたは <xref:System.ServiceModel.Activities.ReceiveParametersContent> アクティビティを指定できます。 このプロパティを編集するには、プロパティ グリッドの **[コンテンツ]** フィールドの横にある省略記号ボタンをクリックするか、**または Receive**アクティビティ デザイナー画面の **[コンテンツ]** ラベルの横にある [**定義**] ボタンをクリックします。 両方とも **[コンテンツ定義]ダイアログボックス**を表示します。 このボックスの使用方法の詳細については[、「[コンテンツ定義] ダイアログ ボックス」を](../workflow-designer/content-definition-dialog-box.md)参照してください。 |
| <xref:System.ServiceModel.Activities.SendReply.CorrelationInitializers%2A> | False | ワークフロー内のこの <xref:System.ServiceModel.Activities.CorrelationInitializer> アクティビティを構成する複数の <xref:System.ServiceModel.Activities.CorrelationHandle> オブジェクトを初期化する <xref:System.ServiceModel.Activities.Receive> オブジェクトのコレクションを指定します。 プロパティ グリッドで<xref:System.ServiceModel.Activities.SendReply.CorrelationInitializers%2A>プロパティの横にある省略記号ボタンをクリックして、[**相互関係初期化子の追加**] ダイアログ ボックスを開きます。 このボックスの使用方法の詳細については[、「[相互関係初期化子の追加] ダイアログ ボックス」を参照してください](../workflow-designer/add-correlationinitializers-dialog-box.md)。 |
| <xref:System.ServiceModel.Activities.SendReply.Action%2A> | False | メッセージのアクション ヘッダーを指定します。 明示的に設定されていない場合、その値はデフォルトで次のようになります。<br /><br /> `https://tempuri.org/{service contract namespace}/{service contract name}/{operation name}` |
| <xref:System.ServiceModel.Activities.SendReply.PersistBeforeSend%2A> | False | 応答メッセージを送信する前にワークフロー サービス インスタンスを永続化するかどうかを指定します。 既定値は **false** です。 |

## <a name="see-also"></a>関連項目

- [CorrelationScope](../workflow-designer/correlationscope-activity-designer.md)
- [InitializeCorrelation](../workflow-designer/initializecorrelation-activity-designer.md)
- [受信](../workflow-designer/receive-activity-designer.md)
- [送信](../workflow-designer/send-activity-designer.md)
- [SendAndReceiveReply](../workflow-designer/sendandreceivereply-template-designer.md)
- [TransactedReceiveScope](../workflow-designer/transactedreceivescope-activity-designer.md)