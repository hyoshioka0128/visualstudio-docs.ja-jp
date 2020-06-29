---
title: DebuggerDisplay 属性を追加する
ms.date: 05/12/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 611df048d4ce569c10ae933be9053acf1174c06f
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85290848"
---
# <a name="add-debuggerdisplay-attribute"></a>DebuggerDisplay 属性を追加する

このコード生成は以下に適用されます。

- C#

**概要:** [DebuggerDisplay 属性](https://docs.microsoft.com/visualstudio/debugger/using-the-debuggerdisplay-attribute)を使用して、デバッガー変数ウィンドウでのオブジェクト、プロパティ、フィールドの表示方法を制御します。

**条件:** コード内にプログラムによってデバッガー内の[プロパティをピン留め](https://docs.microsoft.com/visualstudio/debugger/view-data-values-in-data-tips-in-the-code-editor#pin-properties-in-datatips)したいとき。

**理由:** プロパティをピン留めすると、デバッガー内のオブジェクトのプロパティ リストの一番上にプロパティをバブルアップすることによって、オブジェクトをプロパティによって迅速に検査できます。 

## <a name="how-to"></a>方法

1. 型、デリゲート、プロパティ、またはフィールドのいずれかにカーソルを置きます。 

2. 行の任意の場所で **Ctrl**+ **.** キーを押して **[クイック アクションとリファクタリング]** メニューをトリガーし、 **[DebuggerDisplay 属性の追加]** を選択します。

    ![[Generate Comparison Operators]\(比較演算子の生成\)](media/add-debugger-display-attribute.png)

3. 既定の ToString() を返す auto メソッドと共に DebuggerDisplay 属性が追加されます。 

## <a name="see-also"></a>関連項目

- [コード生成](../code-generation-in-visual-studio.md)
- [変更のプレビュー](../../ide/preview-changes.md)
