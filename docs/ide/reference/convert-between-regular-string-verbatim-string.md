---
title: 通常の文字列リテラルと逐語的文字列リテラルの間で変換する
ms.date: 06/08/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: 7e8e239f53f92727072a2fcd6573d6957b7cd3ec
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85290833"
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