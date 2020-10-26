---
title: Pick アクティビティデザイナー |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Pick.UI
ms.assetid: 642c0a47-1b47-45de-a19a-ca0606cedd7a
caps.latest.revision: 9
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: daefc48cfff2c5c73d9ecf14316777becf4d83c5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72672597"
---
# <a name="pick-activity-designer"></a>Pick アクティビティ デザイナー
<xref:System.Activities.Statements.Pick> アクティビティでは、イベント ベースの制御フローを提供します。 このアクティビティは、トリガー起動イベントに応答して、複数の分岐のいずれか 1 つを実行します。

## <a name="the-pick-activity"></a>Pick アクティビティ
 <xref:System.Activities.Statements.Pick> アクティビティには、<xref:System.Activities.Statements.PickBranch> オブジェクトのコレクションが含まれており、<xref:System.Activities.Statements.Pick> アクティビティはそのオブジェクトの 1 つを、トリガーの役割を果たす受信イベントに応答して実行できます。 このようにして、[!INCLUDE[wfd1](../includes/wfd1-md.md)]では、イベント ベースの制御フロー モデリングが提供されます。 各 <xref:System.Activities.Statements.PickBranch> には、<xref:System.Activities.Statements.PickBranch.Trigger%2A> および <xref:System.Activities.Statements.PickBranch.Action%2A> が含まれます。 <xref:System.Activities.Statements.Pick> アクティビティの実行の開始時に、<xref:System.Activities.Statements.PickBranch> 要素のすべてのトリガー アクティビティがスケジュールされます。 最初のアクティビティが完了すると、対応するアクション アクティビティがスケジュールされ、他のすべてのトリガー アクティビティは取り消されます。

### <a name="how-to-use-the-pick-activity-designer"></a>Pick アクティビティ デザイナーの使用方法
 **Pick**アクティビティデザイナーは、[**ツールボックス]** の [**制御フロー** ] カテゴリにあります。このカテゴリにアクセスするには、の [**ツールボックス**] タブをクリックします (または、[ [!INCLUDE[wfd2](../includes/wfd2-md.md)] **表示**] メニューの [**ツールバー** ] を選択するか、CTRL + ALT + X キーを押します)。

 **Pick**アクティビティデザイナーは、[**ツールボックス**] からドラッグして、 [!INCLUDE[wfd2](../includes/wfd2-md.md)] アクティビティデザイナーを通常配置している画面の任意の場所 ( **Sequence**アクティビティデザイナー内など) にドロップできます。 [!INCLUDE[wfd2](../includes/wfd2-md.md)] にドロップすると、<xref:System.Activities.Statements.Pick> アクティビティが作成されます。このアクティビティには、既定で、Branch1 および Branch2 という表示名を持つ 2 つの空の <xref:System.Activities.Statements.PickBranch> アクティビティが要素として格納されます。 これらの <xref:System.Activities.Statements.PickBranch.DisplayName%2A> プロパティ値は、各分岐の**PickBranch** [**プロパティ**] ウィンドウ内で、または分岐アクティビティデザイナーヘッダーで編集できます。

 オブジェクトのコレクションにアクティビティを追加するには、 <xref:System.Activities.Statements.PickBranch> <xref:System.Activities.Statements.Pick> [**ツールボックス**] から [ピックアップ**分岐**] デザイナーをドラッグアンドドロップする方法と、 **Pick**デザイン画面内からコンテキストメニューを使用する方法の2つの方法があります。 詳細については、「 [ピック分岐](../workflow-designer/pickbranch-activity-designer.md) 」を参照してください。 Pick アクティビティデザイナー内に配置できる項目は、 **Pick** **branch** アクティビティデザイナーのみであることに注意してください。

### <a name="pick-activity-properties-in-the-workflow-designer"></a>ワークフロー デザイナーでの Pick アクティビティのプロパティ
 次の表に、<xref:System.Activities.Statements.Pick> のプロパティと、デザイナーでのその使用方法を示します。 これらのプロパティは、プロパティ グリッドまたはデザイナー画面で編集できます。

|プロパティ名|必須|使用|
|-------------------|--------------|-----------|
|<xref:System.Activities.Activity.DisplayName%2A>|×|ヘッダーの <xref:System.Activities.Statements.Pick> アクティビティ デザイナーの表示名を指定します。 既定値は Pick です。 この値は、プロパティ グリッドで編集することも、アクティビティ デザイナーのヘッダーで直接編集することもできます。<br /><br /> <xref:System.Activities.Activity.DisplayName%2A> は必須ではありませんが、使用することをお勧めします。|

## <a name="see-also"></a>参照
 [Pick アクティビティを使用して](https://msdn.microsoft.com/library/b89be812-a247-4025-b0e3-ffb20db027a6)[フロー](../workflow-designer/control-flow-activity-designers.md) [選択アクティビティ](https://msdn.microsoft.com/library/b3e49b7f-0285-4720-8c09-11ae18f0d53e)を制御する