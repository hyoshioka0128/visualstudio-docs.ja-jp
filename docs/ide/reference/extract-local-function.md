---
title: ローカル関数を抽出する
description: コードを選択してから Ctrl + R キー、Ctrl + M キーを選択して、コードの一部を独自の関数に変換します。
ms.date: 02/19/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: e007246b85671a0f4606bbdb3d1e9c4e0dc83541
ms.sourcegitcommit: cd7f122c6850cf442a4ca42d51d05c7a8fe9038d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/12/2021
ms.locfileid: "98129459"
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
