---
title: 文字列補間の簡略化
ms.date: 02/12/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: 15f034b0ecf46e19681f3b74e4137a2de9e9d950
ms.sourcegitcommit: 68f893f6e472df46f323db34a13a7034dccad25a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/15/2020
ms.locfileid: "77283437"
---
# <a name="simplify-string-interpolation-refactoring"></a>文字列補間を簡略化するリファクタリング

このリファクタリングは以下に適用されます。

- C#

**概要:** [文字列補間](https://docs.microsoft.com/dotnet/csharp/tutorials/string-interpolation)を簡略化できます。

**条件:** 簡略化できる文字列補間があること。

**理由:** 文字列補間を簡略化すると、より明確で簡潔な構文になります。 このリファクタリング ツールでは、タスクが自動的に実行され、タスクを手動で行う必要がありません。

## <a name="how-to"></a>方法

1. 文字列補間にキャレットを配置します。

2. 行の任意の場所で **Ctrl**+ **.** キーを押すと、 **[クイック アクションとリファクタリング]** メニューをトリガーします。

3. **[補間の簡略化]** を選択します。

    ![文字列補間の簡略化](media/simplify-string-interpolation.png)

## <a name="see-also"></a>関連項目

- [リファクタリング](../refactoring-in-visual-studio.md)