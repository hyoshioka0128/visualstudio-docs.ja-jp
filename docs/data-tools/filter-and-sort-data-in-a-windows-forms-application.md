---
title: Windows フォーム アプリケーションのデータのフィルター処理および並べ替えを行う
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- row states, filtering
- data views, sorting
- row version, filtering
- row states
- data views, filtering
- sorting datasets, using data views
- dataset filtering, using data views
ms.assetid: f4f100f1-776d-46dc-b2fd-5b35b98d9561
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 596397cc22cf0f0134463256c0861127dcfb81e1
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75586615"
---
# <a name="filter-and-sort-data-in-a-windows-forms-application"></a>Windows フォーム アプリケーションのデータのフィルター処理および並べ替えを行う

データをフィルター処理するには、<xref:System.Windows.Forms.BindingSource.Filter%2A> プロパティに目的のレコードを返す文字列式を設定します。

データを並べ替えるには、並べ替えに使用する列名に <xref:System.Windows.Forms.BindingSource.Sort%2A> プロパティを設定します。降順で並べ替えるには `DESC` を追加し、昇順に並べ替えるには `ASC` を追加します。

> [!NOTE]
> アプリケーションで <xref:System.Windows.Forms.BindingSource> コンポーネントを使用しない場合は <xref:System.Data.DataView> オブジェクトを使用してデータのフィルター処理と並べ替えを行うことができます。 詳細については、「 [Dataviews](/dotnet/framework/data/adonet/dataset-datatable-dataview/dataviews)」を参照してください。

## <a name="to-filter-data-by-using-a-bindingsource-component"></a>BindingSource コンポーネントを使用してデータをフィルター処理するには

- <xref:System.Windows.Forms.BindingSource.Filter%2A> プロパティに取得する式を設定します。 たとえば、以下のコードは、`CompanyName` が "B" で始まる顧客を返します。

     [!code-csharp[VbRaddataDisplaying#6](../data-tools/codesnippet/CSharp/filter-and-sort-data-in-a-windows-forms-application_1.cs)]
     [!code-vb[VbRaddataDisplaying#6](../data-tools/codesnippet/VisualBasic/filter-and-sort-data-in-a-windows-forms-application_1.vb)]

## <a name="to-sort-data-by-using-a-bindingsource-component"></a>BindingSource コンポーネントを使用してデータを並べ替えるには

- <xref:System.Windows.Forms.BindingSource.Sort%2A> プロパティに並べ替える列を設定します。 たとえば、以下のコードは、`CompanyName` 列に基づいて降順に顧客を並べ替えます。

     [!code-csharp[VbRaddataDisplaying#7](../data-tools/codesnippet/CSharp/filter-and-sort-data-in-a-windows-forms-application_2.cs)]
     [!code-vb[VbRaddataDisplaying#7](../data-tools/codesnippet/VisualBasic/filter-and-sort-data-in-a-windows-forms-application_2.vb)]

## <a name="see-also"></a>関連項目

- [Visual Studio でのデータへのコントロールのバインド](../data-tools/bind-controls-to-data-in-visual-studio.md)
