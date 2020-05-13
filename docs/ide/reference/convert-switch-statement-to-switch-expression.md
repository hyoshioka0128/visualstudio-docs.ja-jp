---
title: switch ステートメントを switch 式に変換する
ms.date: 06/19/2019
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: cc13cffe8352d9fb57f5bb991c3af615eddb2a14
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "68740053"
---
# <a name="convert-switch-statement-to-switch-expression"></a>switch ステートメントを switch 式に変換する

このリファクタリングは以下に適用されます。

- C#

**概要:** [switch ステートメント](/dotnet/csharp/language-reference/keywords/switch)を C# 8.0 の [switch 式](/dotnet/csharp/whats-new/csharp-8#switch-expressions)に変換します。

**条件:** `switch` ステートメントを `switch` 式に、またはその逆に変換します。 

**理由:** 式だけを使っている場合、このリファクタリングにより、従来の `switch` ステートメントから簡単に移行できます。

## <a name="how-to"></a>方法

1. `switch` 式は C# 8.0 の新しい機能であるため、プロジェクト ファイルで、[言語バージョンをプレビューに設定](/dotnet/csharp/language-reference/configure-language-version#edit-the-project-file)します。
2. `switch` キーワード内にカーソルを置き、**Ctrl**+ **.** キーを押して、 **[クイック アクションとリファクタリング]** メニューをトリガーします。
3. **[Convert switch statement to expression]\(switch ステートメントを式に変換する\)** を選択します。

   ![switch ステートメントを switch 式に変換する](media/convert-switch-statement-to-switch-expression.png) 

## <a name="see-also"></a>関連項目

- [リファクタリング](../refactoring-in-visual-studio.md)
