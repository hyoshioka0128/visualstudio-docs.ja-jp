---
title: ピック分岐アクティビティデザイナー |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Activities.Statements.PickBranch.UI
ms.assetid: f523ad47-bbc0-4cda-a35c-41e67c4ba081
caps.latest.revision: 10
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: c7c70aa8282fb8f50ed6faca5bcee3177ef81e15
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72672586"
---
# <a name="pickbranch-activity-designer"></a>PickBranch アクティビティ デザイナー
<xref:System.Activities.Statements.PickBranch> は、受信イベントによってトリガー可能な、<xref:System.Activities.Statements.Pick> アクティビティ内のイベント ベースの実行パスを提供します。

## <a name="pickbranch"></a>PickBranch
 <xref:System.Activities.Statements.PickBranch> オブジェクトは、<xref:System.Activities.Statements.Pick.Branches%2A> アクティビティの <xref:System.Activities.Statements.Pick> コレクションに格納されます。 各 <xref:System.Activities.Statements.PickBranch> は <xref:System.Activities.Statements.Pick> アクティビティの分岐に格納され、トリガーの役割を果たす受信イベントに応答して実行できます。 このようにして、[!INCLUDE[wfd1](../includes/wfd1-md.md)]では、イベント ベースの制御フロー モデリングが提供されます。 各 <xref:System.Activities.Statements.PickBranch> には、<xref:System.Activities.Statements.PickBranch.Trigger%2A> および <xref:System.Activities.Statements.PickBranch.Action%2A> が含まれます。

### <a name="how-to-use-the-pick-activity-designer"></a>Pick アクティビティ デザイナーの使用方法
 **ピック分岐**デザイナーは、[**ツールボックス]** の [**制御フロー** ] カテゴリにあります。これにアクセスするには、の [**ツールボックス**] タブをクリックし [!INCLUDE[wfd2](../includes/wfd2-md.md)] ます (または、[**表示**] メニューの [**ツールバー** ] を選択するか、CTRL + ALT + X キーを押します)。

 <xref:System.Activities.Statements.PickBranch> **Branch1**および**Branch2**という表示名を持つ2つの空のオブジェクトは <xref:System.Activities.Statements.Pick> 、 **Pick**アクティビティデザイナーがに最初にドロップされたときにアクティビティの要素として既定で作成され [!INCLUDE[wfd2](../includes/wfd2-md.md)] ます。 これらの <xref:System.Activities.Statements.PickBranch.DisplayName%2A> プロパティ値は、各分岐の候補 **分岐** デザイナーヘッダーまたは [ **プロパティ** ] ウィンドウで編集できます。

 オブジェクトをオブジェクトのコレクションに追加するには、次の2つの方法があり <xref:System.Activities.Statements.PickBranch> <xref:System.Activities.Statements.Pick> ます。**ツールボックス**から Pick**分岐**デザイナーをドラッグアンドドロップする方法と、 **Pick**デザイン画面内からコンテキストメニューを使用する方法です。

1. Pick **分岐** デザイナーは、 <xref:System.Activities.Statements.PickBranch> [ **ツールボックス** ] からドラッグして、画面上の **ピック** アクティビティデザイナーの分岐のいずれかにドロップすると、を作成し [!INCLUDE[wfd2](../includes/wfd2-md.md)] ます。 新しい <xref:System.Activities.Statements.PickBranch> オブジェクトは、<xref:System.Activities.Statements.Pick> デザイナー内で、コレクションに含まれている既存の <xref:System.Activities.Statements.PickBranch> 要素の左側または右側に配置できます。 マウスを使用して**Pick** **分岐**デザイナーを選択デザイナーにドラッグすると、**選択**デザイナーは、垂直方向の青い灰色のバンドを使用して、特定のマウスの位置にを追加する場所を示し <xref:System.Activities.Statements.PickBranch> ます。

2. コンテキストメニューを取得して [**分岐の作成**] を選択し、新しいを追加するには、 **Pick** **アクティビティデザイナーを**右クリックし <xref:System.Activities.Statements.PickBranch> ます。 新しい <xref:System.Activities.Statements.PickBranch> が選択デザイナーの既存のオブジェクトの右側に追加されていることに注意して <xref:System.Activities.Statements.PickBranch> ください。 **Pick**

   [候補 **分岐** デザイナー] を展開して、[ **トリガー** ] ボックスと [ **アクション** ] ボックスを表示するか、ヘッダーの右側にある二重キャレットをクリックして表示を折りたたむことができます。 <xref:System.Activities.Statements.PickBranch.Trigger%2A> <xref:System.Activities.Statements.PickBranch.Action%2A> <xref:System.Activities.Statements.PickBranch> デザイナーの [**トリガー** ] ボックスと [**アクション**] ボックスにアクティビティをドロップして、それぞれのおよびを編集します。

   <xref:System.Activities.Statements.PickBranch>オブジェクトのコレクション内のオブジェクトは、 <xref:System.Activities.Statements.Pick.Branches%2A> <xref:System.Activities.Statements.Pick> **Pick**デザイナー内の新しい位置にドラッグアンドドロップすることで並べ替えることができます。 **選択**デザイナーは、垂直方向の青い灰色のバンドを使用して、 <xref:System.Activities.Statements.PickBranch> が特定のマウスの位置に追加される場所を示します。

   <xref:System.Activities.Statements.PickBranch> は 2 とおりの方法で削除できます。

3. [ **分岐** ] デザイナーを選択し、削除します。

4. **ピック分岐**デザイナーを選択し、右クリックしてコンテキストメニューを取得し、[**削除**] を選択します。

   [ **分岐** の選択] デザイナーは必ず選択してください。 **トリガー** または **アクション** ボックス内のアクティビティの1つを選択すると、オブジェクトではなく、これらのアクティビティのいずれかが削除され <xref:System.Activities.Statements.PickBranch> ます。

### <a name="pickbranch-properties-in-the-workflow-designer"></a>ワークフロー デザイナーでの PickBranch のプロパティ
 次の表に、最も役に立つ <xref:System.Activities.Statements.PickBranch> のプロパティと、[!INCLUDE[wfd2](../includes/wfd2-md.md)]でのその使用方法を示します。

|プロパティ名|必須|使用|
|-------------------|--------------|-----------|
|<xref:System.Activities.Statements.PickBranch.DisplayName%2A>|×|**ピック分岐**デザイナーのヘッダーに表示されるフレンドリ名。 既定値は Branch です。<br /><br /> <xref:System.Activities.Activity.DisplayName%2A> は必須ではありませんが、使用することをお勧めします。|
|<xref:System.Activities.Statements.PickBranch.Trigger%2A>|○|各 <xref:System.Activities.Statements.PickBranch> には、<xref:System.Activities.Statements.PickBranch.Trigger%2A> を呼び出すことのできる <xref:System.Activities.Statements.PickBranch.Action%2A> アクションが含まれます。|
|<xref:System.Activities.Statements.PickBranch.Action%2A>|×|各 <xref:System.Activities.Statements.PickBranch> には、トリガーされたときに実行される <xref:System.Activities.Statements.PickBranch.Action%2A> が含まれます。|

## <a name="see-also"></a>参照
 [Pick アクティビティを使用して](https://msdn.microsoft.com/library/b89be812-a247-4025-b0e3-ffb20db027a6)[フロー](../workflow-designer/control-flow-activity-designers.md) [選択アクティビティ](https://msdn.microsoft.com/library/b3e49b7f-0285-4720-8c09-11ae18f0d53e)を制御する