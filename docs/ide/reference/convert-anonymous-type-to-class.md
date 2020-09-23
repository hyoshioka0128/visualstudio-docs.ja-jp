---
title: 匿名型をクラスに変換する
ms.date: 03/10/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
monikerRange: '>= vs-2019'
ms.openlocfilehash: 251a011695f6f5056e1fdf8e1a6be36b898b66f5
ms.sourcegitcommit: 566144d59c376474c09bbb55164c01d70f4b621c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/19/2020
ms.locfileid: "90809212"
---
# <a name="convert-anonymous-type-to-class"></a>匿名型をクラスに変換する

このリファクタリングは以下に適用されます。

- C#

- Visual Basic

**概要:** 匿名型をクラスに変換します。

**条件:** クラスに組み込みたい匿名型がある場合です。

**理由:** 匿名型は、それをローカルで使用しているときのみ便利です。 コードが長くなった場合、それをクラスに昇格させる簡単な方法があると便利なためです。

## <a name="how-to"></a>方法

1. 匿名型の上にカーソルを置きます。
2. 行の任意の場所で **Ctrl**+ **.** キーを押すと、 **[クイック アクションとリファクタリング]** メニューをトリガーします。

   ![匿名型をクラスに変換する](media/convert-anon-to-class.png)

2. **Enter** キーを押して、リファクタリングを受け入れます。

   ![受け入れられた匿名型のクラスへの変換](media/convert-anon-to-class-complete.png)

## <a name="see-also"></a>関連項目

- [リファクタリング](../refactoring-in-visual-studio.md)
