---
title: 名前空間に型を移動する
ms.date: 06/17/2019
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: 821e915a0b66f25c5b89a83b31e93b01aea6f400
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "67292705"
---
# <a name="move-type-to-namespace"></a>名前空間に型を移動する

このリファクタリングは以下に適用されます。

- C#

**概要:** 名前空間に型を移動します。

**条件:** 型を別の名前空間またはフォルダーに移動する必要があります。 

**理由:** ソリューションの部分をリファクタリングし、型を別の名前空間またはフォルダーに移動する簡単な方法が必要です。 

## <a name="how-to"></a>方法

1. クラス名にカーソルを置きます。
2. 行の任意の場所で **Ctrl**+ **.** キーを押すと、 **[クイック アクションとリファクタリング]** メニューをトリガーします。
3. **[Move to namespace]\(名前空間に移動する\)** を選択します。

   ![名前空間に移動リファクタリング](media/move-to-namespace.png)

4. 開いたダイアログ ボックスで、型を移動する先の名前空間を選択します。 

   ![名前空間の選択ダイアログ ボックス](media/select-target-namespace.png)

## <a name="see-also"></a>関連項目

- [リファクタリング](../refactoring-in-visual-studio.md)
