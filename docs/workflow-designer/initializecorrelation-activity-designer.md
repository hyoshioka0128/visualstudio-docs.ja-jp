---
title: ワークフローデザイナー InitializeCorrelation アクティビティデザイナー
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.ServiceModel.Activities.InitializeCorrelation.UI
ms.assetid: 4c54f34c-ee84-42a6-abb0-ec260c1ccb76
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: aadb526e50351c8344c8b265dca3364637d1ff0c
ms.sourcegitcommit: 186c0c250d85ac74274fa1e438b4c7c7108d8a36
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/22/2020
ms.locfileid: "86875567"
---
# <a name="initializecorrelation-activity-designer"></a>InitializeCorrelation アクティビティ デザイナー

**InitializeCorrelation**アクティビティデザイナーは、アクティビティを作成および構成するために使用され <xref:System.ServiceModel.Activities.InitializeCorrelation> ます。 アクティビティは、 <xref:System.ServiceModel.Activities.InitializeCorrelation> メッセージを送信または受信する前に、メッセージ間の相関関係を確立します。

## <a name="the-initializecorrelation-activity"></a>InitializeCorrelation アクティビティ

<xref:System.ServiceModel.Activities.InitializeCorrelation> アクティビティを使用すると、メッセージが送受信されずに関連付けが初期化されます。 通常、関連付けはメッセージを送受信するときに初期化されます。 メッセージを送受信する前に関連付けを確立する必要がある場合は、<xref:System.ServiceModel.Activities.InitializeCorrelation> を使用して関連付けを初期化できます。

### <a name="using-the-initializecorrelation-activity-designer"></a>InitializeCorrelation アクティビティ デザイナーの使用

**ツールボックス**の [**メッセージング**] カテゴリの**InitializeCorrelation**アクティビティデザイナーにアクセスします。

**InitializeCorrelation**アクティビティデザイナーは、[**ツールボックス**] からドラッグしてワークフローデザイナー画面にドロップできます。 アクティビティデザイナーを削除する <xref:System.ServiceModel.Activities.InitializeCorrelation> と、既定値の InitializeCorrelation を持つアクティビティが作成さ <xref:System.Activities.Activity.DisplayName%2A> れます。 は、 <xref:System.Activities.Activity.DisplayName%2A> **InitializeCorrelation**アクティビティデザイナーのヘッダー、または [**プロパティ**] ウィンドウの [ **DisplayName** ] ボックスで編集できます。

は、 <xref:System.ServiceModel.Activities.CorrelationHandle> **InitializeCorrelation**アクティビティデザイナー画面の [**プロパティ**] ウィンドウの [**関連付け**] フィールドで指定できます。

関連付けハンドルとその初期化に使用されるキーと値のペアを指定できる [**関連付けの初期化**] ダイアログボックスを表示するには、[**プロパティ**] ウィンドウの [ **correlationdata** ] フィールドの横にある省略記号ボタンを選択します。 または、[表示...] を選択します。**InitializeCorrelation**アクティビティデザイナー画面にヒントテキストを入力します。 このダイアログボックスの使用方法の詳細については、「[[型コレクションエディター] ダイアログボックス](../workflow-designer/type-collection-editor-dialog-box.md)」を参照してください。

### <a name="the-initializecorrelation-properties"></a>InitializeCorrelation プロパティ

次の表は、 <xref:System.ServiceModel.Activities.InitializeCorrelation> プロパティと、デザイナーでのそれらの使用方法を示しています。 これらのプロパティは、[**プロパティ**] ウィンドウまたはワークフローデザイナー画面で編集できます。

|プロパティ名|必須|使用|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|誤り|<xref:System.ServiceModel.Activities.InitializeCorrelation> アクティビティの表示名。 既定値は InitializeCorrelation です。<br /><br /> フレンドリに既定値以外の値を使用することは、厳密には <xref:System.Activities.Activity.DisplayName%2A> 必須ではありませんが、推奨されます。|
|<xref:System.ServiceModel.Activities.InitializeCorrelation.Correlation%2A>|誤り|関連付け内のワークフロー アクティビティを関連付けるために使用される <xref:System.ServiceModel.Activities.CorrelationHandle>。|
|<xref:System.ServiceModel.Activities.InitializeCorrelation.CorrelationData%2A>|誤り|メッセージをワークフロー インスタンスに関連付ける、関連付けデータのディクショナリ。<br /><br /> を構成するには、[**関連付けの初期化**] ダイアログボックスを使用し <xref:System.ServiceModel.Activities.InitializeCorrelation.CorrelationData%2A> ます。 このダイアログボックスを使用する方法の詳細については、「[[型コレクションエディター] ダイアログボックス](../workflow-designer/type-collection-editor-dialog-box.md)」を参照してください。|

## <a name="see-also"></a>こちらもご覧ください

- [CorrelationScope](../workflow-designer/correlationscope-activity-designer.md)
- [受け取れ](../workflow-designer/receive-activity-designer.md)
- [ReceiveAndSendReply](../workflow-designer/receiveandsendreply-template-designer.md)
- [送信](../workflow-designer/send-activity-designer.md)
- [SendAndReceiveReply](../workflow-designer/sendandreceivereply-template-designer.md)
- [TransactedReceiveScope](../workflow-designer/transactedreceivescope-activity-designer.md)