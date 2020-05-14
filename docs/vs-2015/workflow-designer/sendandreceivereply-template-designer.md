---
title: 送信送受信返信テンプレート デザイナー |マイクロソフトドキュメント
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.ServiceModel.Activities.SendAndReceiveReply.UI
- System.ServiceModel.Activities.ReceiveReply.UI
ms.assetid: 818a8c84-6593-416d-b016-1d91b85ffb68
caps.latest.revision: 6
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 1bfe43f410709a924b0ebdb0cf6afbb8d30a8fcf
ms.sourcegitcommit: d6828e7422c8d74ec1e99146fedf0a05f757245f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/30/2020
ms.locfileid: "80395335"
---
# <a name="sendandreceivereply-template-designer"></a>SendAndReceiveReply テンプレート デザイナー
**SendAndReceiveReply**テンプレートは、クライアント上の要求/応答メッセージ交換<xref:System.ServiceModel.Activities.Send>パターン<xref:System.ServiceModel.Activities.ReceiveReply>の一部<xref:System.Activities.Statements.Sequence>として関連付けられているアクティビティ内で構成済みのアクティビティとアクティビティのペアを作成するために使用されます。

## <a name="the-sendandreceivereply-template"></a>SendAndReceiveReply テンプレート
 **SendAndReceiveReply**テンプレートを追加すると、アクティビティ内<xref:System.ServiceModel.Activities.Send>で<xref:System.ServiceModel.Activities.ReceiveReply>と<xref:System.Activities.Statements.Sequence>アクティビティを作成する以外に、次の 3 つの処理が行われます。

1. <xref:System.ServiceModel.Activities.Send.OperationName%2A> アクティビティの <xref:System.ServiceModel.Activities.Send.ServiceContractName%2A> プロパティと <xref:System.ServiceModel.Activities.Send> プロパティを構成する。

2. <xref:System.ServiceModel.Activities.ReceiveReply.Request%2A> アクティビティの <xref:System.ServiceModel.Activities.ReceiveReply> プロパティを <xref:System.ServiceModel.Activities.Send> アクティビティにバインドする。

3. 親アクティビティに、変数として <xref:System.ServiceModel.Activities.CorrelationHandle> を作成する。

### <a name="using-the-sendandreceivereply-template-designer"></a>SendAndReceiveReply テンプレート デザイナーの使用
 **SendAndReceiveReply**アクティビティ デザイナーは、**ツールボックス**の [**View****Toolbox****メッセージング**] カテゴリにあります。 **Toolbar** [!INCLUDE[wfd2](../includes/wfd2-md.md)]

 **SendAndReceiveReply**アクティビティ デザイナーは **、ツールボックス**からドラッグして、通常はアクティビティ[!INCLUDE[wfd2](../includes/wfd2-md.md)]が配置されている場所にドロップできます。 これにより<xref:System.ServiceModel.Activities.Send>**、Send**アクティビティ デザイナーで構成できるアクティビティと<xref:System.ServiceModel.Activities.ReceiveReply>**、ReceiveReplyForSend**デザイナーで構成できる関連付けが作成されます。

 [!INCLUDE[crabout](../includes/crabout-md.md)]**Send**デザイナーを使用してアクティビティ<xref:System.ServiceModel.Activities.Send>を構成するには、「[送信](../workflow-designer/send-activity-designer.md)」トピックを参照してください。

 [!INCLUDE[crabout](../includes/crabout-md.md)]アクティビティを構成するには **、次**の<xref:System.ServiceModel.Activities.ReceiveReply>セクションを参照してください。

### <a name="properties-of-receivereply"></a>ReceiveReply のプロパティ
 次の表に、<xref:System.ServiceModel.Activities.ReceiveReply> のプロパティと、デザイナーでのその使用方法を示します。 これらのプロパティは、プロパティ グリッドで編集できます。また、その一部は[!INCLUDE[wfd2](../includes/wfd2-md.md)]のデザイナー画面で編集できます。

|                                 プロパティ名                                 | 必須 |                                                                                                                                                                                                                                                                                                                                                        使用法                                                                                                                                                                                                                                                                                                                                                        |
|-------------------------------------------------------------------------------|----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|               <xref:System.Activities.Activity.DisplayName%2A>                |  False   |                                                                                                                                                                                            <xref:System.ServiceModel.Activities.ReceiveReply> アクティビティの省略可能な表示名。 既定値は、ReceiveReplyForSend です。<br /><br /> 既定値以外の <xref:System.Activities.Activity.DisplayName%2A> の使用は必須ではありませんが、使用することをお勧めします。                                                                                                                                                                                            |
|         <xref:System.ServiceModel.Activities.ReceiveReply.Request%2A>         |   True   | この <xref:System.ServiceModel.Activities.Send> アクティビティと関連付けられる <xref:System.ServiceModel.Activities.ReceiveReply> アクティビティへの参照。 このプロパティは**null**にすることはできません。 <xref:System.ServiceModel.Activities.Send>と<xref:System.ServiceModel.Activities.ReceiveReply>アクティビティは、要求/応答メッセージング パターンをモデル化するためにクライアント上で一緒に使用されます。 このプロパティでは、関連付ける <xref:System.ServiceModel.Activities.Send> アクティビティを指定します。 このプロパティは、<xref:System.ServiceModel.Activities.Send> アクティビティの作成元である <xref:System.ServiceModel.Activities.ReceiveReply> アクティビティに自動的にバインドされるため、デザイナーでは編集できません。 |
|         <xref:System.ServiceModel.Activities.ReceiveReply.Content%2A>         |  False   |                        受信するメッセージまたはパラメーターの内容を指定します。 <xref:System.ServiceModel.Activities.ReceiveMessageContent> アクティビティまたは <xref:System.ServiceModel.Activities.ReceiveParametersContent> アクティビティを指定できます。 このプロパティを編集するには、プロパティ グリッドの **[コンテンツ]** フィールドの横にある省略記号ボタンをクリックするか、[**定義]を**クリックします。 **[受信**アクティビティ デザイナー] 画面の **[コンテンツ**] ラベルの横にあるボタン。 両方とも **[コンテンツ定義]ダイアログボックス**を表示します。 [!INCLUDE[crabout](../includes/crabout-md.md)]このボックスの使用方法については[、「[コンテンツ定義]ダイアログ ボックス」の](../workflow-designer/content-definition-dialog-box.md)トピックを参照してください。                         |
| <xref:System.ServiceModel.Activities.ReceiveReply.CorrelationInitializers%2A> |  False   |              ワークフロー内のこの <xref:System.ServiceModel.Activities.CorrelationInitializer> アクティビティを構成する複数の <xref:System.ServiceModel.Activities.CorrelationHandle> オブジェクトを初期化する <xref:System.ServiceModel.Activities.Receive> オブジェクトのコレクションを指定します。 プロパティ グリッドで<xref:System.ServiceModel.Activities.Receive.CorrelationInitializers%2A>プロパティの横にある省略記号ボタンをクリックして、[**相互関係初期化子の追加**] ダイアログ ボックスを開きます。 [!INCLUDE[crabout](../includes/crabout-md.md)]このボックスを使用して、[相関初期化子の追加ダイアログ ボックスのトピックを](../workflow-designer/add-correlationinitializers-dialog-box.md)参照してください。               |
|         <xref:System.ServiceModel.Activities.ReceiveReply.Action%2A>          |  False   |                                                                                                                                                                                                                                               メッセージのアクション ヘッダーを指定します。 これを明示的に設定しない場合は、次の既定値が設定されます。<br /><br /> `https://tempuri.org/{service contract namespace}/{service contract name}/{operation name}`.                                                                                                                                                                                                                                              |

## <a name="see-also"></a>関連項目
 [相関スコープ](../workflow-designer/correlationscope-activity-designer.md)[初期化相関受信](../workflow-designer/initializecorrelation-activity-designer.md)[受信](../workflow-designer/receive-activity-designer.md)[と送信応答](../workflow-designer/receiveandsendreply-template-designer.md)[送信](../workflow-designer/send-activity-designer.md)[トランザクション受信スコープ](../workflow-designer/transactedreceivescope-activity-designer.md)