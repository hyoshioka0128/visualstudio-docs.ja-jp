---
title: サポートされていないデータ型
description: 1 つ以上の選択された項目に、デザイナーでサポートされていないデータ型が含まれています
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: error-reference
ms.assetid: 71dcd4f9-2946-42c5-9ce4-99c819ea2785
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 167146b9a7938e5498e8db023602b2e13f74379c
ms.sourcegitcommit: 4ae5e9817ad13edd05425febb322b5be6d3c3425
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/11/2020
ms.locfileid: "90034079"
---
# <a name="one-or-more-selected-items-contain-a-data-type-that-is-not-supported-by-the-designer"></a>1 つ以上の選択された項目に、デザイナーでサポートされていないデータ型が含まれています

**O/r デザイナー**に**サーバーエクスプローラー**または**データベースエクスプローラー**からドラッグした項目の1つ以上に、 **o/r デザイナー**でサポートされていないデータ型 ( [CLR ユーザー定義型](/dotnet/framework/data/adonet/sql/clr-user-defined-types)など) が含まれています。

## <a name="to-correct-this-error"></a>このエラーを解決するには

1. 目的のテーブルをベースにした、サポートされていないデータ型を含まないビューを作成します。

2. **サーバーエクスプローラー**または**データベースエクスプローラー**からデザイナーにビューをドラッグします。

## <a name="see-also"></a>参照

- [Visual Studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
