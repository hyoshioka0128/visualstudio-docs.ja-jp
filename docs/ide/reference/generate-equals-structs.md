---
title: 構造体の IEquatable 演算子を生成する
description: '[クイック アクションとリファクタリング] メニューを使用して、構造体の Equals および IEquatable 演算子を生成する方法について説明します。'
ms.custom: SEO-VS-2020
ms.date: 05/12/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 28d70c0ea95c9373eb87e6199d53f1b43fadd508
ms.sourcegitcommit: 2cf87f79762906ccaa133a7645aa4c77a0bed7da
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2020
ms.locfileid: "96617202"
---
# <a name="generate-iequatable-operators-when-generating-equals-for-structs"></a>構造体の Equals を生成するときに IEquatable 演算子を生成する

このコード生成は以下に適用されます。

- C#

**概要:** [構造体](/dotnet/csharp/language-reference/builtin-types/struct)の **Equals** および **IEquatable** 演算子を生成できます。

**条件:** equals および not equals 演算子に加え、IEquatable 演算子が自動的に追加される構造体があること。

**理由:**

- 値の型を実装する場合、ValueType の Equals メソッドの既定の実装を上回るパフォーマンスを得るには、**Equals** メソッドのオーバーライドを検討する必要があります。

- IEquatable インターフェイスを実装すると、型固有の Equals() メソッドが実装されます。

## <a name="how-to"></a>方法

1. 構造体宣言の行のどこかにカーソルを置きます。

2. 次に、以下のいずれかを実行します。

   - 行の任意の場所で **Ctrl**+ **.** キーを押すと、 **[クイック アクションとリファクタリング]** メニューをトリガーします。

   - 右クリックして **[クイック アクションとリファクタリング]** メニューを選択します。

   - テキスト カーソルが既に赤い波線の行にある場合は、左余白に表示されている ![ねじ回し](../media/screwdriver-icon.png) アイコンをクリックします。

   ![構造体の IEquatable および Equals 演算子を生成する](media/generate-equals-structs.png)

3. ドロップダウン メニューから **[Equals(object) を生成する]** を選択します。

## <a name="see-also"></a>関連項目

- [コード生成](../code-generation-in-visual-studio.md)
- [変更のプレビュー](../../ide/preview-changes.md)