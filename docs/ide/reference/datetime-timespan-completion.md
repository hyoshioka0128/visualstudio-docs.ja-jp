---
title: IntelliSense を使用した DateTime と TimeSpan の入力
description: IntelliSense メニューを使用して、DateTime および TimeSpan 文字列リテラルと書式設定文字列を入力します。
ms.custom: SEO-VS-2020
ms.date: 07/31/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: cd77f2b6b491dd49365cea10b22828815c13d8d9
ms.sourcegitcommit: f1bb1b66ed141837e992b3352ce68ff24c11f53e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2020
ms.locfileid: "93102520"
---
# <a name="datetime-and-timespan-completion-by-using-the-intellisense-menu"></a>IntelliSense メニューを使用した DateTime と TimeSpan の入力

このリファクタリングは以下に適用されます。

- C#

**概要:** IntelliSense メニューを使用した DateTime および TimeSpan 文字列リテラルと書式設定文字列の入力。

**条件:** DateTime および TimeSpan 文字列リテラルと書式設定文字列を記述したいとき。 IntelliSense によって、基本入力と、各文字の説明が示されます。

**理由:** DateTime の形式を記憶しておくことは簡単ではないため、IntelliSense を使用することで楽に記述できます。

## <a name="how-to"></a>方法

1. DateTime または TimeSpan 書式設定文字列にカーソルを置きます。
2. **Ctrl**+**Space** キーを押して、 **IntelliSense** メニューを表示します。
3. 追加する文字を選択します。

   ![IntelliSense を使用した DateTime の入力](media/datetime-completion.png)

## <a name="see-also"></a>関連項目

- [リファクタリング](../refactoring-in-visual-studio.md)
