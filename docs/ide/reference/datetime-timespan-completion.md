---
title: IntelliSense を使用した DateTime と TimeSpan の入力
description: IntelliSense メニューを使用して、DateTime および TimeSpan 文字列リテラルと書式設定文字列を入力します。
ms.custom: SEO-VS-2020
ms.date: 07/31/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jmartens
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: bf637106dbf89b533c90b86b2cc50649064fd577
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99919580"
---
# <a name="datetime-and-timespan-completion-by-using-the-intellisense-menu"></a>IntelliSense メニューを使用した DateTime と TimeSpan の入力

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
