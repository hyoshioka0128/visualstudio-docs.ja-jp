---
title: ワークフローデザイナー遅延アクティビティデザイナー
description: 遅延アクティビティと、delay アクティビティデザイナーを使用して Delay アクティビティを作成および構成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Delay.UI
ms.assetid: f51742a8-2c9a-47d1-8a23-18459d03ae19
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 1b661dddf6c07bca34e5ea044fd1338da68f4e19
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99894310"
---
# <a name="delay-activity-designer"></a>Delay アクティビティ デザイナー

**Delay** アクティビティデザイナーは、アクティビティを作成および構成するために使用され <xref:System.Activities.Statements.Delay> ます。

## <a name="the-delay-activity"></a>Delay アクティビティ

<xref:System.Activities.Statements.Delay> アクティビティで、ワークフローの実行を、指定した時間だけ遅らせます。

### <a name="use-the-delay-activity-designer"></a>Delay アクティビティデザイナーの使用

**Delay** アクティビティデザイナーは、[**ツールボックス**] の [**プリミティブ**] カテゴリにあります。このカテゴリにアクセスするには、ワークフローデザイナーの [**ツールボックス**] タブをクリックします。 または、[**表示**] メニューの [**ツールボックス**] を選択するか、 **Ctrl** + **Alt** + **X** キーを押します。

**Delay** アクティビティデザイナーは、[**ツールボックス**] からドラッグして、アクティビティを通常配置している任意の場所 (内など) にワークフローデザイナー画面にドロップできます <xref:System.Activities.Statements.Sequence> 。 アクティビティデザイナーを削除する <xref:System.Activities.Statements.Delay> と、既定値の Delay を持つアクティビティが作成さ <xref:System.Activities.Activity.DisplayName%2A> れます。 は、 <xref:System.Activities.Activity.DisplayName%2A> **Delay** アクティビティデザイナーのヘッダー、またはプロパティグリッドの [ **DisplayName** ] ボックスで編集できます。

### <a name="the-delay-properties"></a>Delay プロパティ

次の表は、 <xref:System.Activities.Statements.Delay> プロパティと、デザイナーでのそれらの使用方法を示しています。 これらのプロパティは、プロパティグリッドで編集できます。また、一部のプロパティは、ワークフローデザイナー画面で編集できます。

|プロパティ名|必須|使用|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|False|<xref:System.Activities.Statements.Delay> アクティビティの表示名。 既定値は Delay です。 値は <xref:System.Activities.Activity.DisplayName%2A> 厳密には必須ではありませんが、ベストプラクティスとして使用することをお勧めします。|
|<xref:System.Activities.Statements.Delay.Duration%2A>|True|ワークフローの実行を遅らせる時間の長さ。 このプロパティは、プロパティ グリッドで設定します。 時間の長さを指定するには、00:00:00 という形式のリテラル <xref:System.TimeSpan>、または Visual Basic の式を入力します。|

## <a name="see-also"></a>関連項目

- [Primitives](../workflow-designer/primitives-activity-designers.md)
- [Assign](../workflow-designer/assign-activity-designer.md)
- [Delay アクティビティ デザイナー](../workflow-designer/delay-activity-designer.md)
- [InvokeMethod](../workflow-designer/invokemethod-activity-designer.md)
- [WriteLine](../workflow-designer/writeline-activity-designer.md)