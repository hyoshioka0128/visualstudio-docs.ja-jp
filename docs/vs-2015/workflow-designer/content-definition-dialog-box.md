---
title: '[コンテンツ定義] ダイアログボックス |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- MessageContent.UI
ms.assetid: 7e4237c3-90a1-4149-bd8a-3643d1dde0df
caps.latest.revision: 3
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: d989f5a0c57e381041e8fe9c200aae1a76316ad8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72656960"
---
# <a name="content-definition-dialog-box"></a>[コンテンツ定義] ダイアログ ボックス
[ **コンテンツ定義** ] ダイアログボックスは、、、 [!INCLUDE[wfd1](../includes/wfd1-md.md)] 、およびの各アクティビティの **コンテンツ** プロパティを構成するために、で使用され <xref:System.ServiceModel.Activities.Send> <xref:System.ServiceModel.Activities.Receive> <xref:System.ServiceModel.Activities.SendReply> <xref:System.ServiceModel.Activities.ReceiveReply> ます。 [!INCLUDE[crabout](../includes/crabout-md.md)] このボックスを使用するアクティビティデザイナーについては、「 [Send](../workflow-designer/send-activity-designer.md)、 [Receive](../workflow-designer/receive-activity-designer.md)、 [Receiveandsendreply](../workflow-designer/receiveandsendreply-template-designer.md)、および [sendandreceivereply](../workflow-designer/sendandreceivereply-template-designer.md) の各トピック」を参照してください。

 次の表では、[ **関連付けの初期化** ] ダイアログボックスのユーザーインターフェイス (UI) 要素について説明します。

|UI 要素|説明|
|----------------|-----------------|
|**メッセージ**|[メッセージの **データ** 式] テキストボックスと、[ **メッセージの種類** ] ドロップダウンリストボックスを使用して、メッセージの内容を指定します。 既定では、 **コンテンツ定義** は、 <xref:System.ServiceModel.Activities.ReceiveMessageContent> <xref:System.ServiceModel.Channels.Message> ワークフローサービス定義内でまたはメッセージコントラクト型を要求するを使用します。|
|**パラメーター**|[ **パラメーター** ] オプションボタンをクリックして <xref:System.ServiceModel.Activities.ReceiveParametersContent> 、データコントラクトを期待するを使用します。 <xref:System.Activities.OutArgument> キーおよび値のペアのジェネリック コレクションを設定するには、データ グリッドを使用します。これらの値は、現在のワークフローの変数パラメーターに割り当てられます。|

 [ **コンテンツ定義** ] ダイアログボックスは、 **Send**、 **Receive**、 **Receiveandsendreply**、および **sendandreceivereply** の各デザイナーによって使用されます。 デザイナーへのアクセス方法は、どの場合も同様です。ここでは、Receive デザイナーを使用する例で手順を説明します。

 **Receive**アクティビティデザイナーは、[**ツールボックス**] からドラッグして、 [!INCLUDE[wfd2](../includes/wfd2-md.md)] アクティビティを通常配置している画面の任意の場所にドロップできます。 この操作により、Receive という既定の <xref:System.ServiceModel.Activities.Receive> を持つ <xref:System.Activities.Activity.DisplayName%2A> アクティビティが作成されます。 **Receive**アクティビティデザイナーを選択し、[コンテンツ**定義**] ダイアログボックスが表示されるプロパティグリッドで、**コンテンツ**プロパティの (コンテンツ) テキストの横にある省略記号ボタンをクリックします。

 コンテンツは、アクティビティの **Message** セクション内で指定することも、 <xref:System.ServiceModel.Activities.ReceiveMessageContent> アクティビティの **Parameter** セクション内で指定することもでき <xref:System.ServiceModel.Activities.ReceiveParametersContent> ます。

## <a name="see-also"></a>参照
 [ワークフロー デザイナーの UI ヘルプ](../workflow-designer/workflow-designer-ui-help.md)