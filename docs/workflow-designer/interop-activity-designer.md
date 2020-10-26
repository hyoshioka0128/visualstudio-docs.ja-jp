---
title: ワークフローデザイナー-相互運用アクティビティデザイナー
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Interop.UI
ms.assetid: 800a3403-ba86-41c4-8de1-c4fee9703eb1
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8047df3787c0871e369b6079e4f0cc80f6d93949
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72650209"
---
# <a name="interop-activity-designer"></a>Interop アクティビティ デザイナー

**Interop**アクティビティデザイナーは、アクティビティを作成および構成するために使用され <xref:System.Activities.Statements.Interop> ます。

## <a name="the-interop-activity"></a>Interop アクティビティ

<xref:System.Activities.Statements.Interop> アクティビティでは、ワークフロー内の <xref:System.Workflow.ComponentModel.Activity?displayProperty=fullName> から派生する型の実行を管理します。

### <a name="use-the-interop-activity-designer"></a>Interop アクティビティデザイナーの使用

**Interop**アクティビティデザイナーは、[**ツールボックス]** の [**移行**] カテゴリにあります。このカテゴリにアクセスするには、[**ツールボックス**] タブをクリックします。または、[**表示**] メニューの [**ツールボックス**] を選択するか、 **Ctrl** + **Alt** + **X**キーを押します。

アクティビティを含む [移行](../workflow-designer/migration-activity-designers.md) カテゴリは、 <xref:System.Activities.Statements.Interop> プロジェクトが .NET Framework 4 (完全) 以降を対象としている場合にのみ、 **ツールボックス** に表示されます。 必要に応じて、プロジェクトが対象とするフレームワークのバージョンを変更できます。

**Interop**アクティビティデザイナーは、[**ツールボックス**] からドラッグして、アクティビティを通常配置している任意の場所 (内など) にワークフローデザイナー画面にドロップできます <xref:System.Activities.Statements.Sequence> 。 **Interop**アクティビティデザイナーを削除する <xref:System.Activities.Statements.Interop> と、interop という既定の**DisplayName**を持つアクティビティが作成されます。 は、 <xref:System.Activities.Activity.DisplayName%2A> **Interop** アクティビティデザイナーのヘッダー、またはプロパティグリッドの [ **DisplayName** ] ボックスで編集できます。

**Interop**アクティビティデザイナーまたはプロパティグリッドで、[ **ActivityType** ] ボックス内のテキストをクリックして**参照**し、[ **.net 型の参照と選択**] ダイアログボックスを開きます。 ワークフロー3.0 またはワークフロー3.5 アクティビティの型のみが表示されます。 つまり、から派生した型のみ <xref:System.Workflow.ComponentModel.Activity> が表示されます。 このボックスを使用して型を指定する方法の詳細については、「 [[.Net 型の参照と選択] ダイアログボックス](../workflow-designer/browse-and-select-a-dotnet-type-dialog-box.md)」を参照してください。

### <a name="the-interop-properties"></a>Interop のプロパティ

次の表に、 <xref:System.Activities.Statements.Interop> プロパティを示し、デザイナーでのそれらの使用方法について説明します。 これらのプロパティは、プロパティグリッドまたはワークフローデザイナー画面で編集できます。

|プロパティ名|必須|使用|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|×|<xref:System.Activities.Statements.Interop> アクティビティの表示名。 既定値は **Interop**です。 表示名は必須ではありませんが、指定することをお勧めします。|
|<xref:System.Activities.Statements.Interop.ActivityType%2A>|○|<xref:System.Activities.Statements.Interop> アクティビティに含まれているアクティビティの型を指定します。 指定されたこの型は、<xref:System.Workflow.ComponentModel.Activity> から派生していることが必要です。|

## <a name="see-also"></a>こちらもご覧ください

- [移行](../workflow-designer/migration-activity-designers.md)