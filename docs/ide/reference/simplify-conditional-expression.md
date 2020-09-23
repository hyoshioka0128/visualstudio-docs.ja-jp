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
ms.openlocfilehash: 0242c8c89848e3e76673ddfbca8a27c20605048d
ms.sourcegitcommit: 566144d59c376474c09bbb55164c01d70f4b621c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/19/2020
ms.locfileid: "90810351"
---
# <a name="simplify-conditional-expression-refactoring"></a>条件式を簡略化するリファクタリング

このリファクタリングは以下に適用されます。

- C#

**概要:** [条件式](/dotnet/csharp/language-reference/operators/conditional-operator)を簡略化できます。

**条件:** 不要なコードを削除してわかりやすくしたいとき。

**理由:** 条件式を簡略化すると、より明確で簡潔な構文になります。 このリファクタリング ツールでは、タスクが自動的に実行され、タスクを手動で行う必要がありません。

## <a name="how-to"></a>方法

1. 条件式にキャレットを置きます。

2. 行の任意の場所で **Ctrl**+ **.** キーを押して **[クイック アクションとリファクタリング]** メニューをトリガーします。

3. **[条件式を簡略化する]** を選択します。

    ![条件式を簡略化する](media/simplify-conditional-expression.png)

## <a name="see-also"></a>関連項目

- [リファクタリング](../refactoring-in-visual-studio.md)