---
title: デバッグ タスクの検索
description: アプリのデバッグに役立つデバッガー機能を特定する
ms.custom: ''
ms.date: 10/01/2019
ms.topic: conceptual
helpviewer_keywords:
- debugging [Visual Studio], find your feature
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 792b5e2d40f7299bf019fd3f9c86697bf008c391
ms.sourcegitcommit: 95f26af1da51d4c83ae78adcb7372b32364d8a2b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79301147"
---
# <a name="find-your-debugging-task-in-visual-studio"></a>デバッグ タスクを見つける

デバッグ タスクを関連する Visual Studio デバッガーの適切な機能にマップする手助けが必要な場合は、この記事で提供されているリンクを使用します。 ここでのタスクの一覧には、デバッグするコードの一時停止、変数の検査、**出力**ウィンドウへのメッセージの送信などの一般的なタスクが含まれています。 デバッガーの機能の概要が必要な場合は、デバッガー[を最初に見るを](debugger-feature-tour.md)参照してください。

## <a name="pause-running-code"></a>実行中のコードを一時停止する

### <a name="pause-running-code-to-inspect-a-line-of-code-that-may-contain-a-bug"></a>実行中のコードを一時停止して、バグが含まれている可能性のあるコード行を検査する

ブレークポイントを設定します。 詳細については、「[ブレークポイントの使用](using-breakpoints.md)」を参照してください。

### <a name="pause-and-inspect-your-app-when-it-reaches-a-specific-state"></a>特定の状態に達したアプリを一時停止して検査する

条件付きロジックを使用してブレークポイントがアクティブになる場所とタイミングを制御するには、条件付きブレークポイントを試します。 詳細については、[ブレークポイントの条件](using-breakpoints.md#breakpoint-conditions)を参照してください。

### <a name="pause-code-only-when-a-specific-objects-property-or-value-changes"></a>特定のオブジェクトのプロパティまたは値が変更された場合にのみコードを一時停止する

C++ の場合は、[データ ブレークポイント](using-breakpoints.md#BKMK_set_a_data_breakpoint_native_cplusplus)を設定します。 
::: moniker range=">= vs-2019"
NET Core 3 を使用するアプリの場合は、[データ ブレークポイント](using-breakpoints.md#BKMK_set_a_data_breakpoint_managed)を設定することもできます。
::: moniker-end

それ以外の場合は、C# と F# の場合のみ、[条件付きブレークポイントを持つオブジェクト ID を追跡](using-breakpoints.md#using-object-ids-in-breakpoint-conditions-c-and-f)できます。

### <a name="pause-code-inside-a-loop-at-a-certain-iteration"></a>特定の反復でループ内のコードを一時停止する

条件としてヒット**カウント**を使用してブレークポイントを設定します。 詳細については、ヒット[カウント](using-breakpoints.md#set-a-hit-count-condition)を参照してください。

### <a name="pause-code-at-the-start-of-a-function-when-you-know-the-function-name-but-not-its-location"></a>関数名はわかっているが、その場所がわからない場合は、関数の先頭でコードを一時停止する

これは関数ブレークポイントで行うことができます。 詳細については、「[関数ブレークポイントの設定](using-breakpoints.md#BKMK_Set_a_breakpoint_in_a_source_file)」を参照してください。

### <a name="pause-code-at-the-start-of-multiple-functions-with-the-same-name"></a>同じ名前の複数の関数の先頭でコードを一時停止する

同じ名前の関数 (異なるプロジェクトのオーバーロードされた関数) を持つ複数の関数がある場合は、[関数ブレークポイント](using-breakpoints.md#BKMK_Set_a_breakpoint_in_a_source_file)を使用できます。

### <a name="manage-and-keep-track-of-your-breakpoints"></a>ブレークポイントの管理と追跡

**[ブレークポイント**] ウィンドウを使用します。 詳細については、「[ブレークポイントの管理](using-breakpoints.md#BKMK_Specify_advanced_properties_of_a_breakpoint_)」を参照してください。

### <a name="pause-code-and-debug-when-a-specific-handled-or-unhandled-exception-is-thrown"></a>特定のハンドルまたはハンドルされない例外がスローされたときにコードを一時停止し、デバッグする

例外ヘルパーはエラーが発生した場所を示しますが、特定のエラーを一時停止してデバッグする場合は、[例外がスローされたときにデバッガーに中断するように指示](managing-exceptions-with-the-debugger.md#tell-the-debugger-to-break-when-an-exception-is-thrown)できます。

### <a name="set-a-breakpoint-from-the-call-stack"></a>呼び出し履歴からブレークポイントを設定する

実行フローの確認中、または **[呼び出し履歴**] ウィンドウでの関数の表示中にコードを一時停止およびデバッグする場合は、「[呼び出し履歴ウィンドウでのブレークポイントの設定](using-breakpoints.md#BKMK_Set_a_breakpoint_from_debugger_windows)」を参照してください。

### <a name="pause-code-at-a-specific-assembly-instruction"></a>特定のアセンブリ命令でコードを一時停止する

これを行うには、[[逆アセンダ] ウィンドウでブレークポイントを設定します](using-breakpoints.md#BKMK_Set_a_breakpoint_from_debugger_windows)。

## <a name="execute-code"></a>コードの実行

### <a name="learn-the-commands-to-step-through-your-code-while-debugging"></a>デバッグ中にコードをステップ実行するコマンドを学習する

詳細については、「[デバッガーを使用してコードを移動する](navigating-through-code-with-the-debugger.md)」を参照してください。

## <a name="inspect-data"></a>データを検査する

### <a name="check-the-value-of-variables-while-running-your-app"></a>アプリの実行中に変数の値を確認する

[データヒント](view-data-values-in-data-tips-in-the-code-editor.md)を使用して変数にカーソルを合わせるか[、自動変数とローカルウィンドウで変数を検査します](autos-and-locals-windows.md)。

### <a name="observe-the-changing-value-of-a-specific-variable"></a>特定の変数の変化する値を観察する

変数にウォッチを設定します。 詳細については、「[変数に監視を設定する](watch-and-quickwatch-windows.md)」を参照してください。

### <a name="view-strings-that-are-too-long-for-the-debugger-window"></a>デバッガー ウィンドウに対して長すぎる文字列を表示する

デバッグ中に、組み込みの[文字列ビジュアライザー](view-strings-visualizer.md)を開きます。

## <a name="configure-debugging"></a>デバッグを構成する

### <a name="customize-information-shown-in-the-debugger"></a>デバッガーに表示される情報をカスタマイズする

オブジェクトの種類以外の情報を、別のデバッガー ウィンドウの値として表示する場合があります。 C#、Visual Basic、F#、および C++/CLI コードの場合は、[デバッガー表示](using-the-debuggerdisplay-attribute.md)属性を使用します。 さらに高度なオプションを使用する場合は、[カスタム ビジュアライザー](create-custom-visualizers-of-data.md)を作成して UI をカスタマイズすることもできます。

ネイティブ C++ の場合は[、NatVis フレームワーク](create-custom-views-of-native-objects.md)を使用します。

### <a name="configure-debugger-settings"></a>デバッガー設定の構成

デバッガーオプションおよびデバッガプロジェクト設定を構成するには、[デバッガーの設定と準備を](debugger-settings-and-preparation.md)参照してください。

## <a name="additional-tasks"></a>追加のタスク

### <a name="fix-an-exception"></a>例外を修正する

[例外の修正を](write-better-code-with-visual-studio.md#fix-an-exception)参照してください。

### <a name="edit-code-during-a-debugging-session"></a>デバッグ セッション中にコードを編集する

[[エディット コンティニュ] を](edit-and-continue.md)使用します。 XAML の場合は[、XAML ホット リロード](../xaml-tools/xaml-hot-reload.md)を使用します。

### <a name="send-messages-to-the-output-window-without-modifying-code"></a>コードを変更せずに出力ウィンドウにメッセージを送信する

トレースポイントを設定します。 詳しくは、[トレース・ポイントの使用を](using-tracepoints.md)参照してください。

## <a name="view-the-order-in-which-functions-are-called"></a>関数が呼び出される順序を表示する

[コール スタックを表示する方法を](how-to-use-the-call-stack-window.md)参照してください。

### <a name="debug-on-remote-machines"></a>リモート マシンでデバッグする

[リモート デバッグ](remote-debugging.md)を参照してください。

### <a name="debug-an-app-that-is-already-running"></a>既に実行されているアプリをデバッグする

[実行中のプロセスへのアタッチを](attach-to-running-processes-with-the-visual-studio-debugger.md)参照してください。

### <a name="debug-multithreaded-applications"></a>マルチスレッド アプリケーションのデバッグ

[マルチスレッド アプリケーションのデバッグ](debug-multithreaded-applications-in-visual-studio.md)を参照してください。

### <a name="fix-performance-issues"></a>パフォーマンスの問題を修正

[「プロファイリング ツールを最初に見る」を](../profiling/profiling-feature-tour.md)参照してください。