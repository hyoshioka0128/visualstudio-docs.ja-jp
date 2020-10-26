---
title: WriteLine アクティビティデザイナー |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Activities.Statements.WriteLine.UI
ms.assetid: 1b5f29a8-b7fd-477e-949e-2f689cae3c96
caps.latest.revision: 5
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: c4f656578526879774e698523239d5a9b2b14ccd
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72657524"
---
# <a name="writeline-activity-designer"></a>WriteLine アクティビティ デザイナー
**WriteLine**アクティビティデザイナーは、アクティビティを作成および構成するために使用され <xref:System.Activities.Statements.WriteLine> ます。

## <a name="the-writeline-activity"></a>WriteLine アクティビティ
 <xref:System.Activities.Statements.WriteLine> アクティビティは、指定された <xref:System.IO.TextWriter> オブジェクトにテキストを書き込みます。 <xref:System.IO.TextWriter> を指定しない場合、<xref:System.Activities.Statements.WriteLine> はテキストをコンソールに書き込みます。

### <a name="using-the-writeline-activity-designer"></a>WriteLine アクティビティ デザイナーの使用
 **WriteLine**アクティビティデザイナーは、**ツールボックス**の [**プリミティブ**] カテゴリにあります。このカテゴリにアクセスするには、の [**ツールボックス**] タブをクリックします [!INCLUDE[wfd2](../includes/wfd2-md.md)] (または、[**表示**] メニューの [**ツールバー** ] を選択するか、CTRL + ALT + X キーを押します)。

 **WriteLine**アクティビティデザイナーは、[**ツールボックス**] からドラッグして、 [!INCLUDE[wfd2](../includes/wfd2-md.md)] アクティビティを通常配置している画面の任意の場所 (内など) にドロップできます <xref:System.Activities.Statements.Sequence> 。 この操作により、WriteLine という既定の <xref:System.Activities.Statements.WriteLine> を持つ <xref:System.Activities.Activity.DisplayName%2A> アクティビティが作成されます。 は、 <xref:System.Activities.Activity.DisplayName%2A> **WriteLine** アクティビティデザイナーのヘッダー、またはプロパティグリッドの [ **DisplayName** ] ボックスで編集できます。

### <a name="the-writeline-properties"></a>WriteLine プロパティ
 次の表に、<xref:System.Activities.Statements.WriteLine> のプロパティと、デザイナーでのその使用方法を示します。 これらのプロパティは、プロパティ グリッドで編集できます。また、一部のプロパティは、[!INCLUDE[wfd2](../includes/wfd2-md.md)]のデザイナー画面で編集できます。

|プロパティ名|必須|使用|
|-------------------|--------------|-----------|
|<xref:System.Activities.Activity.DisplayName%2A>|×|<xref:System.Activities.Statements.WriteLine> アクティビティの表示名。 既定値は WriteLine です。 <xref:System.Activities.Activity.DisplayName%2A> は必須ではありませんが、使用することをお勧めします。|
|<xref:System.Activities.Statements.WriteLine.Text%2A>|×|書き込むテキスト。 プロパティを設定するには、 **WriteLine**アクティビティデザイナーまたはプロパティグリッドの**テキスト**ボックスに Visual Basic 式を入力します。|
|<xref:System.Activities.Statements.WriteLine.TextWriter%2A>|×|<xref:System.IO.TextWriter> による <xref:System.Activities.Statements.WriteLine> の書き込み先の <xref:System.Activities.Statements.WriteLine.Text%2A>。 既定はコンソールです。|

## <a name="see-also"></a>参照
 [プリミティブ](../workflow-designer/primitives-activity-designers.md)による[遅延](../workflow-designer/delay-activity-designer.md) [InvokeMethod](../workflow-designer/invokemethod-activity-designer.md)の[割り当て](../workflow-designer/assign-activity-designer.md)