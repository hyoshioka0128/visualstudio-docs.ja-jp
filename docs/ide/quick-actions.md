---
title: クイック アクション、電球、ねじ回し
description: 1 つのクイック アクションを使用して、コードのリファクタリング、生成、その他の変更を行う方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 03/28/2018
ms.topic: conceptual
author: TerryGLee
ms.author: tglee
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 967e73748b364e7e41b1773a7fab33831152ab18
ms.sourcegitcommit: 935e4d9a20928b733e573b6801a6eaff0d0b1b14
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "95870782"
---
# <a name="quick-actions"></a>クイック アクション

クイック アクションを使うと、コードのリファクタリング、生成、その他の変更を、1 つの操作で簡単に行うことができます。 クイック アクションは、C#、[C++](/cpp/ide/writing-and-refactoring-code-cpp)および Visual Basic のコード ファイルで使用できます。 クイック アクションには、言語に固有のものと、すべての言語が対象になるものがあります。

クイック アクションを使用して、次の操作を実行できます。

- [コード アナライザー](../code-quality/roslyn-analyzers-overview.md)の規則違反に対してコード修正を適用する

::: moniker range=">=vs-2019"

- コード アナライザーの規則違反を[抑制する](../code-quality/use-roslyn-analyzers.md#suppress-violations)か、その重要度を[構成する](../code-quality/use-roslyn-analyzers.md#set-rule-severity-from-the-light-bulb-menu)

::: moniker-end

::: moniker range="vs-2017"

- コード アナライザーの規則違反を[抑制する](../code-quality/use-roslyn-analyzers.md#suppress-violations)

::: moniker-end

- リファクタリングを適用する (例: [一時変数をインライン化する](../ide/reference/inline-temporary-variable.md))

- コードを生成する (例: [ローカル変数を導入する](../ide/reference/introduce-local-variable.md))

> [!NOTE]
> このトピックは、Windows 上の Visual Studio に適用されます。 Visual Studio for Mac については、「[リファクタリング (Visual Studio for Mac)](/visualstudio/mac/refactoring)」を参照してください。

クイック アクションは、電球 ![電球アイコン](media/light-bulb-icon.png) アイコンまたはねじ回し ![ねじ回しアイコン](media/screwdriver-icon.png) アイコンを使うか、適切なコード行にカーソルを置いて **Ctrl**+ **.** キーを押すと 利用できます。 エラーを示す赤い波線があり、Visual Studio にそのエラーに対処するために使用可能な解決策がある場合は、エラー電球 ![エラー電球アイコン](media/error-light-bulb-icon.png) が表示されます。

いずれの言語でも、サードパーティは、たとえば SDK の一部として、カスタマイズした診断や提案を表示できます。Visual Studio ではそれらの規則に基づいて電球マークが表示されます。

## <a name="icons"></a>アイコン

クイック アクションが使用可能なときに表示されるアイコンは、使用可能な解決策またはリファクタリングの種類を示します。 *ねじ回し* ![ねじ回しアイコン](media/screwdriver-icon.png) アイコンは、コードを変更するのに使用可能なアクションがあることを示すだけで、必ずしもそれらを使用する必要はありません。 *黄色の電球* ![電球アイコン](media/light-bulb-icon.png) アイコンは、コードを改善するために実行する *必要がある* 使用可能なアクションがあることを示します。 *エラー電球* ![エラー電球アイコン](media/error-light-bulb-icon.png) アイコンは、コード内のエラーを修正するために使用可能なアクションがあることを示します。

## <a name="to-see-a-light-bulb-or-screwdriver"></a>電球やねじ回しを表示するには

使用できる修正がある場合は、電球が表示されます。

- エラーの場所をマウスでポイントしたとき

   ![電球でのマウス ホバー](../ide/media/vs2015_lightbulb_hover.png)

- 該当するコード行にキャレット (カーソル) を移動したとき、エディターの左余白に

行のどこかで **Ctrl**+ **.** キーを押しても、 使用可能なクイック アクションとリファクタリングの一覧が表示されます。

修正候補を表示するには、電球の横の下矢印を選択するか、**[修正候補を表示する]** リンクを選択します。 使用可能なクイック アクションのリストが表示されます。

![拡大電球](../ide/media/vs2015_lightbulb_hover_expanded.png)

## <a name="see-also"></a>関連項目

- [Visual Studio でのコード生成](../ide/code-generation-in-visual-studio.md)
- [共通のクイック アクション](../ide/common-quick-actions.md)
- [コード スタイルとクイック アクション](../ide/code-styles-and-code-cleanup.md)
- [コードの記述とリファクタリング (C++)](/cpp/ide/writing-and-refactoring-code-cpp)
- [リファクタリング (Visual Studio for Mac)](/visualstudio/mac/refactoring)
