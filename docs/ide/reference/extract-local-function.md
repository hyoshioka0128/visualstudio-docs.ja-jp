---
title: ローカル関数を抽出する
description: コードを選択してから Ctrl + R キー、Ctrl + M キーを入力して、コードの一部を独自のメソッドに変換します。
ms.date: 02/19/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: 031fbe22ec61837d489df7a6af923ef0cd2454c7
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "77519327"
---
# <a name="extract-local-function-refactoring"></a>ローカル関数の抽出のリファクタリング

このリファクタリングは以下に適用されます。

- C#

**概要:** 既存のメソッドのコード フラグメントをローカル関数に変換できます。

**条件:** メソッドに、ローカル関数から呼び出される必要がある既存のコードのフラグメントがあるとき。

**理由:** コードのコピー/貼り付けはできるが、重複につながるおそれがあるため。 そのフラグメントをそれ自体のローカル関数にリファクタリングすることをお勧めします。

## <a name="how-to"></a>方法

1. 抽出するコードを強調表示します。

2. 行の任意の場所で **Ctrl**+ **.** キーを押すと、 **[クイック アクションとリファクタリング]** メニューをトリガーします。 

3. **[ローカル関数の抽出]** を選択します。

    ![ローカル関数を抽出する](media/extract-local-function.png)

## <a name="see-also"></a>関連項目

- [リファクタリング](../refactoring-in-visual-studio.md)
- [変更のプレビュー](../../ide/preview-changes.md)
