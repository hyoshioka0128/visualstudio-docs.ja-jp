---
title: IntelliSense メニューを使用した DateTime と TimeSpan の入力
ms.date: 07/31/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: 36b6d5440e532653845638f87f7f1d7066af6ba3
ms.sourcegitcommit: 43df639b2cd99200f725a8ebb941477481a6f0ff
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/31/2020
ms.locfileid: "87471556"
---
# <a name="datetime-and-timespan-completion-through-intellisense-menu"></a>IntelliSense メニューを使用した DateTime と TimeSpan の入力

このリファクタリングは以下に適用されます。

- C#

**概要:** IntelliSense メニューを使用した DateTime および TimeSpan 文字列リテラルと書式設定文字列の入力。

**条件:** DateTime および TimeSpan 文字列リテラルと書式設定文字列を記述したいとき。 IntelliSense によって、基本入力と、各文字の説明が示されます。 

**理由:** DateTime の形式を記憶しておくことは簡単ではないため、IntelliSense を使用することで楽に記述できます。

## <a name="how-to"></a>方法

1. DateTime または TimeSpan 書式設定文字列にカーソルを置きます。
2. **Ctrl**+**Space** キーを押して、**IntelliSense** メニューを表示します。
3. 追加する文字を選択します。

   ![IntelliSense を使用した DateTime の入力](media/datetime-completion.png)

## <a name="see-also"></a>関連項目

- [リファクタリング](../refactoring-in-visual-studio.md)
