---
title: ReceiveAndSendReply テンプレートデザイナー |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80395386"
---
# <a name="receiveandsendreply-template-designer"></a>ReceiveAndSendReply テンプレート デザイナー
**Receiveandsendreply**テンプレートは、 <xref:System.ServiceModel.Activities.Receive> <xref:System.ServiceModel.Activities.SendReply> <xref:System.Activities.Statements.Sequence> サーバー上で要求/応答メッセージ交換パターンの一部として関連付けられているアクティビティ内に、事前構成済みのアクティビティとアクティビティのペアを作成するために使用されます。

## <a name="the-receiveandsendreply-template"></a>ReceiveAndSendReply テンプレート
 **Receiveandsendreply**テンプレートを追加すると、アクティビティを含むアクティビティとアクティビティを作成する以外に、次の3つの処理が行われ <xref:System.ServiceModel.Activities.Receive> <xref:System.ServiceModel.Activities.SendReply> <xref:System.Activities.Statements.Sequence> ます。

1. <xref:System.ServiceModel.Activities.Receive.OperationName%2A> アクティビティの <xref:System.ServiceModel.Activities.Receive.ServiceContractName%2A> プロパティと <xref:System.ServiceModel.Activities.Receive> プロパティを構成する。

2. <xref:System.ServiceModel.Activities.SendReply.Request%2A> アクティビティの <xref:System.ServiceModel.Activities.Receive> プロパティを <xref:System.ServiceModel.Activities.Send> アクティビティにバインドする。

3. 親アクティビティに、変数として <xref:System.ServiceModel.Activities.CorrelationHandle> を作成する。

### <a name="using-the-receiveandsendreply-template-designer"></a>ReceiveAndSendReply テンプレート デザイナーの使用
 **Receiveandsendreply**アクティビティデザイナーは、 **[ツールボックス**] の [**メッセージング**] カテゴリにあります。これにアクセスするには、の [**ツールボックス**] タブをクリックします [!INCLUDE[wfd2](../includes/wfd2-md.md)] (または、[**表示**] メニューの [**ツールバー** ] を選択するか、CTRL + ALT + X キーを押します)。

 **Receiveandsendreply**アクティビティデザイナーは、[**ツールボックス**] からドラッグして、 [!INCLUDE[wfd2](../includes/wfd2-md.md)] アクティビティを通常配置している画面の任意の場所にドロップできます。 これにより、 <xref:System.ServiceModel.Activities.Receive> **Send** アクティビティデザイナーで構成できるアクティビティと、 <xref:System.ServiceModel.Activities.SendReply> SendReplyToReceive デザイナーで構成できる相関が作成されます。

 [!INCLUDE[crabout](../includes/crabout-md.md)]**receive** designer を使用してアクティビティを構成する方法 <xref:System.ServiceModel.Activities.Receive> について[は、](../workflow-designer/receive-activity-designer.md) 「」を参照してください。

 [!INCLUDE[crabout](../includes/crabout-md.md)]**SendReplyToReceive**デザイナーを使用してアクティビティを構成する方法 <xref:System.ServiceModel.Activities.SendReply> については、次のセクションを参照してください。

### <a name="properties-of-sendreply"></a>SendReply のプロパティ
 次の表に、<xref:System.ServiceModel.Activities.SendReply> のプロパティと、デザイナーでのその使用方法を示します。 これらのプロパティは、プロパティ グリッドで編集できます。また、その一部は[!INCLUDE[wfd2](../includes/wfd2-md.md)]のデザイナー画面で編集できます。

|                               プロパティ名                                | 必須 |                                                                                                                                                                                                                                                                                                                                                      使用法                                                                                                                                                                                                                                                                                                                                                       |
|----------------------------------------------------------------------------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|              <xref:System.Activities.Activity.DisplayName%2A>              |  ×   |                                                                                                                                                                                            <xref:System.ServiceModel.Activities.SendReply> アクティビティの省略可能な表示名。 既定値は SendReplyToReceive です。<br /><br /> 既定値以外の <xref:System.Activities.Activity.DisplayName%2A> の使用は必須ではありませんが、使用することをお勧めします。                                                                                                                                                                                             |
|         <xref:System.ServiceModel.Activities.SendReply.Request%2A>         |   ○   | この <xref:System.ServiceModel.Activities.Receive> アクティビティと関連付けられる <xref:System.ServiceModel.Activities.SendReply> アクティビティへの参照。 このプロパティを **null**にすることはできません。 <xref:System.ServiceModel.Activities.Receive> と <xref:System.ServiceModel.Activities.SendReply> アクティビティは、要求/応答メッセージングパターンをモデル化するために、サーバー上で一緒に使用されます。 このプロパティでは、関連付ける <xref:System.ServiceModel.Activities.Send> アクティビティを指定します。 このプロパティは、<xref:System.ServiceModel.Activities.Send> アクティビティの作成元である <xref:System.ServiceModel.Activities.SendReply> アクティビティに自動的にバインドされるため、デザイナーでは編集できません。 |
|         <xref:System.ServiceModel.Activities.SendReply.Content%2A>         |  ×   |                       受信するメッセージまたはパラメーターの内容を指定します。 <xref:System.ServiceModel.Activities.ReceiveMessageContent> アクティビティまたは <xref:System.ServiceModel.Activities.ReceiveParametersContent> アクティビティを指定できます。 このプロパティを編集するには、プロパティグリッドで**コンテンツ**フィールドの横にある省略記号ボタンをクリックするか、[**定義...** ] をクリックします。 **Receive**アクティビティデザイナー画面の**コンテンツ**ラベルの横にあるボタン。 どちらの場合も、[ **コンテンツ定義** ] ダイアログボックスが表示されます。 [!INCLUDE[crabout](../includes/crabout-md.md)] このボックスの使用方法については、「[ [コンテンツ定義] ダイアログボックス](../workflow-designer/content-definition-dialog-box.md) 」を参照してください。                       |
| <xref:System.ServiceModel.Activities.SendReply.CorrelationInitializers%2A> |  ×   |            ワークフロー内のこの <xref:System.ServiceModel.Activities.CorrelationInitializer> アクティビティを構成する複数の <xref:System.ServiceModel.Activities.CorrelationHandle> オブジェクトを初期化する <xref:System.ServiceModel.Activities.Receive> オブジェクトのコレクションを指定します。 プロパティグリッドでプロパティの横にある省略記号ボタンをクリックして <xref:System.ServiceModel.Activities.SendReply.CorrelationInitializers%2A> 、[ **関連付け初期化子の追加** ] ダイアログボックスを開きます。 [!INCLUDE[crabout](../includes/crabout-md.md)] このボックスの使用方法については、「[ [CorrelationInitializers の追加] ダイアログボックス](../workflow-designer/add-correlationinitializers-dialog-box.md) 」を参照してください。            |
|         <xref:System.ServiceModel.Activities.SendReply.Action%2A>          |  ×   |                                                                                                                                                                                                                                              メッセージのアクション ヘッダーを指定します。 これを明示的に設定しない場合は、次の既定値が設定されます。<br /><br /> `https://tempuri.org/{service contract namespace}/{service contract name}/{operation name}`                                                                                                                                                                                                                                              |
|    <xref:System.ServiceModel.Activities.SendReply.PersistBeforeSend%2A>    |  ×   |                                                                                                                                                                                                                                                                                          応答メッセージを送信する前にワークフロー サービス インスタンスを永続化するかどうかを指定します。 既定値は **false** です。                                                                                                                                                                                                                                                                                           |

## <a name="see-also"></a>参照
 [Correlationscope](../workflow-designer/correlationscope-activity-designer.md) [InitializeCorrelation](../workflow-designer/initializecorrelation-activity-designer.md) [Receive](../workflow-designer/receive-activity-designer.md) [Send](../workflow-designer/send-activity-designer.md) [sendandreceivereply](../workflow-designer/sendandreceivereply-template-designer.md) [TransactedReceiveScope](../workflow-designer/transactedreceivescope-activity-designer.md)