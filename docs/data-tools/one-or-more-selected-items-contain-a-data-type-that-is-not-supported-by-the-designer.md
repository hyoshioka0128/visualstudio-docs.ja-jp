---
title: サポートされていないデータ型
description: 1 つ以上の選択された項目に、デザイナーでサポートされていないデータ型が含まれています
ms.date: 11/04/2016
ms.topic: error-reference
ms.assetid: 71dcd4f9-2946-42c5-9ce4-99c819ea2785
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: b393798ea3abd89b79bb47e4449d33272a3324f8
ms.sourcegitcommit: 2a201c93ed526b0f7e5848657500f1111b08ac2a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2020
ms.locfileid: "89741852"
---
# <a name="one-or-more-selected-items-contain-a-data-type-that-is-not-supported-by-the-designer"></a>1 つ以上の選択された項目に、デザイナーでサポートされていないデータ型が含まれています

**O/r デザイナー**に**サーバーエクスプローラー**または**データベースエクスプローラー**からドラッグした項目の1つ以上に、 **o/r デザイナー**でサポートされていないデータ型 ( [CLR ユーザー定義型](/dotnet/framework/data/adonet/sql/clr-user-defined-types)など) が含まれています。

## <a name="to-correct-this-error"></a>このエラーを解決するには

1. 目的のテーブルをベースにした、サポートされていないデータ型を含まないビューを作成します。

2. **サーバーエクスプローラー**または**データベースエクスプローラー**からデザイナーにビューをドラッグします。

## <a name="see-also"></a>関連項目

- [Visual Studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
