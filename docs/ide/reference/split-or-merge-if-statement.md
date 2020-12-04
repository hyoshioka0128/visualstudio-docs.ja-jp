---
title: if ステートメントの分割または結合
description: '[クイック アクションとリファクタリング] メニューを使用して、if ステートメントを分割またはマージする方法を説明します。'
ms.custom: SEO-VS-2020
ms.date: 03/10/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: f72c6c2ed1cfdd1c8ea4471976d6a4980dfe422f
ms.sourcegitcommit: df6ba39a62eae387e29f89388be9e3ee5ceff69c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/02/2020
ms.locfileid: "96479928"
---
# <a name="split-or-merge-if-statements"></a>if ステートメントの分割または結合

このリファクタリングは以下に適用されます。

- C#

- Visual Basic

**概要:** **概要:** [if](/dotnet/csharp/language-reference/keywords/if-else) ステートメントを分割または結合します。

**条件:** `&&` または `||` 演算子が使われている `if` ステートメントを、入れ子になった `if` ステートメントに分割します。または、`if` ステートメントを外側の `if` ステートメントと結合します。

**理由:** スタイルの好みの問題です。  

## <a name="how-to"></a>操作方法

`if` ステートメントを分割する場合:

1. `&&` または `||` 演算子による `if` ステートメント内にカーソルを置きます。

2. 行の任意の場所で **Ctrl**+ **.** キーを押すと、 **[クイック アクションとリファクタリング]** メニューをトリガーします。

    ![if ステートメントを分割する](../media/split-if-statement.png)

3. **[Split into nested if statements]\(入れ子になった if ステートメントに分割する\)** を選択します。

    ![完了した if ステートメントの分割](../media/split-if-statement-complete.png)

内側の `if` ステートメントと外側の `if` ステートメントを結合する場合: 

1. 内側の `if` キーワードにカーソルを置きます。

2. 行の任意の場所で **Ctrl**+ **.** キーを押すと、 **[クイック アクションとリファクタリング]** メニューをトリガーします。

    ![if ステートメントを結合する](../media/merge-if-statement.png)

3. **[Merge with outer if statement]\(外側の if ステートメントと結合する\)** を選択します。

    ![完了した if ステートメントの結合](../media/merge-if-statement-complete.png)

## <a name="see-also"></a>関連項目

- [リファクタリング](../refactoring-in-visual-studio.md)