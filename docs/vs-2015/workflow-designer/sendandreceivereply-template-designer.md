---
title: SendAndReceiveReply テンプレートデザイナー |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80395335"
---
# <a name="sendandreceivereply-template-designer"></a>SendAndReceiveReply テンプレート デザイナー
**Sendandreceivereply**テンプレートは、 <xref:System.ServiceModel.Activities.Send> <xref:System.ServiceModel.Activities.ReceiveReply> <xref:System.Activities.Statements.Sequence> クライアントでの要求/応答メッセージ交換パターンの一部として関連付けられているアクティビティ内に、事前構成されたアクティビティとアクティビティのペアを作成するために使用されます。

## <a name="the-sendandreceivereply-template"></a>SendAndReceiveReply テンプレート
 **Sendandreceivereply**テンプレートを追加すると、アクティビティ内にアクティビティとアクティビティを作成する以外に、次の3つの処理が行われ <xref:System.ServiceModel.Activities.Send> <xref:System.ServiceModel.Activities.ReceiveReply> <xref:System.Activities.Statements.Sequence> ます。

1. <xref:System.ServiceModel.Activities.Send.OperationName%2A> アクティビティの <xref:System.ServiceModel.Activities.Send.ServiceContractName%2A> プロパティと <xref:System.ServiceModel.Activities.Send> プロパティを構成する。

2. <xref:System.ServiceModel.Activities.ReceiveReply.Request%2A> アクティビティの <xref:System.ServiceModel.Activities.ReceiveReply> プロパティを <xref:System.ServiceModel.Activities.Send> アクティビティにバインドする。

3. 親アクティビティに、変数として <xref:System.ServiceModel.Activities.CorrelationHandle> を作成する。

### <a name="using-the-sendandreceivereply-template-designer"></a>SendAndReceiveReply テンプレート デザイナーの使用
 **Sendandreceivereply**アクティビティデザイナーは、**ツールボックス**の [**メッセージング**] カテゴリにあります。これにアクセスするには、の [**ツールボックス**] タブをクリックします [!INCLUDE[wfd2](../includes/wfd2-md.md)] (または、[**表示**] メニューの [**ツールバー** ] を選択するか、CTRL + ALT + X キーを押します)。

 **Sendandreceivereply**アクティビティデザイナーは、[**ツールボックス**] からドラッグして、 [!INCLUDE[wfd2](../includes/wfd2-md.md)] アクティビティを通常配置している画面の任意の場所にドロップできます。 これにより、 <xref:System.ServiceModel.Activities.Send> **send** アクティビティデザイナーで構成できるアクティビティと、 <xref:System.ServiceModel.Activities.ReceiveReply> **receivereplyforsend** デザイナーで構成できる相関が作成されます。

 [!INCLUDE[crabout](../includes/crabout-md.md)]**送信**デザイナーを使用してアクティビティを構成する方法 <xref:System.ServiceModel.Activities.Send> については、「 [」を](../workflow-designer/send-activity-designer.md)参照してください。

 [!INCLUDE[crabout](../includes/crabout-md.md)]**Receivereplyforsend**デザイナーを使用してアクティビティを構成する方法 <xref:System.ServiceModel.Activities.ReceiveReply> については、次のセクションを参照してください。

### <a name="properties-of-receivereply"></a>ReceiveReply のプロパティ
 次の表に、<xref:System.ServiceModel.Activities.ReceiveReply> のプロパティと、デザイナーでのその使用方法を示します。 これらのプロパティは、プロパティ グリッドで編集できます。また、その一部は[!INCLUDE[wfd2](../includes/wfd2-md.md)]のデザイナー画面で編集できます。

|                                 プロパティ名                                 | 必須 |                                                                                                                                                                                                                                                                                                                                                        使用法                                                                                                                                                                                                                                                                                                                                                        |
|-------------------------------------------------------------------------------|----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|               <xref:System.Activities.Activity.DisplayName%2A>                |  ×   |                                                                                                                                                                                            <xref:System.ServiceModel.Activities.ReceiveReply> アクティビティの省略可能な表示名。 既定値は、ReceiveReplyForSend です。<br /><br /> 既定値以外の <xref:System.Activities.Activity.DisplayName%2A> の使用は必須ではありませんが、使用することをお勧めします。                                                                                                                                                                                            |
|         <xref:System.ServiceModel.Activities.ReceiveReply.Request%2A>         |   True   | この <xref:System.ServiceModel.Activities.Send> アクティビティと関連付けられる <xref:System.ServiceModel.Activities.ReceiveReply> アクティビティへの参照。 このプロパティを **null**にすることはできません。 <xref:System.ServiceModel.Activities.Send> と <xref:System.ServiceModel.Activities.ReceiveReply> アクティビティは、要求/応答のメッセージングパターンをモデル化するために、クライアントで一緒に使用されます。 このプロパティでは、関連付ける <xref:System.ServiceModel.Activities.Send> アクティビティを指定します。 このプロパティは、<xref:System.ServiceModel.Activities.Send> アクティビティの作成元である <xref:System.ServiceModel.Activities.ReceiveReply> アクティビティに自動的にバインドされるため、デザイナーでは編集できません。 |
|         <xref:System.ServiceModel.Activities.ReceiveReply.Content%2A>         |  ×   |                        受信するメッセージまたはパラメーターの内容を指定します。 <xref:System.ServiceModel.Activities.ReceiveMessageContent> アクティビティまたは <xref:System.ServiceModel.Activities.ReceiveParametersContent> アクティビティを指定できます。 このプロパティを編集するには、プロパティグリッドで**コンテンツ**フィールドの横にある省略記号ボタンをクリックするか、[**定義...** ] をクリックします。 **Receive**アクティビティデザイナー画面の**コンテンツ**ラベルの横にあるボタン。 どちらの場合も、[ **コンテンツ定義** ] ダイアログボックスが表示されます。 [!INCLUDE[crabout](../includes/crabout-md.md)] このボックスの使用方法については、「[ [コンテンツ定義] ダイアログボックス](../workflow-designer/content-definition-dialog-box.md) 」を参照してください。                         |
| <xref:System.ServiceModel.Activities.ReceiveReply.CorrelationInitializers%2A> |  ×   |              ワークフロー内のこの <xref:System.ServiceModel.Activities.CorrelationInitializer> アクティビティを構成する複数の <xref:System.ServiceModel.Activities.CorrelationHandle> オブジェクトを初期化する <xref:System.ServiceModel.Activities.Receive> オブジェクトのコレクションを指定します。 プロパティグリッドでプロパティの横にある省略記号ボタンをクリックして <xref:System.ServiceModel.Activities.Receive.CorrelationInitializers%2A> 、[ **関連付け初期化子の追加** ] ダイアログボックスを開きます。 [!INCLUDE[crabout](../includes/crabout-md.md)] このボックスの使用方法については、「[ [CorrelationInitializers の追加] ダイアログボックス](../workflow-designer/add-correlationinitializers-dialog-box.md) 」を参照してください。               |
|         <xref:System.ServiceModel.Activities.ReceiveReply.Action%2A>          |  ×   |                                                                                                                                                                                                                                               メッセージのアクション ヘッダーを指定します。 これを明示的に設定しない場合は、次の既定値が設定されます。<br /><br /> `https://tempuri.org/{service contract namespace}/{service contract name}/{operation name}`.                                                                                                                                                                                                                                              |

## <a name="see-also"></a>参照
 [Correlationscope](../workflow-designer/correlationscope-activity-designer.md) [InitializeCorrelation](../workflow-designer/initializecorrelation-activity-designer.md) [Receive](../workflow-designer/receive-activity-designer.md) [receiveandsendreply](../workflow-designer/receiveandsendreply-template-designer.md) [Send](../workflow-designer/send-activity-designer.md) [TransactedReceiveScope](../workflow-designer/transactedreceivescope-activity-designer.md)