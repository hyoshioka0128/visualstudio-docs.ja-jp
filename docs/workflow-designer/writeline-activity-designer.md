---
title: ワークフローデザイナー-WriteLine アクティビティデザイナー
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.WriteLine.UI
ms.assetid: 1b5f29a8-b7fd-477e-949e-2f689cae3c96
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7e3b4da69a2d9154f36e42d3b20657e204767872
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "75593025"
---
# <a name="writeline-activity-designer"></a>WriteLine アクティビティ デザイナー

**WriteLine**アクティビティデザイナーは、アクティビティを作成および構成するために使用され <xref:System.Activities.Statements.WriteLine> ます。

## <a name="the-writeline-activity"></a>WriteLine アクティビティ

<xref:System.Activities.Statements.WriteLine> アクティビティは、指定された <xref:System.IO.TextWriter> オブジェクトにテキストを書き込みます。 <xref:System.IO.TextWriter> を指定しない場合、<xref:System.Activities.Statements.WriteLine> はテキストをコンソールに書き込みます。

### <a name="using-the-writeline-activity-designer"></a>WriteLine アクティビティ デザイナーの使用

**WriteLine**アクティビティデザイナーにアクセスするには、**ツールボックス**の [**プリミティブ**] カテゴリを使用します。 **WriteLine**アクティビティデザイナーは、[**ツールボックス**] からドラッグして、アクティビティを通常配置している任意の場所 (内など) にワークフローデザイナー画面にドロップできます <xref:System.Activities.Statements.Sequence> 。 この操作により、WriteLine という既定の <xref:System.Activities.Statements.WriteLine> を持つ <xref:System.Activities.Activity.DisplayName%2A> アクティビティが作成されます。 は、 <xref:System.Activities.Activity.DisplayName%2A> **WriteLine** アクティビティデザイナーのヘッダー、またはプロパティグリッドの [ **DisplayName** ] ボックスで編集できます。

### <a name="the-writeline-properties"></a>WriteLine プロパティ

次の表に、<xref:System.Activities.Statements.WriteLine> のプロパティと、デザイナーでのその使用方法を示します。 これらのプロパティは、プロパティグリッドで編集することができ、一部のプロパティはワークフローデザイナー画面で編集できます。

|プロパティ名|必須|使用|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|×|<xref:System.Activities.Statements.WriteLine> アクティビティの表示名。 既定値は WriteLine です。 <xref:System.Activities.Activity.DisplayName%2A> は必須ではありませんが、使用することをお勧めします。|
|<xref:System.Activities.Statements.WriteLine.Text%2A>|×|書き込むテキスト。 プロパティを設定するには、 **WriteLine**アクティビティデザイナーまたはプロパティグリッドの**テキスト**ボックスに Visual Basic 式を入力します。|
|<xref:System.Activities.Statements.WriteLine.TextWriter%2A>|×|<xref:System.IO.TextWriter> による <xref:System.Activities.Statements.WriteLine> の書き込み先の <xref:System.Activities.Statements.WriteLine.Text%2A>。 既定はコンソールです。|

## <a name="see-also"></a>こちらもご覧ください

- [プリミティブ](../workflow-designer/primitives-activity-designers.md)
- [Assign](../workflow-designer/assign-activity-designer.md)
- [[遅延]](../workflow-designer/delay-activity-designer.md)
- [InvokeMethod](../workflow-designer/invokemethod-activity-designer.md)
