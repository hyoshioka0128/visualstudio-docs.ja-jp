---
title: '[ワークフローデザイナー-コンテンツ定義] ダイアログボックス'
description: '[コンテンツ定義] ダイアログボックスを使用して、Send、Receive、SendReply、および ReceiveReply の各アクティビティのコンテンツプロパティを構成する方法について説明します。'
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- MessageContent.UI
ms.assetid: 7e4237c3-90a1-4149-bd8a-3643d1dde0df
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2858c179d05645b3e47e6be27e386168392fcb48
ms.sourcegitcommit: ed26b6e313b766c4d92764c303954e2385c6693e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/10/2020
ms.locfileid: "94438166"
---
# <a name="content-definition-dialog-box"></a>[コンテンツ定義] ダイアログ ボックス

[ **コンテンツ定義** ] ダイアログボックスは、、、、およびの各アクティビティの **コンテンツ** プロパティを構成するためにワークフローデザイナーで使用され <xref:System.ServiceModel.Activities.Send> <xref:System.ServiceModel.Activities.Receive> <xref:System.ServiceModel.Activities.SendReply> <xref:System.ServiceModel.Activities.ReceiveReply> ます。 このボックスを使用するアクティビティデザイナーの詳細については、「 [Send](../workflow-designer/send-activity-designer.md)、 [Receive](../workflow-designer/receive-activity-designer.md)、 [Receiveandsendreply](../workflow-designer/receiveandsendreply-template-designer.md)、および [sendandreceivereply](../workflow-designer/sendandreceivereply-template-designer.md) 」のトピックを参照してください。

次の表では、[ **関連付けの初期化** ] ダイアログボックスのユーザーインターフェイス (UI) 要素について説明します。

|UI 要素|説明|
|-|-----------------|
|**メッセージ**|[メッセージの **データ** 式] テキストボックスと、[ **メッセージの種類** ] ドロップダウンリストボックスを使用して、メッセージの内容を指定します。 既定では、 **コンテンツ定義** は、 <xref:System.ServiceModel.Activities.ReceiveMessageContent> <xref:System.ServiceModel.Channels.Message> ワークフローサービス定義内でまたはメッセージコントラクト型を要求するを使用します。|
|**パラメーター**|[ **パラメーター** ] オプションボタンをクリックして <xref:System.ServiceModel.Activities.ReceiveParametersContent> 、データコントラクトを期待するを使用します。 <xref:System.Activities.OutArgument> キーおよび値のペアのジェネリック コレクションを設定するには、データ グリッドを使用します。これらの値は、現在のワークフローの変数パラメーターに割り当てられます。|

[ **コンテンツ定義** ] ダイアログボックスは、 **Send** 、 **Receive** 、 **Receiveandsendreply** 、および **sendandreceivereply** の各デザイナーによって使用されます。 デザイナーへのアクセス方法は、どの場合も同様です。ここでは、Receive デザイナーを使用する例で手順を説明します。

**Receive** アクティビティデザイナーは、[ **ツールボックス** ] からドラッグして、アクティビティを通常配置している任意の場所のワークフローデザイナー画面にドロップできます。 この操作により、Receive という既定の <xref:System.ServiceModel.Activities.Receive> を持つ <xref:System.Activities.Activity.DisplayName%2A> アクティビティが作成されます。 **Receive** アクティビティデザイナーを選択し、[コンテンツ **定義** ] ダイアログボックスが表示されるプロパティグリッドで、 **コンテンツ** プロパティの (コンテンツ) テキストの横にある省略記号ボタンをクリックします。

コンテンツは、アクティビティの **Message** セクション内で指定することも、 <xref:System.ServiceModel.Activities.ReceiveMessageContent> アクティビティの **Parameter** セクション内で指定することもでき <xref:System.ServiceModel.Activities.ReceiveParametersContent> ます。

## <a name="see-also"></a>関連項目

- [ワークフロー デザイナーの UI ヘルプ](browse-and-select-a-dotnet-type-dialog-box.md)