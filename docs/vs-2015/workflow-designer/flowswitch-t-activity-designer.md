---
title: FlowSwitch &lt; T &gt; アクティビティデザイナー |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Activities.Core.Presentation.FlowSwitchLink.UI
- System.Activities.Statements.FlowSwitch`1.UI
- System.Activities.Core.Presentation.FlowSwitchLink`1.UI
- System.Activities.Core.Presentation.FlowSwitchLinkIdentifier.UI
ms.assetid: 5b9c5afe-7499-4ee8-8c33-28aff14bde07
caps.latest.revision: 4
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 27abb660766a7c04742eca221432af19f05f0d28
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72656640"
---
# <a name="flowswitchlttgt-activity-designer"></a>FlowSwitch &lt; T &gt; アクティビティデザイナー
<xref:System.Activities.Statements.FlowSwitch%601> アクティビティは、3 つ以上の代替分岐が必要な場合に、一致条件に基づいて制御フローの分岐を提供する条件ノードです。 フローの分岐に必要なパスが 2 つのみである場合は、代わりに <xref:System.Activities.Statements.FlowDecision> アクティビティを使用します。

## <a name="the-flowswitcht-activity"></a>FlowSwitch \<T> アクティビティ
 <xref:System.Activities.Statements.FlowSwitch%601>アクティビティには、 <xref:System.Activities.Statements.FlowSwitch%601.Expression%2A> 評価時に*T*型 (ジェネリックパラメーターで指定) の値を返すが含まれています。 アクティビティには、<xref:System.Activities.Statements.FlowSwitch%601.Cases%2A> のセットも含まれます。これは、この評価の想定される結果から、<xref:System.Activities.Statements.FlowNode> オブジェクトへの一意のマッピングを指定します。 実行されるは、 <xref:System.Activities.Statements.FlowNode> *T* 型のオブジェクトが評価されたの値と一致するものです <xref:System.Activities.Statements.FlowSwitch%601.Expression%2A> 。 <xref:System.Activities.Statements.FlowSwitch%601.Default%2A> case は、一致が取得されない case に対して (必要に応じて) 提供できます。

### <a name="using-the-flowswitcht-activity-designer"></a>FlowSwitch \<T> アクティビティデザイナーの使用
 **FlowSwitch \<T> **アクティビティデザイナーは、**ツールボックス**の [**フローチャート**] カテゴリにあります。このカテゴリにアクセスするには、の左側にある [**ツールボックス**] タブをクリックします [!INCLUDE[wfd2](../includes/wfd2-md.md)] (または、[**表示**] メニューの [**ツールバー** ] を選択するか、CTRL + ALT + X キーを押します)。

 ** \<T> FlowSwitch**アクティビティデザイナーは、[**ツールボックス**] からドラッグして、 [!INCLUDE[wfd2](../includes/wfd2-md.md)] **Flowchart**アクティビティデザイナー内の画面にドロップできます。 表示される **[型の選択** ] ウィンドウを使用して、の評価から取得した型 (コードに関連付けられている、その <xref:System.Activities.Statements.FlowSwitch%601> ジェネリックパラメーターによって関連付けられる) を指定し <xref:System.Activities.Statements.FlowSwitch%601.Expression%2A> ます。 この手順では <xref:System.Activities.Statements.FlowSwitch%601> 、アクティビティ内に **Switch** という名前のアクティビティを作成し <xref:System.Activities.Statements.Flowchart> ます。 をクリックすると、[ <xref:System.Activities.Statements.FlowSwitch%601.Expression%2A> **プロパティ**] ウィンドウの [**式**] ボックスに "VB の式を入力してください" というヒントテキストが表示されます。

 ** \<T> FlowSwitch**アクティビティデザイナーの上にマウスポインターを置くと、リンクするために使用される正方形ハンドルが端に表示され <xref:System.Activities.Statements.FlowSwitch%601.Cases%2A> ます。 **FlowSwitch<T \> **アクティビティデザイナーとその他のアクティビティデザイナーを**フローチャート**にドラッグすると、 <xref:System.Activities.Activity> それらが表すオブジェクトを相互にリンクして、実行の順序を指定できます。 に関連付けられているのいずれかを作成するには、 <xref:System.Activities.Statements.FlowSwitch%601.Cases%2A> <xref:System.Activities.Statements.FlowSwitch%601> **FlowSwitch \<T> **の境界上にあるいずれかの四角形のハンドルをクリックし、マウスボタンを押したままドラッグして、そのデザイナーの上にマウスを置いたときに、対象アクティビティの周囲に同様の方法で表示されるハンドルのいずれかにドラッグします。 マウスボタンを放すと、 **FlowSwitch \<T> **から変換先デザイナーへの矢印が表示され、このケースが示されます。 このケースの既定値は矢印に表示され、[**プロパティ**] ウィンドウの [**ケース**] ボックスで編集できます。

### <a name="the-flowswitcht-properties"></a>FlowSwitch の \<T> プロパティ
 次の表に、<xref:System.Activities.Statements.FlowSwitch%601> のプロパティと、デザイナーでのその使用方法を示します。 これらのプロパティは、プロパティ グリッドまたはデザイナー画面で編集できます。

|プロパティ名|必須|使用|
|-------------------|--------------|-----------|
|<xref:System.Activities.Statements.FlowSwitch%601.Expression%2A>|○|実行パスのどの <xref:System.Activities.Statements.FlowSwitch%601.Cases%2A> に切り替えるかを決定するために評価される式を指定します。|
|<xref:System.Activities.Statements.FlowSwitch%601.Cases%2A>|×|<xref:System.Activities.Statements.FlowSwitch%601.Expression%2A> の評価によって得られる可能性のある結果から、<xref:System.Activities.Statements.FlowNode> オブジェクトのセットへの一意のマッピングを指定します。|
|<xref:System.Activities.Statements.FlowSwitch%601.Default%2A>|○|<xref:System.Activities.Statements.FlowSwitch%601.Expression%2A> の評価が、<xref:System.Activities.Statements.FlowSwitch%601.Cases%2A> オブジェクトに含まれる値のいずれにも一致しない場合のマッピングを指定します。|

## <a name="see-also"></a>参照
 [フロー](../workflow-designer/flowchart-activity-designers.md) [チャートフローチャート](../workflow-designer/flowchart-activity-designer.md) [flowdecision](../workflow-designer/flowdecision-activity-designer.md)