---
title: 条件式および論理演算を反転させる
description: '[クイックアクションとリファクタリング] メニューを使用して、条件式または AND/OR 条件付き演算子を反転させる方法について説明します。'
ms.custom: SEO-VS-2020
ms.date: 02/19/2019
ms.topic: reference
author: kendrahavens
ms.author: kehavens
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: 180e42d5399116df95289e4e5fd0aed1255bf3de
ms.sourcegitcommit: 2cf87f79762906ccaa133a7645aa4c77a0bed7da
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2020
ms.locfileid: "96617384"
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
