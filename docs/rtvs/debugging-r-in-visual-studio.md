---
title: R コードのデバッグ
description: Visual Studio では、ブレークポイント、アタッチ、呼び出し履歴、変数の検査など、R の完全なデバッグ エクスペリエンスが提供されています。
ms.date: 01/24/2018
ms.topic: conceptual
author: kraigb
ms.author: kraigb
manager: jmartens
ms.workload:
- data-science
ms.openlocfilehash: e3696cac00c726cffb76f29a1da2c503a15af2bd
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99885821"
---
# <a name="debug-r-in-visual-studio"></a>Visual Studio で R をデバッグする

R Tools for Visual Studio (RTVS) は、Visual Studio の全デバッグ機能と統合されています (「[Feature Tour of the Visual Studio Debugger](../debugger/debugger-feature-tour.md)」(Visual Studio デバッガーの機能ツアー) を参照してください)。 このサポートには、ブレークポイント、実行中のプロセスへのアタッチ、変数の検査と監視、コール スタックの検査が含まれます。 この記事では、R および RTVS に固有のデバッグの機能について説明します。

R プロジェクトのスタートアップ R ファイルに対するデバッガーの起動は、他のプロジェクト タイプと同じです。**[デバッグ]** の **[デバッグ開始]**、**F5** キー、またはデバッグ ツールバーの **[Source startup file]\(ソース スタートアップ ファイル\)** を使います。

![R のデバッガー開始ボタン](media/debugger-start-button.png)

スタートアップ ファイルを変更するには、ソリューション エクスプローラーでファイルを右クリックして、 **[R スタートアップ スクリプトとして設定]** を選びます。

いずれの場合も、デバッガーを開始すると、ファイルが対話型ウィンドウに "ソース化" されます。これは、ファイルが読み込まれて、次の対話型ウィンドウの出力のように、そこで実行されることを意味します。

```output
> rtvs::debug_source("c:/proj/rproject1/rproject1/script.R")
Sourcing: c:\proj\rproject1\rproject1\script.R
Sourcing: c:\proj\rproject1\rproject1\Settings.R
```

この例では、スクリプトのソース指定に `rtvs::debug_source` 関数が使用されています。 RTVS はデバッグの準備でコードを変更する必要があるため、この関数が必要です。 RTVS のソース指定コマンドを使用し、デバッガーをアタッチすると、Visual Studio で `rtvs::debug_source` が自動的に使用されます。

また、対話型ウィンドウから、**[R Tools]**、**[セッション]** の順に選択して **[デバッガーのアタッチ]** コマンドを使用するか、**[デバッグ]** の **[R Interactive にアタッチ]** コマンドを使用するか、ツールバーの **[デバッガーのアタッチ]** コマンドを使用して直接、デバッガーを手動でアタッチすることもできます。 その場合は、ユーザーがデバッグするファイルをソース化する必要があります。 ソース ファイルを手動で指定するには、R で通常の `source` コマンドではなく、`rtvs::debug_source` を使用してください。

デバッガーと対話型ウィンドウの間のこの接続により、異なるパラメーター値での関数の呼び出し (およびデバッグ) のような作業が簡単になります。 たとえば、ソース化されたファイル (つまり、セッションに読み込まれているファイル) に、次のような関数があるものとします。

```R
add <- function(x, y) {
    return(x + y)
}
```

そして、`return` ステートメントにブレークポイントを設定します。 対話型ウィンドウで `add(4,5)` を入力すると、ブレークポイントでデバッガーが停止します。

## <a name="environment-browser-in-the-interactive-window"></a>対話型ウィンドウの環境ブラウザー

デバッガーで停止しているときは、[対話型ウィンドウ](interactive-repl-for-r-in-visual-studio.md)の環境ブラウザー プロンプトでも停止しています。 プロンプトは [`Browse[n]>`] と表示されます。n は数字です。

環境ブラウザーは、いくつかの特別なコマンドをサポートしています。

| コマンド | 説明 |
| --- | --- |
| n | 次: コード ファイルの次のステートメントを実行します (ステップ オーバーと同じ)。 |
| s | ステップ イン: コード ファイルの次のステートメントを実行し、次のステートメントが関数呼び出しの場合は関数スコープにステップ インします。 |
| f | 終了: 現在の関数スコープの残りの部分を実行し、呼び出し元に戻ります (ステップ アウトと同じ)。 |
| c、cont | 続行: 次のブレークポイントまでプログラムを実行します。 |
| Q | 完了: デバッグ セッションを終了します。 |
| where | 履歴を表示: 呼び出し履歴を対話型ウィンドウに表示します。 |
| help | ヘルプを表示: 使用可能なコマンドを対話型ウィンドウに表示します。 |
| &lt;expr&gt; | *expr* の式を評価します。 |

![対話型ウィンドウの環境ブラウザー](media/debugger-environment-browser.png)
