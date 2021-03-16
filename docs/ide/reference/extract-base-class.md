---
title: 基底クラスの抽出
description: このリファクタリングによって、選択されたクラスから新しい基底クラスにメンバーが抽出されます。
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
ms.openlocfilehash: 9d7a21bbd3e51ee6a6776ca728a545cbbb731cab
ms.sourcegitcommit: 8590cf6b3351e82827fd21159beefef0c02bf162
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/08/2021
ms.locfileid: "102466278"
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
