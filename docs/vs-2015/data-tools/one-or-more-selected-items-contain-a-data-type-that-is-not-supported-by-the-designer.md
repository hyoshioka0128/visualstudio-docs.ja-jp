---
title: 1つ以上の選択された項目に、デザイナーでサポートされていないデータ型が含まれています |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
ms.assetid: 71dcd4f9-2946-42c5-9ce4-99c819ea2785
caps.latest.revision: 8
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 4e208b697da1c25dfa2e152ad08096f61c876ebe
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72658052"
---
# <a name="one-or-more-selected-items-contain-a-data-type-that-is-not-supported-by-the-designer"></a>1 つ以上の選択された項目に、デザイナーでサポートされていないデータ型が含まれています
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

データベースエクスプローラー**サーバーエクスプローラー**からにドラッグした1つ以上の項目に、でサポートされて / **Database Explorer** [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] いないデータ型が含まれてい [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] ます ( [CLR ユーザー定義型](https://msdn.microsoft.com/library/9f70e0b0-3a0d-4eb1-b914-07a5d0c167c2)など)。

### <a name="to-correct-this-error"></a>このエラーを解決するには

1. 目的のテーブルをベースにした、サポートされていないデータ型を含まないビューを作成します。

2. ビューを**サーバーエクスプローラー** / **データベースエクスプローラー**からデザイナーにドラッグします。

## <a name="see-also"></a>参照
 [Visual Studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)[チュートリアル: LINQ to SQL クラスの作成 (O/R デザイナー)](https://msdn.microsoft.com/library/35aad4a4-2e8a-46e2-ae09-5fbfd333c233) [LINQ to SQL](https://msdn.microsoft.com/library/73d13345-eece-471a-af40-4cc7a2f11655)
