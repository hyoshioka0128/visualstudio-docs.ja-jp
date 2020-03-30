---
title: 受信送受信返信テンプレート デザイナー |マイクロソフトドキュメント
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.ServiceModel.Activities.ReceiveAndSendReply.UI
- System.ServiceModel.Activities.SendReply.UI
ms.assetid: d1d9a058-df7e-48f5-a2e7-3caeeba7eaa6
caps.latest.revision: 5
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 4c00eed244867cfd38b20f6a8f065fc6da006801
ms.sourcegitcommit: d6828e7422c8d74ec1e99146fedf0a05f757245f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/30/2020
ms.locfileid: "80395386"
---
# <a name="receiveandsendreply-template-designer"></a>ReceiveAndSendReply テンプレート デザイナー
**ReceiveAndSendReply**テンプレートは、サーバー上の要求/応答メッセージ交換<xref:System.ServiceModel.Activities.Receive>パターン<xref:System.ServiceModel.Activities.SendReply>の一部<xref:System.Activities.Statements.Sequence>として関連付けられているアクティビティ内で構成済みのアクティビティとアクティビティのペアを作成するために使用されます。

## <a name="the-receiveandsendreply-template"></a>ReceiveAndSendReply テンプレート
 **ReceiveAndSendReply**テンプレートを追加すると、アクティビティを<xref:System.ServiceModel.Activities.Receive>使用<xref:System.ServiceModel.Activities.SendReply>して と<xref:System.Activities.Statements.Sequence>アクティビティを作成する以外に、次の 3 つの処理が行われます。

1. <xref:System.ServiceModel.Activities.Receive.OperationName%2A> アクティビティの <xref:System.ServiceModel.Activities.Receive.ServiceContractName%2A> プロパティと <xref:System.ServiceModel.Activities.Receive> プロパティを構成する。

2. <xref:System.ServiceModel.Activities.SendReply.Request%2A> アクティビティの <xref:System.ServiceModel.Activities.Receive> プロパティを <xref:System.ServiceModel.Activities.Send> アクティビティにバインドする。

3. 親アクティビティに、変数として <xref:System.ServiceModel.Activities.CorrelationHandle> を作成する。

### <a name="using-the-receiveandsendreply-template-designer"></a>ReceiveAndSendReply テンプレート デザイナーの使用
 **ReceiveAndSendReply**アクティビティ デザイナーは、**ツールボックス**の [**View****Toolbox****メッセージング**] カテゴリにあります。 **Toolbar** [!INCLUDE[wfd2](../includes/wfd2-md.md)]

 **ReceiveAndSendReply**アクティビティ デザイナーは **、ツールボックス**からドラッグして、通常、アクティビティ[!INCLUDE[wfd2](../includes/wfd2-md.md)]が配置されている場所にドロップできます。 これにより、Send<xref:System.ServiceModel.Activities.Receive>アクティビティ デザイナーと **、SendReplyToReceive**デザイナーで構成<xref:System.ServiceModel.Activities.SendReply>できる関連付けで構成できるアクティビティが作成されます。

 [!INCLUDE[crabout](../includes/crabout-md.md)]**Receive**デザイナーを使用してアクティビティ<xref:System.ServiceModel.Activities.Receive>を構成するには、「[受信](../workflow-designer/receive-activity-designer.md)」トピックを参照してください。

 [!INCLUDE[crabout](../includes/crabout-md.md)]**SendReplyToReceive**デザイナーを使用してアクティビティ<xref:System.ServiceModel.Activities.SendReply>を構成するには、次のセクションを参照してください。

### <a name="properties-of-sendreply"></a>SendReply のプロパティ
 次の表に、<xref:System.ServiceModel.Activities.SendReply> のプロパティと、デザイナーでのその使用方法を示します。 これらのプロパティは、プロパティ グリッドで編集できます。また、その一部は[!INCLUDE[wfd2](../includes/wfd2-md.md)]のデザイナー画面で編集できます。

|                               プロパティ名                                | 必須 |                                                                                                                                                                                                                                                                                                                                                      使用法                                                                                                                                                                                                                                                                                                                                                       |
|----------------------------------------------------------------------------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|              <xref:System.Activities.Activity.DisplayName%2A>              |  False   |                                                                                                                                                                                            <xref:System.ServiceModel.Activities.SendReply> アクティビティの省略可能な表示名。 既定値は SendReplyToReceive です。<br /><br /> 既定値以外の <xref:System.Activities.Activity.DisplayName%2A> の使用は必須ではありませんが、使用することをお勧めします。                                                                                                                                                                                             |
|         <xref:System.ServiceModel.Activities.SendReply.Request%2A>         |   True   | この <xref:System.ServiceModel.Activities.Receive> アクティビティと関連付けられる <xref:System.ServiceModel.Activities.SendReply> アクティビティへの参照。 このプロパティは**null**にすることはできません。 <xref:System.ServiceModel.Activities.Receive>アクティビティ<xref:System.ServiceModel.Activities.SendReply>は、要求/応答メッセージング パターンをモデル化するために、サーバー上で一緒に使用されます。 このプロパティでは、関連付ける <xref:System.ServiceModel.Activities.Send> アクティビティを指定します。 このプロパティは、<xref:System.ServiceModel.Activities.Send> アクティビティの作成元である <xref:System.ServiceModel.Activities.SendReply> アクティビティに自動的にバインドされるため、デザイナーでは編集できません。 |
|         <xref:System.ServiceModel.Activities.SendReply.Content%2A>         |  False   |                       受信するメッセージまたはパラメーターの内容を指定します。 <xref:System.ServiceModel.Activities.ReceiveMessageContent> アクティビティまたは <xref:System.ServiceModel.Activities.ReceiveParametersContent> アクティビティを指定できます。 このプロパティを編集するには、プロパティ グリッドの **[コンテンツ]** フィールドの横にある省略記号ボタンをクリックするか、[**定義]を**クリックします。 **[受信**アクティビティ デザイナー] 画面の **[コンテンツ**] ラベルの横にあるボタン。 両方とも **[コンテンツ定義]ダイアログボックス**を表示します。 [!INCLUDE[crabout](../includes/crabout-md.md)]このボックスの使用方法については[、「[コンテンツ定義]ダイアログ ボックス」の](../workflow-designer/content-definition-dialog-box.md)トピックを参照してください。                       |
| <xref:System.ServiceModel.Activities.SendReply.CorrelationInitializers%2A> |  False   |            ワークフロー内のこの <xref:System.ServiceModel.Activities.CorrelationInitializer> アクティビティを構成する複数の <xref:System.ServiceModel.Activities.CorrelationHandle> オブジェクトを初期化する <xref:System.ServiceModel.Activities.Receive> オブジェクトのコレクションを指定します。 プロパティ グリッドで<xref:System.ServiceModel.Activities.SendReply.CorrelationInitializers%2A>プロパティの横にある省略記号ボタンをクリックして、[**相互関係初期化子の追加**] ダイアログ ボックスを開きます。 [!INCLUDE[crabout](../includes/crabout-md.md)]このボックスを使用して、[相関初期化子の追加ダイアログ ボックスのトピックを](../workflow-designer/add-correlationinitializers-dialog-box.md)参照してください。            |
|         <xref:System.ServiceModel.Activities.SendReply.Action%2A>          |  False   |                                                                                                                                                                                                                                              メッセージのアクション ヘッダーを指定します。 これを明示的に設定しない場合は、次の既定値が設定されます。<br /><br /> `https://tempuri.org/{service contract namespace}/{service contract name}/{operation name}`                                                                                                                                                                                                                                              |
|    <xref:System.ServiceModel.Activities.SendReply.PersistBeforeSend%2A>    |  False   |                                                                                                                                                                                                                                                                                          応答メッセージを送信する前にワークフロー サービス インスタンスを永続化するかどうかを指定します。 既定値は **false** です。                                                                                                                                                                                                                                                                                           |

## <a name="see-also"></a>関連項目
 [相関スコープ](../workflow-designer/correlationscope-activity-designer.md)[初期化相関受信](../workflow-designer/initializecorrelation-activity-designer.md)[Receive](../workflow-designer/receive-activity-designer.md)[送信送信](../workflow-designer/send-activity-designer.md)[と受信応答](../workflow-designer/sendandreceivereply-template-designer.md)[トランザクション受信スコープ](../workflow-designer/transactedreceivescope-activity-designer.md)