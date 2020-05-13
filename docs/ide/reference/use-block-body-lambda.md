---
title: ラムダ式またはブロックの本体の使用
ms.date: 02/14/2019
ms.topic: reference
author: kendrahavens
ms.author: kehavens
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: 5c46506e81e5334efea9060e957269e92e9d49cc
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "65531909"
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