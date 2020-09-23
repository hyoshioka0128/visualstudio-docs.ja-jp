---
title: DebuggerDisplay 属性を追加する
ms.date: 05/12/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: db49bfd1672866a755cce6780527520da2cad420
ms.sourcegitcommit: 566144d59c376474c09bbb55164c01d70f4b621c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/19/2020
ms.locfileid: "90810390"
---
# <a name="add-debuggerdisplay-attribute"></a>DebuggerDisplay 属性を追加する

このコード生成は以下に適用されます。

- C#

**概要:** [DebuggerDisplay 属性](../../debugger/using-the-debuggerdisplay-attribute.md)を使用して、デバッガー変数ウィンドウでのオブジェクト、プロパティ、フィールドの表示方法を制御します。

**条件:** コード内にプログラムによってデバッガー内の[プロパティをピン留め](../../debugger/view-data-values-in-data-tips-in-the-code-editor.md#pin-properties-in-datatips)したいとき。

**理由:** プロパティをピン留めすると、デバッガー内のオブジェクトのプロパティ リストの一番上にプロパティをバブルアップすることによって、オブジェクトをプロパティによって迅速に検査できます。 

## <a name="how-to"></a>方法

1. 型、デリゲート、プロパティ、またはフィールドのいずれかにカーソルを置きます。 

2. 行の任意の場所で **Ctrl**+ **.** キーを押して **[クイック アクションとリファクタリング]** メニューをトリガーし、 **[DebuggerDisplay 属性の追加]** を選択します。

    ![[Generate Comparison Operators]\(比較演算子の生成\)](media/add-debugger-display-attribute.png)

3. 既定の ToString() を返す auto メソッドと共に DebuggerDisplay 属性が追加されます。 

## <a name="see-also"></a>関連項目

- [コード生成](../code-generation-in-visual-studio.md)
- [変更のプレビュー](../../ide/preview-changes.md)