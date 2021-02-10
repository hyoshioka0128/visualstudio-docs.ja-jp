---
title: if ステートメントを反転させる
description: '[クイック アクションとリファクタリング] メニューを使用して、コードの意味を変更せずに if または if else ステートメントを反転させる方法について説明します。'
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
ms.openlocfilehash: cf4ad7c25030e4a331ee67f4957ddac59afdd966
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99852233"
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
