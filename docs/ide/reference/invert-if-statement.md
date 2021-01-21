---
title: if ステートメントを反転させる
description: '[クイック アクションとリファクタリング] メニューを使用して、コードの意味を変更せずに if または if else ステートメントを反転させる方法について説明します。'
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
ms.openlocfilehash: 71b3a11e053b6a600d0b33db7c52a91c4950bf5b
ms.sourcegitcommit: 2cf87f79762906ccaa133a7645aa4c77a0bed7da
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2020
ms.locfileid: "96616981"
---
# <a name="invert-if-statement"></a>if ステートメントを反転させる

このリファクタリングは以下に適用されます。

- C#
- Visual Basic

**概要:** コードの意味を変えずに `if` または `if else` ステートメントを反転させることができます。

**条件:** 反転させたほうがわかりやすい `if` または `if else` ステートメントがあるとき。

**理由:** 手動で `if` または `if else` ステートメントを反転させると、時間がかかり、エラーが発生する可能性があります。 このコード修正では、このリファクタリングを自動的に実行できます。

## <a name="invert-if-statement-refactoring"></a>if ステートメント反転のリファクタリング

1. `if` または `if else` ステートメントにカーソルを置きます。

    ![if else を反転する](media/invert-if.png)

2. 行の任意の場所で **Ctrl**+ **.** キーを押すと、 **[クイック アクションとリファクタリング]** メニューをトリガーします。

    ![if else 反転のコード修正](media/invert-if-codefix.png)

3. **[if を反転する]** を選択します。

    ![if else 反転の結果](media/invert-if-codefix-result.png)

## <a name="see-also"></a>関連項目

- [リファクタリング](../refactoring-in-visual-studio.md)
- [.NET 開発者向けのヒント](../csharp-developer-productivity.md)
