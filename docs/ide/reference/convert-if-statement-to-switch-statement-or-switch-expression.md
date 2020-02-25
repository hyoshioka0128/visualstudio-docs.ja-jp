---
title: if ステートメントを switch ステートメントまたは switch 式に変換する
ms.date: 02/12/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: cb0c06fe0493f973ea9cf0a566ffda45a49eeeff
ms.sourcegitcommit: 68f893f6e472df46f323db34a13a7034dccad25a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/15/2020
ms.locfileid: "77283461"
---
# <a name="convert-if-statement-to-switch-statement-or-switch-expression"></a>if ステートメントを switch ステートメントまたは switch 式に変換する

このリファクタリングは以下に適用されます。

- C#

**概要:** if ステートメントを [switch ステートメント](/dotnet/csharp/language-reference/keywords/switch)または C# 8.0 [switch 式](/dotnet/csharp/whats-new/csharp-8#switch-expressions)に変換します。

**条件:** `if` ステートメントを `switch` 式に、または `switch` 式をその逆に変換します。 

**理由:** `if` ステートメントを使っている場合、このリファクタリングにより、`switch` ステートメントまたは `switch` 式に簡単に移行できます。

## <a name="how-to"></a>方法

1. `if` キーワードにカーソルを置きます。
2. 行の任意の場所で **Ctrl**+ **.** キーを押すと、 **[クイック アクションとリファクタリング]** メニューをトリガーします。
3. **['switch' ステートメントに変換]** を選択します。

   ![if ステートメントを switch ステートメントまたは switch 式に変換する](media/convert-if-statement-to-switch-statement-or-switch-expression.png) 

## <a name="see-also"></a>関連項目

- [リファクタリング](../refactoring-in-visual-studio.md)
