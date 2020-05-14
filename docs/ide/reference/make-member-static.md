---
title: メンバーを静的にする
ms.date: 02/19/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: 1ecc66cb58ad11bd431acb341dae0493ce8192da
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "77519303"
---
# <a name="make-member-static"></a>メンバーを静的にする

このリファクタリングは以下に適用されます。

- C#

**概要:** メンバーを静的にします。

**条件:** 静的でないメンバーを静的にしたいとき。

**理由:** 静的メンバーを使用すると読みやすさが向上します。特定のコードが分離されていることを把握することで、理解、再読み取り、再利用が容易になります。 

## <a name="how-to"></a>方法

1. メンバー名にキャレットを配置します。

2. 行の任意の場所で **Ctrl**+ **.** キーを押すと、 (ピリオド) **[クイック アクションとリファクタリング]** メニューがトリガーされます。

   ![メンバーを静的にする](media/make-member-static.png)

3. **[静的にする]** を選択します。

## <a name="see-also"></a>関連項目

- [リファクタリング](../refactoring-in-visual-studio.md)
