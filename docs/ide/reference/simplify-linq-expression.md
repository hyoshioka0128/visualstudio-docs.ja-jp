---
title: LINQ 式の簡略化
description: このリファクタリングは、Where メソッドの不要な Enumerable 呼び出しを削除するために利用されます。
ms.date: 08/12/2020
ms.topic: reference
author: m-redding
ms.author: midumont
manager: jmartens
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: 20a3524d786b1f03fc3e221d1b257892d9439a0b
ms.sourcegitcommit: 8590cf6b3351e82827fd21159beefef0c02bf162
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/08/2021
ms.locfileid: "102466168"
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
