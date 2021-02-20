---
title: 文字列補間の簡略化
description: '[クイック アクションとリファクタリング] メニューを使用して文字列補間を簡略化する方法を説明します。'
ms.custom: SEO-VS-2020
ms.date: 03/10/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jmartens
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: ee23429980accbbedaa2cf14aaf8a673864179a9
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99897794"
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