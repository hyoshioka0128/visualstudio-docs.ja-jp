---
title: 条件式を簡略化する
ms.date: 06/08/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: d0571c01217441d4a39fbfe6fb58ccfe95fd0c5a
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85290956"
---
# <a name="simplify-conditional-expression-refactoring"></a>条件式を簡略化するリファクタリング

このリファクタリングは以下に適用されます。

- C#

**概要:** [条件式](https://docs.microsoft.com/dotnet/csharp/language-reference/operators/conditional-operator)を簡略化できます。

**条件:** 不要なコードを削除してわかりやすくしたいとき。

**理由:** 条件式を簡略化すると、より明確で簡潔な構文になります。 このリファクタリング ツールでは、タスクが自動的に実行され、タスクを手動で行う必要がありません。

## <a name="how-to"></a>方法

1. 条件式にキャレットを置きます。

2. 行の任意の場所で **Ctrl**+ **.** キーを押して **[クイック アクションとリファクタリング]** メニューをトリガーします。

3. **[条件式を簡略化する]** を選択します。

    ![条件式を簡略化する](media/simplify-conditional-expression.png)

## <a name="see-also"></a>関連項目

- [リファクタリング](../refactoring-in-visual-studio.md)