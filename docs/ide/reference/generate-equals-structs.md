---
title: 構造体の IEquatable 演算子を生成する
description: '[クイック アクションとリファクタリング] メニューを使用して、構造体の Equals および IEquatable 演算子を生成する方法について説明します。'
ms.custom: SEO-VS-2020
ms.date: 05/12/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jmartens
ms.workload:
- dotnet
ms.openlocfilehash: 05792636e1094c53869f0235145aec73b26deea9
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99952981"
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