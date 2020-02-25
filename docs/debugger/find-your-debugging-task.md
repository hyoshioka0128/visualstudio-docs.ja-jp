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
ms.sourcegitcommit: 2ae2436dc3484b9dfa10e0483afba1e5a02a52eb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/25/2020
ms.locfileid: "77578769"
---
# <a name="find-your-debugging-task-in-visual-studio"></a>Visual Studio でのデバッグタスクの検索

デバッグタスクを、関連する Visual Studio デバッガーの正しい機能にマップするためのヘルプが必要な場合は、この記事に記載されているリンクを使用してください。 ここでのタスクの一覧には、デバッグするコードの一時停止、変数の検査、**出力**ウィンドウへのメッセージの送信などの一般的なタスクが含まれています。 デバッガーの機能の概要については、「[デバッガーの最初](debugger-feature-tour.md)の表示」を参照してください。

## <a name="pause-running-code"></a>実行中のコードの一時停止

### <a name="pause-running-code-to-inspect-a-line-of-code-that-may-contain-a-bug"></a>バグが含まれている可能性のあるコード行を検査するために実行中のコードを一時停止します

ブレークポイントを設定します。 詳細については、「[ブレークポイントの使用](using-breakpoints.md)」を参照してください。

### <a name="pause-and-inspect-your-app-when-it-reaches-a-specific-state"></a>特定の状態に達したときにアプリを一時停止して検査する

条件付きブレークポイントを使って、条件付きロジックを使用してブレークポイントがアクティブになる場所とタイミングを制御します。 詳細については、「[ブレークポイント条件](using-breakpoints.md#breakpoint-conditions)」を参照してください。

### <a name="pause-code-only-when-a-specific-objects-property-or-value-changes"></a>特定のオブジェクトのプロパティまたは値が変更される場合にのみコードを一時停止する

C++では、[データブレークポイント](using-breakpoints.md#BKMK_set_a_data_breakpoint_native_cplusplus)を設定します。 
::: moniker range=">= vs-2019"
.NET Core 3 を使用するアプリでは、[データブレークポイント](using-breakpoints.md#BKMK_set_a_data_breakpoint_managed)を設定することもできます。
::: moniker-end

それ以外のC#場合F# 、とだけでは、[条件付きブレークポイントを使用してオブジェクト ID を追跡](using-breakpoints.md#using-object-ids-in-breakpoint-conditions-c-and-f)できます。

### <a name="pause-code-inside-a-loop-at-a-certain-iteration"></a>特定の反復処理でループ内のコードを一時停止する

**ヒットカウント**を条件として使用して、ブレークポイントを設定します。 詳細については、「[ヒットカウント](using-breakpoints.md#set-a-hit-count-condition)」を参照してください。

### <a name="pause-code-at-the-start-of-a-function-when-you-know-the-function-name-but-not-its-location"></a>関数名がわかっているものの、その位置を把握していないときに、関数の開始時にコードを一時停止します

これを行うには、関数のブレークポイントを使用します。 詳細については、「[関数ブレークポイントの設定](using-breakpoints.md#BKMK_Set_a_breakpoint_in_a_source_file)」を参照してください。

### <a name="pause-code-at-the-start-of-multiple-functions-with-the-same-name"></a>同じ名前の複数の関数の先頭でコードを一時停止します

同じ名前 (オーバーロードされた関数、または異なるプロジェクトの関数) を持つ複数の関数がある場合は、[関数のブレークポイント](using-breakpoints.md#BKMK_Set_a_breakpoint_in_a_source_file)を使用できます。

### <a name="manage-and-keep-track-of-your-breakpoints"></a>ブレークポイントの管理と追跡

**[ブレークポイント]** ウィンドウを使用します。 詳細については、「[ブレークポイントの管理](using-breakpoints.md#BKMK_Specify_advanced_properties_of_a_breakpoint_)」を参照してください。

### <a name="pause-code-and-debug-when-a-specific-handled-or-unhandled-exception-is-thrown"></a>特定の処理済みまたは未処理の例外がスローされたときにコードを一時停止し、デバッグする

例外ヘルパーはエラーが発生した場所を示していますが、特定のエラーを一時停止してデバッグする場合は、[例外がスローされたときにデバッガーを中断するように指示](managing-exceptions-with-the-debugger.md#tell-the-debugger-to-break-when-an-exception-is-thrown)できます。

### <a name="set-a-breakpoint-from-the-call-stack"></a>コールスタックからブレークポイントを設定する

実行フローの検証中にコードを一時停止およびデバッグする場合、または [**呼び出し**履歴] ウィンドウで関数を表示する場合は、「 [[呼び出し履歴] ウィンドウでブレークポイントを設定](using-breakpoints.md#BKMK_Set_a_breakpoint_from_debugger_windows)する」を参照してください。

### <a name="pause-code-at-a-specific-assembly-instruction"></a>特定のアセンブリ命令でコードを一時停止する

これを行うには[、[逆アセンブリ] ウィンドウでブレークポイントを設定](using-breakpoints.md#BKMK_Set_a_breakpoint_from_debugger_windows)します。

## <a name="execute-code"></a>コードの実行

### <a name="learn-the-commands-to-step-through-your-code-while-debugging"></a>デバッグ中にコードをステップ実行するコマンドについて説明します。

詳細については、「[デバッガーでのコード間の移動](navigating-through-code-with-the-debugger.md)」を参照してください。

## <a name="inspect-data"></a>データを検査する

### <a name="check-the-value-of-variables-while-running-your-app"></a>アプリの実行中に変数の値を確認する

[データヒント](view-data-values-in-data-tips-in-the-code-editor.md)を使用して変数をポイントするか[、[自動変数] ウィンドウと [ローカル] ウィンドウで変数を検査](autos-and-locals-windows.md)します。

### <a name="observe-the-changing-value-of-a-specific-variable"></a>特定の変数の値の変更を観察する

変数にウォッチを設定します。 詳細については、「[変数のウォッチ式の設定](watch-and-quickwatch-windows.md)」を参照してください。

### <a name="view-strings-that-are-too-long-for-the-debugger-window"></a>デバッガーウィンドウに長すぎる文字列を表示する

デバッグ中に組み込み[文字列ビジュアライザー](view-strings-visualizer.md)を開きます。

## <a name="configure-debugging"></a>デバッグを構成する

### <a name="customize-information-shown-in-the-debugger"></a>デバッガーに表示される情報をカスタマイズする

オブジェクトの種類以外の情報を、さまざまなデバッガーウィンドウの値として表示することもできます。 、 C#Visual Basic、 F#、およびC++/Cli コードの場合は、[デバッガ display](using-the-debuggerdisplay-attribute.md)属性を使用します。 詳細設定オプションについては、[カスタムビジュアライザー](create-custom-visualizers-of-data.md)を作成して UI をカスタマイズすることもできます。

ネイティブC++の場合は、 [NatVis フレームワーク](create-custom-views-of-native-objects.md)を使用します。

### <a name="configure-debugger-settings"></a>デバッガー設定の構成

デバッガーのオプションとデバッガーのプロジェクト設定を構成するには、「[デバッガーの設定と準備](debugger-settings-and-preparation.md)」を参照してください。

## <a name="additional-tasks"></a>追加のタスク

### <a name="fix-an-exception"></a>例外を修正する

「[例外の修正](write-better-code-with-visual-studio.md#fix-an-exception)」を参照してください。

### <a name="edit-code-during-a-debugging-session"></a>デバッグセッション中のコードの編集

[エディットコンティニュ](edit-and-continue.md)を使用します。 XAML の場合は、 [Xaml ホットリロード](../xaml-tools/xaml-hot-reload.md)を使用します。

### <a name="send-messages-to-the-output-window-without-modifying-code"></a>コードを変更せずに出力ウィンドウにメッセージを送信する

トレースポイントを設定します。 詳細については、「[トレースポイントの使用](using-tracepoints.md)」を参照してください。

## <a name="view-the-order-in-which-functions-are-called"></a>関数が呼び出される順序を表示する

「[呼び出し履歴を表示する方法」を](how-to-use-the-call-stack-window.md)参照してください。

### <a name="debug-on-remote-machines"></a>リモートコンピューターでのデバッグ

「[Remote debugging](remote-debugging.md)」(リモート デバッグ) を参照してください。

### <a name="debug-an-app-that-is-already-running"></a>既に実行されているアプリをデバッグする

「[実行中のプロセスへのアタッチ」を](attach-to-running-processes-with-the-visual-studio-debugger.md)参照してください。

### <a name="debug-multithreaded-applications"></a>マルチスレッド アプリケーションのデバッグ

「[マルチスレッドアプリケーションのデバッグ](debug-multithreaded-applications-in-visual-studio.md)」を参照してください。

### <a name="fix-performance-issues"></a>パフォーマンスの問題を修正

「[プロファイリングツールの概要」を](../profiling/profiling-feature-tour.md)参照してください。