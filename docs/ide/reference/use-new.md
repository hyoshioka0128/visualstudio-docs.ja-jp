---
title: new() の使用
description: '`var` を使用できないときに `new()` を使用する方法について説明します。'
ms.date: 11/03/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jmartens
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: 889be18ab342f515bf5add266088a7ee69c087c1
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106218075"
---
# <a name="use-new"></a>`new()` を使用します

この方法は、次の対象に適用されます。

- C#

**概要:** `new()` を使用してください。

**条件:** `var` を使用できないフィールド、または `var` を使用しないコード スタイル設定があります。

**理由:** そのため、型を 2 回繰り返して、繰り返しコードを記述する必要がありません。

## <a name="how-to"></a>方法

1. フィールド宣言にカレットを置きます。

2. 行の任意の場所で **Ctrl**+ **.** キーを押すと、 **[クイック アクションとリファクタリング]** メニューをトリガーします。

3. **['new(…)' を使用します]** を選択します。

    !['new(…)' を使用します](media/use-new.png)

## <a name="see-also"></a>関連項目

- [リファクタリング](../refactoring-in-visual-studio.md)
