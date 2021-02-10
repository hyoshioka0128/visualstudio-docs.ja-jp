---
title: 条件式および論理演算を反転させる
description: '[クイックアクションとリファクタリング] メニューを使用して、条件式または AND/OR 条件付き演算子を反転させる方法について説明します。'
ms.custom: SEO-VS-2020
ms.date: 02/19/2019
ms.topic: reference
author: kendrahavens
ms.author: kehavens
manager: jmartens
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: 0bd75a40f52a6148a6c50b212183bb8dc7a52d56
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99852246"
---
# <a name="invert-conditional-expressions-and-conditional-andor-operators"></a>条件式と AND/OR 条件付き演算子を反転させる

このリファクタリングは以下に適用されます。

- C#
- Visual Basic

**概要:** 条件式または AND/OR 条件付き演算子を反転させることができます。

**条件:** 反転させたほうがわかりやすい条件式または AND/OR 条件付き演算子があります。

**理由:** 式や AND/OR 条件付き演算子を手動で反転させると、時間がかかり、エラーが発生する可能性があります。 このコード修正では、このリファクタリングを自動的に実行できます。

## <a name="invert-conditional-expressions-and-conditional-andor-operators-refactoring"></a>条件式と AND/OR 条件付き演算子リファクタリングを反映させる

1. 条件式または AND/OR 条件付き演算子にカーソルを置きます。
2. 行の任意の場所で **Ctrl**+ **.** キーを押すと、 **[クイック アクションとリファクタリング]** メニューをトリガーします。
3. **[Invert conditional]\(条件式の反転\)** または **[Replace '&&' with '||']\('&&' を '||' で置換\)** を選択します。

    ![[条件式の反転] オプションのショートカット。](media/invert-conditional.png)

    ![[Replace '&&' with '||']\('&&' を '||' で置換\) オプションのスクリーンショット。](media/invert-logical-operator.png)

## <a name="see-also"></a>関連項目

- [リファクタリング](../refactoring-in-visual-studio.md)
- [.NET 開発者向けのヒント](../csharp-developer-productivity.md)
