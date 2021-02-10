---
title: ローカル関数をメソッドに変換する
description: '[クイック アクションとリファクタリング] メニューを使用して、ローカル関数をメソッドに変換する方法について説明します。'
ms.custom: SEO-VS-2020
ms.date: 02/19/2019
ms.topic: reference
author: kendrahavens
ms.author: kehavens
manager: jmartens
ms.workload:
- dotnet
ms.openlocfilehash: 3cecafe64f7ead8157a9cb6c80d2f0a245566390
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99919727"
---
# <a name="convert-a-local-function-to-a-method"></a>ローカル関数をメソッドに変換する

このリファクタリングは以下に適用されます。

- C#

**概要:** ローカル関数をメソッドに変換します。

**条件:** 現在のローカル コンテキストの外で定義するローカル関数があります。

**理由:** ローカル コンテキストの外で呼び出せるよう、ローカル関数をメソッドに変換します。 ローカル関数が長すぎるとき、メソッドに変換します。 別のメソッドで関数を定義すると、コードが読みやすくなります。

## <a name="convert-local-function-to-method-refactoring"></a>ローカル関数をメソッド リファクタリングに変換する

1. ローカル関数にカーソルを置きます。

    ![ローカル関数をメソッド コード サンプルに変換する](media/convert-local-function-to-method.png)

2. 行の任意の場所で **Ctrl**+ **.** キーを押すと、 **[クイック アクションとリファクタリング]** メニューをトリガーします。

    ![ローカル関数をメソッドのコード修正サンプルに変換する](media/convert-local-function-to-method-codefix.png)

2. Enter キーを押して、リファクタリングを受け入れます。

    ![ローカル関数をメソッドの結果サンプルに変換する](media/convert-local-function-to-method-result.png)

## <a name="see-also"></a>関連項目

- [リファクタリング](../refactoring-in-visual-studio.md)
- [.NET 開発者向けのヒント](../csharp-developer-productivity.md)
