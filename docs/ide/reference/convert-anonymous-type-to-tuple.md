---
title: 匿名型をタプルに変換する
description: Visual Studio で [クイック アクションとリファクタリング] メニューを使用して、匿名型をタプルに変換する方法について説明します。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 452ba826a2765ef624e6c3d04bb20915a26c51fb
ms.sourcegitcommit: 967c2f8c1b3f805cf42c0246389517689d971b53
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96040863"
---
# <a name="convert-anonymous-type-to-tuple"></a>匿名型をタプルに変換する

このリファクタリングは以下に適用されます。

- C#

- Visual Basic

**概要:** 匿名型をタプルに変換します。

**条件:** タプルの資格を満たす匿名型があります。

**理由:** [タプル](/dotnet/csharp/tuples)は構文を軽量に保つのに便利です。 このクイック アクションにより、この C# 機能が利用しやすくなります。

## <a name="how-to"></a>操作方法

1. 匿名型の上にカーソルを置きます。
2. 行の任意の場所で **Ctrl**+ **.** キーを押すと、 **[クイック アクションとリファクタリング]** メニューをトリガーします。

   ![匿名型をタプルに変換する](media/convert-anon-to-tuple.png)

2. **Enter** キーを押して、リファクタリングを受け入れます。

   ![受け入れられた匿名型のタプルへの変換](media/convert-anon-to-tuple-complete.png)

## <a name="see-also"></a>関連項目

- [リファクタリング](../refactoring-in-visual-studio.md)
