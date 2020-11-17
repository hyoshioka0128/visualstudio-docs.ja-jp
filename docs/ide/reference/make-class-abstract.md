---
title: クラスを抽象にする
ms.date: 11/03/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: 8bfcaa7117249ceffbaed706ac420c5250c02089
ms.sourcegitcommit: f4b49f1fc50ffcb39c6b87e2716b4dc7085c7fb5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2020
ms.locfileid: "93403546"
---
# <a name="make-class-abstract"></a>クラスを抽象にする

このリファクタリングは以下に適用されます。

- C#

- Visual Basic

**概要:** クラスを抽象にリファクタリングにします。

**条件:** 抽象ではないクラスに抽象メソッドを記述します。

**理由:** 抽象メソッドを記述した後にクラスを抽象化するようにコードを修正すると、時間を節約できます。

## <a name="how-to"></a>方法

1. 抽象メソッドにカレットを置きます。

2. 行の任意の場所で **Ctrl**+ **.** キーを押すと、 **[クイック アクションとリファクタリング]** メニューをトリガーします。

3. **[Make class 'abstract']\(クラスを 'abstract' にします\)** を選択します。

    ![クラスを抽象にする](media/make-class-abstract.png)

## <a name="see-also"></a>関連項目

- [リファクタリング](../refactoring-in-visual-studio.md)
