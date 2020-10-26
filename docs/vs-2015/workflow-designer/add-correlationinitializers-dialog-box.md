---
title: '[CorrelationInitializers の追加] ダイアログボックス |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- AddCorrelationInitializers.UI
ms.assetid: c0517467-d54a-4ee6-aef0-c19b96b6f395
caps.latest.revision: 5
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: e1402b90dfc78068546b510ce6b85379b1695f47
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72672037"
---
# <a name="add-correlationinitializers-dialog-box"></a>[関連付け初期化子の追加] ダイアログ ボックス
[ **関連付け初期化子の追加** ] ダイアログボックスは、、、 [!INCLUDE[wfd1](../includes/wfd1-md.md)] 、およびアクティビティの **correlationinitializers** プロパティを構成するために、で使用され <xref:System.ServiceModel.Activities.Send> <xref:System.ServiceModel.Activities.Receive> <xref:System.ServiceModel.Activities.SendReply> <xref:System.ServiceModel.Activities.ReceiveReply> ます。 [!INCLUDE[crabout](../includes/crabout-md.md)] このボックスを使用するアクティビティデザイナーについては、「 [Send](../workflow-designer/send-activity-designer.md)、 [Receive](../workflow-designer/receive-activity-designer.md)、 [Receiveandsendreply](../workflow-designer/receiveandsendreply-template-designer.md)、および [sendandreceivereply](../workflow-designer/sendandreceivereply-template-designer.md) の各トピック」を参照してください。

 このダイアログ ボックスで指定したコレクションの関連付け初期化子では、メッセージング アクティビティ間の相関関係 (クエリベース、コンテキスト、コールバック コンテキスト、または要求/応答の相関関係) を初期化できます。

 次の表では、[ **関連付け初期化子の追加** ] ダイアログボックスのユーザーインターフェイス (UI) 要素について説明します。

|UI 要素|説明|
|----------------|-----------------|
|**初期化子の追加**|[ **初期化の追加** ] ボックスをクリックして、追加の初期化子をコレクションに追加します。|
|**[関連付けの種類]**|関連付け初期化子の種類を指定します。 次の 4 種類から選択できます。<br /><br /> 1. を指定するコールバック関連付け初期化子 <xref:System.ServiceModel.Activities.CallbackCorrelationInitializer> 。<br />2. を指定するコンテキスト関連付け初期化子 <xref:System.ServiceModel.Activities.CorrelationInitializer> 。<br />3. を指定するための要求と応答の関連付け初期化子 <xref:System.ServiceModel.Activities.RequestReplyCorrelationInitializer> 。<br />4. を指定するためのクエリ関連付け初期化子 <xref:System.ServiceModel.Activities.QueryCorrelationInitializer> 。<br /><br /> **Correlationtype**を編集するには<br /><br /> 1. [ **初期化子の追加** ] DataGrid の特定の行にタブを追加します。<br />2. Ctrl + Tab キーを押して、 **Correlationtypecombobox**にフォーカスを設定します<br />3. Alt + ↓キーを押して、 **コンボボックス** をポップアップ表示して編集します。|
|**XPath クエリ**|送受信メッセージから相関関係データを抽出するためのクエリを含む、キーと値のペア。 このリストは、<xref:System.ServiceModel.Activities.QueryCorrelationInitializer> 型を使用している場合にのみ有効です。|

## <a name="to-launch-the-add-correlation-initializers-dialog-box"></a>[関連付け初期化子の追加] ダイアログ ボックスを開くには
 [ **関連付け初期化子の追加** ] ダイアログボックスは、 **Send**、 **Receive**、 **Receiveandsendreply**、および **sendandreceivereply** の各デザイナーによって使用されます。 これらのアクセスは、各ケースで類似しています。また、 **受信** デザイナーに関連するケースでは、この手順を説明するために使用します。

 **Receive**アクティビティデザイナーは、[**ツールボックス**] からドラッグして、 [!INCLUDE[wfd2](../includes/wfd2-md.md)] アクティビティを通常配置している画面の任意の場所にドロップできます。 この操作により、Receive という既定の <xref:System.ServiceModel.Activities.Receive> を持つ <xref:System.Activities.Activity.DisplayName%2A> アクティビティが作成されます。 **Receive**アクティビティデザイナーを選択し、[**関連付け初期化子の追加**] ダイアログボックスのプロパティグリッドで、 **Correlationinitializers**プロパティの (コレクション) テキストの横にある省略記号ボタンをクリックします。

## <a name="see-also"></a>参照
 [[関連付け初期化] ダイアログ ボックス](../workflow-designer/initialize-correlation-dialog-box.md)