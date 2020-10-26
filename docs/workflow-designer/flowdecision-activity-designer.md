---
title: ワークフローデザイナー FlowDecision アクティビティデザイナー
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.FlowDecision.UI
ms.assetid: 4a49edc3-3662-4b7b-812e-0a5ba00d6c94
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 79e405f82bcf33bc01ad07f1092879c17dec5849
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "76111439"
---
# <a name="flowdecision-activity-designer"></a>FlowDecision アクティビティ デザイナー

<xref:System.Activities.Statements.FlowDecision> ノードは条件ノードであり、指定した条件を満たすかどうかに基づいて、2 つの選択肢のどちらかに進む制御フローの分岐を提供します。 フローに 3 つ以上の分岐が必要な場合は、代わりに <xref:System.Activities.Statements.FlowSwitch%601> を使用します。

## <a name="the-flowdecision-node"></a>FlowDecision ノード

<xref:System.Activities.Statements.FlowDecision> は、フローを 2 つに分岐できる場合に使用します。 <xref:System.Activities.Statements.FlowDecision> ノードには、<xref:System.Activities.Statements.FlowDecision.Condition%2A> および <xref:System.Activities.Statements.FlowNode> があり、<xref:System.Activities.Statements.FlowDecision.True%2A> または <xref:System.Activities.Statements.FlowDecision.False%2A> という、想定される 2 つの結果のそれぞれに関連付けられています。 <xref:System.Activities.Statements.FlowDecision.Condition%2A> が評価され、この評価の値により、次に <xref:System.Activities.Statements.FlowNode> 内で処理される <xref:System.Activities.Statements.Flowchart> が決定されます。

### <a name="using-the-flowdecision-designer"></a>FlowDecision デザイナーの使用

**Flowdecision**デザイナーは、[**ツールボックス**] の [**フローチャート**] カテゴリにあります。このカテゴリにアクセスするには、ワークフローデザイナーの [**ツールボックス**] タブをクリックします。 または、[**表示**] メニューの [**ツールボックス**] を選択するか、 **Ctrl** + **Alt** + **X**キーを押します。

**Flowdecision**デザイナーは、[**ツールボックス**] からドラッグして、 **Flowchart**アクティビティデザイナー内のワークフローデザイナー画面にドロップできます。 これにより <xref:System.Activities.Statements.FlowDecision> 、アクティビティ内にラベル付きの **決定** が作成さ <xref:System.Activities.Statements.Flowchart> れます。 デザイナー上にマウスポインターを置くと、2つの分岐の **True** および **False** の四角形ハンドルが表示されます。

**Flowdecision**デザイナーと他のデザイナーを**フローチャート**にドラッグすると、ノードをリンクして実行の順序を指定できます。 ソースノード ( **Flowdecision**の**True**と**False**の分岐を含む) と宛先ノードの間にリンクを作成するには、ソースノードのデザイナー上にマウスポインターを移動します。 そのハンドルのどちらかをクリックし、マウス ボタンを押したまま、接続先ノードにマウス ポインターを置いたときと同じように表示されるハンドルのどちらかにドラッグします。 マウス ボタンを放すと、これら 2 つのノードの間にリンクが作成されます。このリンクは、接続元デザイナーから接続先デザイナーへの矢印で表されます。

を示す式を [ <xref:System.Activities.Statements.FlowDecision.Condition%2A> **プロパティ**] ウィンドウの [**条件**] ボックスに入力するには、ヒントテキストに "VB の式を入力してください" と表示されている場所をクリックします。

### <a name="the-flowdecision-properties"></a>FlowDecision プロパティ

次の表に、<xref:System.Activities.Statements.FlowDecision> のプロパティと、デザイナーでのその使用方法を示します。 これらのプロパティは、プロパティ グリッドまたはデザイナー画面で編集できます。

|プロパティ名|必須|使用法|
|-|--------------|-|
|<xref:System.Activities.Statements.FlowDecision.Condition%2A>|○|フロー制御が使用するパスを決定する条件。|
|<xref:System.Activities.Statements.FlowDecision.True%2A>|×|<xref:System.Activities.Statements.FlowDecision.Condition%2A> が満たされた場合にフロー制御で使用されるパス。|
|<xref:System.Activities.Statements.FlowDecision.False%2A>|×|<xref:System.Activities.Statements.FlowDecision.Condition%2A> が満たされない場合にフロー制御で使用されるパス。|

## <a name="see-also"></a>関連項目

- [フローチャート](../workflow-designer/flowchart-activity-designers.md)
- [フローチャート](../workflow-designer/flowchart-activity-designer.md)
- [FlowSwitch\<T>](../workflow-designer/flowswitch-t-activity-designer.md)
