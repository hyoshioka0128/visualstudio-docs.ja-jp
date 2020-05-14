---
title: 匿名型をタプルに変換する
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
ms.openlocfilehash: f7e89c5b5a05900fe42af62ef87f70292e94e662
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "79094278"
---
# <a name="convert-anonymous-type-to-tuple"></a>匿名型をタプルに変換する

このリファクタリングは以下に適用されます。

- C#

- Visual Basic

**概要:** 匿名型をタプルに変換します。

**条件:** タプルの資格を満たす匿名型があります。

**理由:** [タプル](/dotnet/csharp/tuples)は構文を軽量に保つのに便利です。 このクイック アクションにより、この C# 機能が利用しやすくなります。

## <a name="how-to"></a>方法

1. 匿名型の上にカーソルを置きます。
2. 行の任意の場所で **Ctrl**+ **.** キーを押すと、 **[クイック アクションとリファクタリング]** メニューをトリガーします。

   ![匿名型をタプルに変換する](media/convert-anon-to-tuple.png)

2. **Enter** キーを押して、リファクタリングを受け入れます。

   ![匿名型をタプルに変換する](media/convert-anon-to-tuple-complete.png)

## <a name="see-also"></a>関連項目

- [リファクタリング](../refactoring-in-visual-studio.md)
