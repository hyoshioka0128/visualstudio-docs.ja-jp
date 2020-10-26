---
title: LINQ 式の簡略化
ms.date: 08/12/2020
ms.topic: reference
author: m-redding
ms.author: midumont
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: 04485d6ce67c822fd0620bd63f3557851db6dbb9
ms.sourcegitcommit: 577c905de52057a741e68c2ed168ea527813fda5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/15/2020
ms.locfileid: "88251350"
---
# <a name="simplify-linq-expression"></a>LINQ 式の簡略化

このリファクタリングは以下に適用されます。

- C#

**概要:** `Enumerable.Single()` と Enumerable メソッド (`SingleOrDefault()`、`Last()`、`LastOrDefault()`、`Any()`、`Count()`、`First()`、`FirstOrDefault()`) に対して `SomeEnumerableType.Where(<LambdaExpression>).Single()` インスタンスを `SomeEnumerable.Single(<LambdaExpression>)` にリファクタリングします。

**条件:** メソッドによって `Single()` や `SingleOrDefault()` などが呼び出されるすべてのインスタンスには引数がなく、前に `Where()` 式が付きます。 `Where()` 式への入力は式ツリーとして構築できません。

**理由:** `.Where()` メソッドで Enumerable の不要な呼び出しを削除すると、パフォーマンスが改善され、読みやすくなります。

## <a name="how-to"></a>操作方法

1. Visual Basic の `SomeEnumerableType.Where(<LambdaExpression>).Single()` インスタンスの中にカーソルを置きます。
2. 行の任意の場所で **Ctrl**+ **.** キーを押すと、 **[クイック アクションとリファクタリング]** メニューをトリガーします。
3. **[LINQ 式の簡略化]** を選択します

   ![typeof を nameof に変換する](media/simplify-linq-expression.png)

## <a name="see-also"></a>関連項目

- [リファクタリング](../refactoring-in-visual-studio.md)
