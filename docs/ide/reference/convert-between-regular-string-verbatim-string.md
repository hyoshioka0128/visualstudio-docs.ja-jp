---
title: 通常の文字列リテラルと逐語的文字列リテラルの間で変換する
description: '[クイック アクションとリファクタリング] メニューを使用して、通常の文字列リテラルと逐語的文字列リテラルの間で変換を行う方法について説明します。'
ms.custom: SEO-VS-2020
ms.date: 06/08/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: d50b979902e6eb5a606305b262f5009caef87467
ms.sourcegitcommit: 967c2f8c1b3f805cf42c0246389517689d971b53
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96040460"
---
# <a name="convert-between-regular-string-and-verbatim-string-literals-refactoring"></a>通常の文字列リテラルと逐語的文字列リテラルの間で変換するリファクタリング

このリファクタリングは以下に適用されます。

- C#

**概要:** 通常の文字列リテラルと逐語的文字列リテラルの間で変換できます。

**条件:** 領域を節約するか、コードのわかりやすさを高めたいとき。

**理由:** 逐語的文字列リテラルを標準の文字列リテラルに変換すると、領域を節約するのに役立ちます。 通常の文字列リテラルを逐語的文字列リテラルに変換すると、よりわかりやすくなります。

## <a name="how-to"></a>方法

1. 通常の文字列リテラルまたは逐語的文字列リテラルのいずれかにキャレットを置きます。

2. 行の任意の場所で **Ctrl**+ **.** キーを押すと、 **[クイック アクションとリファクタリング]** メニューをトリガーします。

3. 次のオプションから 1 つを選択します。

    **[Convert to regular string]\(標準文字列に変換\)** を選択します。

    ![[Convert to regular string]\(標準文字列に変換\)](media/convert-to-regular-string.png)

    **[Convert to verbatim string]\(逐語的文字列に変換\)** を選択します。

    ![[Convert to verbatim string]\(逐語的文字列に変換\)](media/convert-to-verbatim-string.png)

## <a name="see-also"></a>関連項目

- [リファクタリング](../refactoring-in-visual-studio.md)