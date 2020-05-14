---
title: if ステートメントを反転させる
ms.date: 02/19/2019
ms.topic: reference
author: kendrahavens
ms.author: kehavens
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: a0419100cbc5fcd543eb250fa85cbfe2ebd1c97f
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "65531590"
---
# <a name="invert-if-statement"></a>if ステートメントを反転させる

このリファクタリングは以下に適用されます。

- C#
- Visual Basic

**概要:** コードの意味を変えずに `if` または `if else` ステートメントを反転させることができます。

**条件:** 反転させたほうがわかりやすい `if` または `if else` ステートメントがあるとき。

**理由:** 手動で `if` または `if else` ステートメントを反転させると、時間がかかり、エラーが発生する可能性があります。 このコード修正では、このリファクタリングを自動的に実行できます。

## <a name="invert-if-statement-refactoring"></a>if ステートメント反転のリファクタリング

1. `if` または `if else` ステートメントにカーソルを置きます。

    ![if else を反転する](media/invert-if.png)

2. 行の任意の場所で **Ctrl**+ **.** キーを押すと、 **[クイック アクションとリファクタリング]** メニューをトリガーします。

    ![if else 反転のコード修正](media/invert-if-codefix.png)

3. **[if を反転する]** を選択します。

    ![if else 反転の結果](media/invert-if-codefix-result.png)

## <a name="see-also"></a>関連項目

- [リファクタリング](../refactoring-in-visual-studio.md)
- [.NET 開発者向けのヒント](../csharp-developer-productivity.md)
