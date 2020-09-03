---
title: ワークフローデザイナー-Flowchart アクティビティデザイナー
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Flowchart.UI
- System.Activities.Statements.FlowStep.UI
- System.Activities.Core.Presentation.FlowStart.UI
ms.assetid: d5af2276-5215-4138-880a-cf2b90bbf3a0
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d786e9acfa99d2b106b72822a0106e2161724790
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "75597036"
---
# <a name="flowchart-activity-designer"></a>フローチャート アクティビティ デザイナー

<xref:System.Activities.Statements.Flowchart> アクティビティは、複雑なフロー制御を定義および管理するワークフローを作成するために使用します。 は、 <xref:System.Activities.Statements.Flowchart> コードまたはワークフローデザイナーを使用して作成できます。 このトピックでは、ワークフローデザイナーのエクスペリエンスについて説明します。 ワークフローデザイナー Workflow アクティビティデザイナーを使用すると、開発者はワークフローを自然な方法で作成できます。

## <a name="the-flowchart-activity"></a>Flowchart アクティビティ

<xref:System.Activities.Statements.Flowchart> では、ワークフローの開始時に実行される一意の <xref:System.Activities.Statements.Flowchart.StartNode%2A> を指定します。また、リンクされた <xref:System.Activities.Statements.Flowchart.Nodes%2A> のネットワークを使用して、任意のループを作成したり、特定の時点で実行フローの経路をワークフロー内の任意のポイントへ移動したりします。

### <a name="using-the-flowchart-activity-designer"></a>Flowchart アクティビティ デザイナーの使用

**Flowchart**アクティビティデザイナーは、[**ツールボックス**] の [**フローチャート**] カテゴリにあります。このカテゴリにアクセスするには、ワークフローデザイナーの [**ツールボックス**] タブをクリックします。 または、[**表示**] メニューの [**ツールボックス**] を選択するか、 **Ctrl** + **Alt** + **X**キーを押します。

**Flowchart**アクティビティデザイナーは、[**ツールボックス**] からドラッグして、アクティビティデザイナーが通常配置されている任意の場所 (ルートアクティビティ、または別の制御フローアクティビティの子として) ワークフローデザイナーにドロップすることができます。 **Flowchart**アクティビティデザイナーを空のワークフローデザイナーサーフェイスにドロップすると、アクティビティが作成されます。このアクティビティは、既定では、実行を開始 <xref:System.Activities.Statements.Flowchart> する開始ノードが緑色のボールとして表示される展開ビューに表示されます。 **Flowchart**アクティビティデザイナーを別の制御フローアクティビティにドロップすると、それ自体が最小化されたビューに表示されます。これは、 **flowchart**アクティビティデザイナーをダブルクリックすることで展開できます。 **ツールボックス**のアクティビティは、他の制御フローアクティビティも含めて、 **Flowchart**アクティビティデザイナーに直接ドラッグできます。

さまざまなアクティビティデザイナーをワークフローデザイナーキャンバスにドラッグすると、 <xref:System.Activities.Activity> それらが表すオブジェクトをリンクして、実行の順序を指定できます。 接続元アクティビティと接続先アクティビティの間のリンクを作成するには、接続元アクティビティのデザイナー上にマウス ポインターを置きます。これで、その両側に正方形のハンドルが表示されます。 そのハンドルのどちらかをクリックし、マウス ボタンを押したまま、接続先アクティビティをマウスでポイントしたときにその周りに同様に表示されるハンドルのどちらかにドラッグします。 マウス ボタンを放すと、この 2 つのアクティビティの間にリンクが作成されます。このリンクは、接続元デザイナーから接続先デザイナーへの矢印で表されます。

### <a name="flowchart-activity-properties"></a>Flowchart アクティビティのプロパティ

次の表に、<xref:System.Activities.Statements.Flowchart> のプロパティと、デザイナーでのその使用方法を示します。 これらのプロパティは、プロパティ グリッドまたはデザイナー画面で編集できます。

|プロパティ名|必須|使用|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|×|ヘッダーのアクティビティ デザイナーの表示名を指定します。 既定値は Flowchart です。 この値は、[ **プロパティ** ] ウィンドウで編集することも、アクティビティデザイナーのヘッダーで直接編集することもできます。<br /><br /> <xref:System.Activities.Activity.DisplayName%2A> は必須ではありませんが、使用することをお勧めします。|
|<xref:System.Activities.Statements.Flowchart.Variables%2A>|×|子アクティビティ間で状態を共有するために、この <xref:System.Activities.Statements.Flowchart> 内にスコープ設定された変数のコレクション。|
|<xref:System.Activities.Statements.Flowchart.StartNode%2A>|×|<xref:System.Activities.Statements.FlowNode> の開始時に実行される <xref:System.Activities.Statements.Flowchart>。|
|<xref:System.Activities.Statements.Flowchart.Nodes%2A>|×|<xref:System.Activities.Statements.FlowNode> 内の <xref:System.Activities.Statements.Flowchart> オブジェクトのコレクションが格納されます。|

## <a name="see-also"></a>こちらもご覧ください

- [フローチャート](../workflow-designer/flowchart-activity-designers.md)
- [FlowDecision](../workflow-designer/flowdecision-activity-designer.md)
- [FlowSwitch\<T>](../workflow-designer/flowswitch-t-activity-designer.md)
