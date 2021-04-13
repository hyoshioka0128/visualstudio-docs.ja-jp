---
title: クラスを抽象にする
description: 抽象メソッドの記述後、クラスを抽象にする方法について説明します。
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
ms.openlocfilehash: ac3d6b9cef8d20d85049da830dfb830321faab75
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106214539"
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
