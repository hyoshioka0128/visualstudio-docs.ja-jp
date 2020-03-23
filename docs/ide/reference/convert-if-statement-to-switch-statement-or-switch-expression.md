---
title: if ステートメントを switch ステートメントまたは switch 式に変換する
ms.date: 03/10/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: 93ad96809c77d5644b13e6221a41f0b182fb448f
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "79094146"
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
3. 次の 2 つのオプションから選択します。 

    **['switch' ステートメントに変換]** を選択します。

   ![if ステートメントを switch ステートメントに変換する](media/convert-if-to-switch-statement.png) 

    **['switch' 式に変換する]** を選択します。 

    ![if ステートメントを switch 式に変換する](media/convert-if-to-switch-expression.png) 

## <a name="see-also"></a>関連項目

- [リファクタリング](../refactoring-in-visual-studio.md)
