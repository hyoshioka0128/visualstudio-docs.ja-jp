---
title: クラスを抽象にする
ms.date: 11/03/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jmartens
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: 7b44c8331c10bc0cf2f87e19094a77c0cbec251a
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99919421"
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
