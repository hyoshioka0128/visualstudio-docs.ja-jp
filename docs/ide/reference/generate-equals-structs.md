---
title: 構造体の IEquatable 演算子を生成する
ms.date: 05/12/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: ccc5be9debbdc2b4901d4aad15a0dc4d2bf1bb9f
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85290832"
---
# <a name="generate-iequatable-operators-when-generating-equals-for-structs"></a>構造体の Equals を生成するときに IEquatable 演算子を生成する

このコード生成は以下に適用されます。

- C#

**概要:** [構造体](https://docs.microsoft.com/dotnet/csharp/language-reference/builtin-types/struct)の **Equals** および **IEquatable** 演算子を生成できます。

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
