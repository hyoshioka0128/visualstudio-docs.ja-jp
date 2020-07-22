---
title: ワークフローデザイナーの分岐アクティビティデザイナー
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.PickBranch.UI
ms.assetid: f523ad47-bbc0-4cda-a35c-41e67c4ba081
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 34da9091c0f96b7270678f9b36fe861e4a87418f
ms.sourcegitcommit: 186c0c250d85ac74274fa1e438b4c7c7108d8a36
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/22/2020
ms.locfileid: "86876087"
---
# <a name="pickbranch-activity-designer"></a>PickBranch アクティビティ デザイナー

<xref:System.Activities.Statements.PickBranch> は、受信イベントによってトリガー可能な、<xref:System.Activities.Statements.Pick> アクティビティ内のイベント ベースの実行パスを提供します。

## <a name="pickbranch"></a>PickBranch

<xref:System.Activities.Statements.PickBranch> オブジェクトは、<xref:System.Activities.Statements.Pick.Branches%2A> アクティビティの <xref:System.Activities.Statements.Pick> コレクションに格納されます。 各 <xref:System.Activities.Statements.PickBranch> は <xref:System.Activities.Statements.Pick> アクティビティの分岐に格納され、トリガーの役割を果たす受信イベントに応答して実行できます。 この方法では、ワークフローデザイナーによってイベントベースの制御フローモデリングが提供されます。 各 <xref:System.Activities.Statements.PickBranch> には、<xref:System.Activities.Statements.PickBranch.Trigger%2A> および <xref:System.Activities.Statements.PickBranch.Action%2A> が含まれます。

### <a name="how-to-use-the-pick-activity-designer"></a>Pick アクティビティ デザイナーの使用方法

[**ツールボックス**] の [**制御フロー** ] カテゴリで、[候補**分岐**デザイナー] にアクセスします。

<xref:System.Activities.Statements.PickBranch> **Branch1**と**Branch2**の表示名を持つ2つの空のオブジェクトは <xref:System.Activities.Statements.Pick> 、 **Pick**アクティビティデザイナーが最初にワークフローデザイナーにドロップされたときに、アクティビティの要素として既定で作成されます。 これらの <xref:System.Activities.Statements.PickBranch.DisplayName%2A> プロパティ値は、各分岐の候補**分岐**デザイナーヘッダーまたは [**プロパティ**] ウィンドウで編集できます。

オブジェクトをオブジェクトのコレクションに追加するには、 <xref:System.Activities.Statements.PickBranch> <xref:System.Activities.Statements.Pick> [**ツールボックス**] から [Pick **branch** ] デザイナーをドラッグアンドドロップする方法と、 **Pick**デザイン画面内から右クリックメニューを使用する方法の2つがあります。

- **ピック分岐**デザイナーは、 <xref:System.Activities.Statements.PickBranch> [**ツールボックス**] からドラッグして、ワークフローデザイナーサーフェイス上の**Pick**アクティビティデザイナーの分岐のいずれかにドロップすると、を作成します。 新しい <xref:System.Activities.Statements.PickBranch> オブジェクトは、<xref:System.Activities.Statements.Pick> デザイナー内で、コレクションに含まれている既存の <xref:System.Activities.Statements.PickBranch> 要素の左側または右側に配置できます。 マウスを使用して**Pick** **分岐**デザイナーを選択デザイナーにドラッグすると、**選択**デザイナーは、垂直方向の青い灰色のバンドを使用して、特定のマウスの位置にを追加する場所を示し <xref:System.Activities.Statements.PickBranch> ます。

- コンテキストメニューを取得して [**分岐の作成**] を選択し、新しいを追加するには、Pick アクティビティデザイナーを右クリックします (ただし、 **Pick** **分岐**デザイナー内ではありません) <xref:System.Activities.Statements.PickBranch> 。 新しい <xref:System.Activities.Statements.PickBranch> が選択デザイナーの既存のオブジェクトの右側に追加されていることに注意して <xref:System.Activities.Statements.PickBranch> ください。 **Pick**

[候補**分岐**デザイナー] を展開して、[**トリガー** ] ボックスと [**アクション**] ボックスを表示するか、ヘッダーの右側にある二重キャレットをクリックして表示を折りたたむことができます。 <xref:System.Activities.Statements.PickBranch.Trigger%2A> <xref:System.Activities.Statements.PickBranch.Action%2A> <xref:System.Activities.Statements.PickBranch> デザイナーの [**トリガー** ] ボックスと [**アクション**] ボックスにアクティビティをドロップして、それぞれのおよびを編集します。

<xref:System.Activities.Statements.PickBranch>オブジェクトのコレクション内のオブジェクトは、 <xref:System.Activities.Statements.Pick.Branches%2A> <xref:System.Activities.Statements.Pick> **Pick**デザイナー内の新しい位置にドラッグアンドドロップすることで並べ替えることができます。 **選択**デザイナーは、垂直方向の青い灰色のバンドを使用して、 <xref:System.Activities.Statements.PickBranch> が特定のマウスの位置に追加される場所を示します。

<xref:System.Activities.Statements.PickBranch> は 2 とおりの方法で削除できます。

- [**分岐**] デザイナーを選択し、削除します。
- **ピック分岐**デザイナーを選択し、右クリックしてコンテキストメニューを取得し、[**削除**] を選択します。

[**分岐**の選択] デザイナーは必ず選択してください。**トリガー**または**アクション**ボックス内のアクティビティの1つを選択すると、オブジェクトではなく、これらのアクティビティのいずれかが削除され <xref:System.Activities.Statements.PickBranch> ます。

### <a name="pickbranch-properties-in-the-workflow-designer"></a>ワークフロー デザイナーでの PickBranch のプロパティ

次の表は、最も役に立つ <xref:System.Activities.Statements.PickBranch> プロパティと、それらのプロパティをワークフローデザイナーで使用する方法を示しています。

|プロパティ名|必須|使用|
|-|--------------|-|
|<xref:System.Activities.Statements.PickBranch.DisplayName%2A>|誤り|**ピック分岐**デザイナーのヘッダーに表示されるフレンドリ名。 既定値は Branch です。<br /><br /> <xref:System.Activities.Activity.DisplayName%2A> は必須ではありませんが、使用することをお勧めします。|
|<xref:System.Activities.Statements.PickBranch.Trigger%2A>|正しい|各 <xref:System.Activities.Statements.PickBranch> には、<xref:System.Activities.Statements.PickBranch.Trigger%2A> を呼び出すことのできる <xref:System.Activities.Statements.PickBranch.Action%2A> アクションが含まれます。|
|<xref:System.Activities.Statements.PickBranch.Action%2A>|誤り|各 <xref:System.Activities.Statements.PickBranch> には、トリガーされたときに実行される <xref:System.Activities.Statements.PickBranch.Action%2A> が含まれます。|

## <a name="see-also"></a>関連項目

- [制御フロー](../workflow-designer/control-flow-activity-designers.md)
- [Pick アクティビティ](/dotnet/framework/windows-workflow-foundation/pick-activity)
- [Pick アクティビティの使用](/dotnet/framework/windows-workflow-foundation/samples/using-the-pick-activity)