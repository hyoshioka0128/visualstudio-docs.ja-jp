---
title: ローカル関数を抽出する
description: コードを選択してから Ctrl + R キー、Ctrl + M キーを選択して、コードの一部を独自の関数に変換します。
ms.date: 02/19/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jmartens
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: 80ac8f23b5404d70b70166915cd791f2c0d7ed07
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99860972"
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

    ![行が強調表示されている Visual Studio コード ウィンドウのスクリーンショット。 [クイック アクションとリファクタリング] メニューが開いていて、[ローカル関数の抽出] が選択されています。](media/extract-local-function.png)

## <a name="see-also"></a>関連項目

- [リファクタリング](../refactoring-in-visual-studio.md)
- [変更のプレビュー](../../ide/preview-changes.md)
