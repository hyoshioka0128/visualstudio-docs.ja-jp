---
title: Windows フォーム アプリケーションのデータのフィルター処理および並べ替えを行う
description: Windows フォームアプリケーションでデータのフィルター処理と並べ替えを行います。 フィルタープロパティを、目的のレコードを返す文字列式に設定します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
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
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: 045da0ade1ce60e2a8d21c24238c8e2b061e8612
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106215826"
---
# <a name="filter-and-sort-data-in-a-windows-forms-application"></a>Windows フォーム アプリケーションのデータのフィルター処理および並べ替えを行う

データをフィルター処理するには、<xref:System.Windows.Forms.BindingSource.Filter%2A> プロパティに目的のレコードを返す文字列式を設定します。

データを並べ替えるには、並べ替えに使用する <xref:System.Windows.Forms.BindingSource.Sort%2A> 列名にプロパティを設定します。 `DESC` 降順で並べ替えるには、を追加し、昇順で並べ替えるにはを追加し `ASC` ます。

> [!NOTE]
> アプリケーションでコンポーネントを使用しない場合は <xref:System.Windows.Forms.BindingSource> 、オブジェクトを使用してデータのフィルター処理と並べ替えを行うことができ <xref:System.Data.DataView> ます。 詳しくは、「[DataView](/dotnet/framework/data/adonet/dataset-datatable-dataview/dataviews)」をご覧ください。

## <a name="to-filter-data-by-using-a-bindingsource-component"></a>BindingSource コンポーネントを使用してデータをフィルター処理するには

- <xref:System.Windows.Forms.BindingSource.Filter%2A> プロパティに取得する式を設定します。 たとえば、以下のコードは、`CompanyName` が "B" で始まる顧客を返します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataDisplaying/CS/Form1.cs" id="Snippet6":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataDisplaying/VB/Form1.vb" id="Snippet6":::

## <a name="to-sort-data-by-using-a-bindingsource-component"></a>BindingSource コンポーネントを使用してデータを並べ替えるには

- <xref:System.Windows.Forms.BindingSource.Sort%2A> プロパティに並べ替える列を設定します。 たとえば、以下のコードは、`CompanyName` 列に基づいて降順に顧客を並べ替えます。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataDisplaying/CS/Form1.cs" id="Snippet7":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataDisplaying/VB/Form1.vb" id="Snippet7":::

## <a name="see-also"></a>関連項目

- [Visual Studio でのデータへのコントロールのバインド](../data-tools/bind-controls-to-data-in-visual-studio.md)
