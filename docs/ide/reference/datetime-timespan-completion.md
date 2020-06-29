---
title: IntelliSense メニューを使用した DateTime と TimeSpan の入力
ms.date: 06/08/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: eaa8a344e46c031b37b52106ba9aef25dac59b0c
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85290837"
---
# <a name="datetime-and-timespan-completion-through-intellisense-menu"></a>IntelliSense メニューを使用した DateTime と TimeSpan の入力

このリファクタリングは以下に適用されます。

- C#

**概要:** IntelliSense メニューを使用した DateTime および TimeSpan 文字列リテラルの入力。

**条件:** DateTime および TimeSpan 文字列リテラルを記述したいとき。 IntelliSense によって、基本入力と、各文字の説明が示されます。 

**理由:** DateTime の形式を記憶しておくことは簡単ではないため、IntelliSense を使用することで楽に記述できます。

## <a name="how-to"></a>方法

1. DateTime または TimeSpan 文字列リテラル内にカーソルを置きます。
2. **Ctrl**+**Space** キーを押して、**IntelliSense** メニューを表示します。
3. 追加する文字を選択します。

   ![IntelliSense を使用した DateTime の入力](media/datetime-completion.png)

## <a name="see-also"></a>関連項目

- [リファクタリング](../refactoring-in-visual-studio.md)
