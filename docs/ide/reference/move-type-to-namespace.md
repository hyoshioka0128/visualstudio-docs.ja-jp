---
title: 名前空間に型を移動する
description: '[クイック アクションとリファクタリング] メニューを使用して、型を別の名前空間またはフォルダーに移動する方法について説明します。'
ms.custom: SEO-VS-2020
ms.date: 06/17/2019
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jmartens
dev_langs:
- CSharp
ms.workload:
- dotnet
monikerRange: vs-2019
ms.openlocfilehash: d6578100bbdab9413fb70a561c146823ac77c914
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99927959"
---
# <a name="move-type-to-namespace"></a>名前空間に型を移動する

このリファクタリングは以下に適用されます。

- C#

**概要:** 名前空間に型を移動します。

**条件:** 型を別の名前空間またはフォルダーに移動する必要があります。 

**理由:** ソリューションの部分をリファクタリングし、型を別の名前空間またはフォルダーに移動する簡単な方法が必要です。 

## <a name="how-to"></a>操作方法

1. クラス名にカーソルを置きます。
2. 行の任意の場所で **Ctrl**+ **.** キーを押すと、 **[クイック アクションとリファクタリング]** メニューをトリガーします。
3. **[Move to namespace]\(名前空間に移動する\)** を選択します。

   ![名前空間に移動リファクタリング](media/move-to-namespace.png)

4. 開いたダイアログ ボックスで、型を移動する先の名前空間を選択します。 

   ![名前空間の選択ダイアログ ボックス](media/select-target-namespace.png)

## <a name="see-also"></a>関連項目

- [リファクタリング](../refactoring-in-visual-studio.md)
