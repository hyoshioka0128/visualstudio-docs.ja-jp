---
title: new() の使用
ms.date: 11/03/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: b2091c046efac9f5676e5d2d99ef798283b95f6e
ms.sourcegitcommit: f4b49f1fc50ffcb39c6b87e2716b4dc7085c7fb5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2020
ms.locfileid: "93403555"
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
