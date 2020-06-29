---
title: IComparable を実装する型の比較演算子を生成する
ms.date: 05/12/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 31e33b562a5a11ff77c1d610fbce9e90506b036d
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85290836"
---
# <a name="generate-comparison-operators-for-types-that-implement-icomparable"></a>IComparable を実装する型の比較演算子を生成する

このコード生成は以下に適用されます。

- C#

**概要:** IComparable を実装する型の**比較**演算子を生成できます。

**条件:** 比較演算子が自動的に追加される　IComparable を実装する型があること。

**理由:** 値の型を実装する場合、ValueType の Equals メソッドの既定の実装を上回るパフォーマンスを得るには、**Equals** メソッドのオーバーライドを検討する必要があります。

## <a name="how-to"></a>方法

1. クラス内または IComparable キーワード上にカーソルを置きます。

2. 次に、以下のいずれかを実行します。

   - 行の任意の場所で **Ctrl**+ **.** キーを押すと、 **[クイック アクションとリファクタリング]** メニューをトリガーします。

   - 右クリックして **[クイック アクションとリファクタリング]** メニューを選択します。

   - テキスト カーソルが既に赤い波線の行にある場合は、左余白に表示されている ![ねじ回し](../media/screwdriver-icon.png) アイコンをクリックします。

   ![[Generate Comparison Operators]\(比較演算子を生成\)](media/generate-comparison-operators.png)

3. ドロップダウン メニューから **[Equals(object) を生成する]** を選択します。

## <a name="see-also"></a>関連項目

- [コード生成](../code-generation-in-visual-studio.md)
- [変更のプレビュー](../../ide/preview-changes.md)
