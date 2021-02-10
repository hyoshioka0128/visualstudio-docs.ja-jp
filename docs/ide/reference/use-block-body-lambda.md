---
title: ラムダ式またはブロックの本体の使用
description: '[クイック アクションとリファクタリング] メニューを使用して、式本体またはブロック本体を使用するようにラムダ式をリファクタリングする方法を説明します。'
ms.custom: SEO-VS-2020
ms.date: 02/14/2019
ms.topic: reference
author: kendrahavens
ms.author: kehavens
manager: jmartens
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: bc3b80ad625c58fbe9127978ebc23fd8c764f4d3
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99889903"
---
# <a name="use-expression-body-or-block-body-for-lambda-expressions"></a>ラムダ式に式の本体またはブロックの本体を使用する

このリファクタリングは以下に適用されます。

- C#

**概要:** 式の本体またはブロックの本体を使用するためにラムダ式をリファクタリングできます。

**条件:** 式の本体またはブロックの本体を使用するためにラムダ式を使用します。

**理由:** ラムダ式リファクタリングすることで、ユーザー設定に基づいて読みやすさを向上させることができます。

## <a name="lambda-expression-body-or-block-body-refactoring"></a>ラムダ式の式本体またはブロック本体のリファクタリング

1. ラムダ演算子の右にカーソルを置きます。
2. 行の任意の場所で **Ctrl**+ **.** キーを押すと、 **[クイック アクションとリファクタリング]** メニューをトリガーします。

  ![ラムダ式/ブロック本体の使用](media/block-body-lambda.png)

3. **[Use block body for lambda expressions]\(ラムダ式にブロックの本体を使用する\)** または **[Use expression body for lambda expressions]\(ラムダ式に式の本体を使用する\)** を選択します。

## <a name="see-also"></a>関連項目

- [リファクタリング](../refactoring-in-visual-studio.md)
- [.NET 開発者向けのヒント](../csharp-developer-productivity.md)