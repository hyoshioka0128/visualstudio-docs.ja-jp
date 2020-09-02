---
title: Exists Sincollection &lt; T &gt; アクティビティデザイナー |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Activities.Statements.ExistsInCollection`1.UI
ms.assetid: 0acf9a13-caf5-4bb4-ba22-ec37d2b7267a
caps.latest.revision: 6
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 08aabbcb7dbef2df9a3affa8589a9c6d4205ac58
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72656733"
---
# <a name="existsincollectionlttgt-activity-designer"></a>Exists Sincollection &lt; T &gt; アクティビティデザイナー
存在するアクティビティデザイナーは、アクティビティを作成および構成するために使用されます。 ** \<T> ** <xref:System.Activities.Statements.ExistsInCollection%601>

## <a name="the-existsincollectiont-activity"></a>存在しているコレクション \<T> アクティビティ
 <xref:System.Activities.Statements.ExistsInCollection%601> アクティビティでは、指定した項目が特定のコレクションに存在するかどうかを確認します。

### <a name="using-the-existsincollectiont-activity-designer"></a>"存在しないコレクション" \<T> アクティビティデザイナーの使用
 存在しない**コレクション \<T> **アクティビティデザイナーは、**ツールボックス**の [**コレクション**] カテゴリにあります。ツールボックスの [**ツールボックス**] タブをクリックしてアクセスします [!INCLUDE[wfd2](../includes/wfd2-md.md)] (または、[**表示**] メニューの [**ツールバー** ] を選択するか、CTRL + ALT + X キーを押します)。

 Exists ** \<T> sincollection**アクティビティデザイナーは、[**ツールボックス**] からドラッグして、 [!INCLUDE[wfd2](../includes/wfd2-md.md)] アクティビティを通常配置している画面の任意の場所 (内など) にドロップできます <xref:System.Activities.Statements.Sequence> 。 これ <xref:System.Activities.Statements.ExistsInCollection%601> により、既定値の存在を持つアクティビティが作成さ <xref:System.Activities.Activity.DisplayName%2A> \<Int32> れます。 (既定では、 *Typeargument* は **Int32**です。 プロパティグリッドで変更できます)。 この値は、"存在し <xref:System.Activities.Activity.DisplayName%2A> ない** \<T> コレクション**" アクティビティデザイナーのヘッダー、またはプロパティグリッドの [ **DisplayName** ] ボックスで編集できます。 他のプロパティは、プロパティ グリッドで編集する必要があります。

### <a name="the-existsincollectiont-properties"></a>存在するコレクションの \<T> プロパティ
 次の表に、<xref:System.Activities.Statements.ExistsInCollection%601> のプロパティと、デザイナーでのその使用方法を示します。

|プロパティ名|必須|使用|
|-------------------|--------------|-----------|
|<xref:System.Activities.Activity.DisplayName%2A>|×|<xref:System.Activities.Statements.ExistsInCollection%601> アクティビティの表示名。 既定値は存在しないコレクション \<Int32> です。 <xref:System.Activities.Activity.DisplayName%2A> 値は必須ではありませんが、使用することをお勧めします。|
|<xref:System.Activities.Statements.ExistsInCollection%601.Item%2A>|○|コレクションに追加する項目 \<T> 。 この項目 *の型は型で* 、型は *typeargument*です。 項目を指定するには、プロパティ グリッドで Visual Basic の式を入力します。|
|<xref:System.Activities.Statements.ExistsInCollection%601.Collection%2A>|○|項目の追加先のコレクション。 このコレクションの型は **ICollection \<TypeArgument> です。** コレクションを指定するには、プロパティ グリッドで Visual Basic の式を入力します。|
|*TypeArgument*|○|<xref:System.Collections.Generic.ICollection%601> に格納される項目の T 型。 既定では、この *Typeargument* 型は **Int32**に設定されています。 型を変更するには、プロパティグリッドで、コンボボックスの *Typeargument* の値を変更します。|
|<xref:System.Activities.Activity%601.Result%2A>|×|指定した項目がコレクション内に存在するかどうかを示す値。 結果にバインドする変数を指定するには、プロパティ グリッドで Visual Basic 変数を入力します。|

## <a name="see-also"></a>参照
 [コレクション](../workflow-designer/collection-activity-designers.md) [addtocollection \<T> ](../workflow-designer/addtocollection-t-activity-designer.md) [clearcollection \<T> ](../workflow-designer/clearcollection-t-activity-designer.md) [removefromcollection \<T> ](../workflow-designer/removefromcollection-t-activity-designer.md)