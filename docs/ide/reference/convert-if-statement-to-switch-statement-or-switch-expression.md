---
title: if ステートメントを switch ステートメントまたは式に変換する
description: '[クイック アクションとリファクタリング] メニューを使用して、if ステートメントを switch ステートメントまたは C# 8.0 スイッチ式に変換する方法について説明します。'
ms.custom: SEO-VS-2020
ms.date: 03/10/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jmartens
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: 0d857338eb1c9b5bb66ccb89e20e6f892944d608
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99936831"
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
