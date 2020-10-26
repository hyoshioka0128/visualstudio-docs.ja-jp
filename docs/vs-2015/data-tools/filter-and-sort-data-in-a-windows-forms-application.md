---
title: Windows フォームアプリケーションでのデータのフィルター処理と並べ替え |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- row states, filtering
- data views, sorting
- row version, filtering
- row states
- data views, filtering
- sorting datasets, using data views
- dataset filtering, using data views
ms.assetid: f4f100f1-776d-46dc-b2fd-5b35b98d9561
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 24c623efc141ff84c2585f967596271d1efbc502
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72671641"
---
# <a name="filter-and-sort-data-in-a-windows-forms-application"></a>Windows フォーム アプリケーションのデータのフィルター処理および並べ替えを行う
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

データをフィルター処理するには、<xref:System.Windows.Forms.BindingSource.Filter%2A> プロパティに目的のレコードを返す文字列式を設定します。

 データを並べ替えるには、<xref:System.Windows.Forms.BindingSource.Sort%2A> プロパティに並べ替える列の名前を設定し、降順の場合は末尾に `DESC` を、昇順の場合は末尾に `ASC` を付けます。

> [!NOTE]
> アプリケーションでコンポーネントを使用しない場合は <xref:System.Windows.Forms.BindingSource> 、オブジェクトを使用してデータのフィルター処理と並べ替えを行うことができ <xref:System.Data.DataView> ます。 詳しくは、「[DataView](https://msdn.microsoft.com/library/0fe5dfa2-c1cd-435f-90b6-b4dd2e3ef34b)」をご覧ください。

## <a name="to-filter-data-by-using-a-bindingsource-component"></a>BindingSource コンポーネントを使用してデータをフィルター処理するには

- <xref:System.Windows.Forms.BindingSource.Filter%2A> プロパティに取得する式を設定します。 たとえば、以下のコードは、`CompanyName` が "B" で始まる顧客を返します。

     [!code-csharp[VbRaddataDisplaying#6](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataDisplaying/CS/Form1.cs#6)]
     [!code-vb[VbRaddataDisplaying#6](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataDisplaying/VB/Form1.vb#6)]

## <a name="to-sort-data-by-using-a-bindingsource-component"></a>BindingSource コンポーネントを使用してデータを並べ替えるには

- <xref:System.Windows.Forms.BindingSource.Sort%2A> プロパティに並べ替える列を設定します。 たとえば、以下のコードは、`CompanyName` 列に基づいて降順に顧客を並べ替えます。

     [!code-csharp[VbRaddataDisplaying#7](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataDisplaying/CS/Form1.cs#7)]
     [!code-vb[VbRaddataDisplaying#7](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataDisplaying/VB/Form1.vb#7)]

## <a name="see-also"></a>参照
 [Visual Studio でのデータへのコントロールのバインド](../data-tools/bind-controls-to-data-in-visual-studio.md)
