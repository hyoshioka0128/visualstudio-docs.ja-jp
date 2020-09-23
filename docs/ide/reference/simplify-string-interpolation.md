---
title: 文字列補間の簡略化
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
ms.openlocfilehash: 5e801d417280d5d9ce8225c2185b582544fe2cef
ms.sourcegitcommit: 566144d59c376474c09bbb55164c01d70f4b621c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/19/2020
ms.locfileid: "90810338"
---
# <a name="simplify-string-interpolation-refactoring"></a>文字列補間を簡略化するリファクタリング

このリファクタリングは以下に適用されます。

- C#

- Visual Basic

**概要:** [文字列補間](/dotnet/csharp/tutorials/string-interpolation)を簡略化できます。

**条件:** 簡略化できる文字列補間があること。

**理由:** 文字列補間を簡略化すると、より明確で簡潔な構文になります。 このリファクタリング ツールでは、タスクが自動的に実行され、タスクを手動で行う必要がありません。

## <a name="how-to"></a>方法

1. 文字列補間にキャレットを配置します。

2. 行の任意の場所で **Ctrl**+ **.** キーを押すと、 **[クイック アクションとリファクタリング]** メニューをトリガーします。

3. **[補間の簡略化]** を選択します。

    ![文字列補間の簡略化](media/simplify-string-interpolation.png)

## <a name="see-also"></a>関連項目

- [リファクタリング](../refactoring-in-visual-studio.md)