---
title: 静的ローカル関数のリファクタリング オプション
ms.date: 02/10/2020
ms.topic: reference
author: governesss
ms.author: midumont
manager: jillfra
f1_keywords:
- vs.csharp.refactoring.make.local.function.static
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: c297457c910c484c05c974c581e89c75e0ad44e5
ms.sourcegitcommit: a86ee68e3ec23869b6eaaf6c6b7946b1d9a88d01
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/11/2020
ms.locfileid: "77144838"
---
# <a name="static-local-function-refactorings-and-quick-actions"></a>静的ローカル関数のリファクタリングとクイック アクション

この記事では、静的ローカル関数に関連する 2 つの生産性向上機能の概要について説明します。 1 つは、ローカル関数を静的にするリファクタリングです。もう 1 つは、静的ローカル関数に変数を渡すコードを生成するクイック アクションです。

## <a name="make-local-function-static"></a>ローカル関数を静的にする

このリファクタリングは以下に適用されます。

- C#

**概要:** ローカル関数を静的にし、関数の外部で定義された変数を、関数の宣言と呼び出しに渡します。

**条件:** ローカル関数を静的にし、すべての変数をその関数のスコープ内で定義することができます。

**理由:** 静的ローカル関数を使用すると読みやすさが向上します。特定のコードが分離されていることを把握することで、理解、再読み取り、再利用が容易になります。 また、静的ローカル関数によってスコープも提供され、1 つのメソッド内のみで呼び出される静的関数でクラスが煩雑になるのを防ぐことができます。

### <a name="how-to"></a>方法

1. ローカル関数名にキャレットを配置します。

2. 行の任意の場所で **Ctrl**+ **.** キーを押すと、 (ピリオド) **[クイック アクションとリファクタリング]** メニューがトリガーされます。

   ![ローカル関数を静的にする](media/make-local-function-static.png)

3. **[Make local function 'static']\([ローカル関数を '静的' にする]\)** を選択します。

## <a name="pass-variable-explicitly-in-a-static-local-function"></a>静的ローカル関数に変数を明示的に渡す

このクイック アクションは、次に適用されます。

- C#

**概要:** ローカルの静的関数に変数を明示的に渡します。

**条件:** ローカル関数を静的にしつつ、その外部で初期化された変数を引き続き使うことができます。

**理由:** 静的ローカル関数を使うことで、読みやすさが向上します。その宣言や呼び出しはプログラムの特定のコンテキストでしか行えない、ということがわかるためです。 これにより、このコンテキストの外部で変数を定義できる柔軟性がもたらされますが、変数を引数として静的ローカル関数に渡すこともできます。

### <a name="how-to"></a>方法

1. 静的ローカル関数内で使用される場所で、変数にキャレットを配置します。

2. 行の任意の場所で **Ctrl**+ **.** キーを押すと、 (ピリオド) **[クイック アクションとリファクタリング]** メニューがトリガーされます。

   ![静的ローカル関数に変数を明示的に渡す](media/pass-variable-explicitly-static-local-function.png)

3. **[ローカルの静的関数で変数を明示的に渡す]** を選択します。

## <a name="see-also"></a>関連項目

- [リファクタリング](../refactoring-in-visual-studio.md)