---
title: 基底クラスの抽出
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
ms.openlocfilehash: 8eb87ff8e3acc141c49a495b155fb769e03fb89b
ms.sourcegitcommit: f4b49f1fc50ffcb39c6b87e2716b4dc7085c7fb5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2020
ms.locfileid: "93403531"
---
# <a name="extract-base-class"></a>基底クラスの抽出

このリファクタリングは以下に適用されます。

- C#

- Visual Basic

**概要:** 基底クラスを抽出します。

**条件:** 選択したクラスから新しい基底クラスにメンバーを抽出する必要があります。

**理由:** メンバーを手動でプルすると、時間がかかり、ワークフローが終了します。 

## <a name="how-to"></a>方法

1. クラス名または強調表示されたメンバーのいずれかにカレットを置きます。

2. 行の任意の場所で **Ctrl**+ **.** キーを押すと、 **[クイック アクションとリファクタリング]** メニューをトリガーします。

3. **[メンバーを新しい基底クラスに引き上げます]** を選択します。

    ![[Extract base class]\(基本クラスの抽出\) ダイアログ](media/extract-base-class.png)

新しい **[Extract Base Class]\(基底クラスの抽出\)** ダイアログ ボックスが開き、基底クラスの名前と配置先の場所を指定できます。 新しい基底クラスに転送するメンバーを選択し、[抽象化する] 列のチェック ボックスをオンにすることで、メンバーを抽象にすることができます。

## <a name="see-also"></a>関連項目

- [リファクタリング](../refactoring-in-visual-studio.md)
