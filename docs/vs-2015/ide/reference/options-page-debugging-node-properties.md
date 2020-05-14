---
title: '[デバッグ] ノード プロパティ ([オプション] ページ) | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
ms.assetid: 564cc8b2-0084-420e-b560-200cc5621a7e
caps.latest.revision: 13
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 10537fb64e6ae0ebbe185024b76442704437e273
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72668843"
---
# <a name="options-page-debugging-node-properties"></a>[デバッグ] ノード プロパティ ([オプション] ページ)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

次の表では、 **[オプション]** ダイアログ ボックスの **[デバッグ]** カテゴリ (`DTE.Properties("Debugging", <Property Page>)`) に関連付けられているページ (またはプロパティ コレクション) について説明します。

## <a name="general"></a>全般
 `DTE.Properties("Debugging", "General")`

|プロパティ項目名|[値]|説明|
|------------------------|-----------|-----------------|
|PromptOnBreakpointDelete|Get/Set (Boolean)|デバッガーでプロジェクト内のすべてのブレークポイントを削除する前に確認を求めるかどうかを指定します。|
|BreakAllProcesses|Get/Set (Boolean)|単一のプロセスが中断するたびに、デバッガーですべてのプロセスを中断するかどうかを指定します。|
|BreakAtBoundaries|Get/Set (Boolean)|例外が AppDomain 間の境界、またはマネージド コードとネイティブ コードとの間の境界を越える場合にデバッガーが実行を中断するかどうかを指定します。|
|EnableAddressLevelDebugging|Get/Set (Boolean)|アドレス レベルのデバッグ機能が有効かどうかを指定します。|
|ShowDisassemblyIfNoSource|Get/Set (Boolean)|ソース コードを使用できない場合にデバッガーが逆アセンブリ コードを表示するかどうかを指定します。|
|EnableBreakpointFilters|Get/Set (Boolean)|ブレークポイント フィルターが有効かどうかを指定します。|
|EnableExceptionAssistant|Get/Set (Boolean)|マネージド例外に例外処理アシスタントを使用するかどうかを指定します。|
|UnwindCallstack|Get/Set (Boolean)|デバッガーが未処理の例外の呼び出し履歴をアンワインドするかどうかを指定します。|
|EnableJustMyCode|Get/Set (Boolean)|C# コードと Visual Basic コード用に "マイ コードのみ" 設定を有効にするかどうかを指定します。|
|ShowAllMembers|Get/Set (Boolean)|非ユーザー オブジェクトの場合は、デバッガーですべてのオブジェクト メンバーを変数ウィンドウに表示するかどうかを指定します。 "マイ コードのみ" 設定が有効になっていないと、このオプションは機能しません。|
|WarnIfNoUserCode|Get/Set (Boolean)|ユーザー コードがないプロセスへのアタッチをユーザーが試みたときにデバッガーで警告を出力するかどうかを指定します。 "マイ コードのみ" 設定が有効になっていないと、このオプションは機能しません。|
|EnablePropertyEvaluation|Get/Set (Boolean)|マネージド コード内のプロパティおよび暗黙的な関数呼び出しをデバッガーで自動的に評価するかどうかを指定します。|
|CallStringConversion|Get/Set (Boolean)|デバッガーで変数ウィンドウ内のオブジェクトに対して文字列変換関数を暗黙的に呼び出すかどうかを指定します。 このオプションは C# コードと JScript コードにのみ適用されます。|
|EnableSourceServer|Get/Set (Boolean)|デバッガーがソース サーバーのコードにアクセスできるかどうかを指定します。|
|PrintSourceServerDiagnostics|Get/Set (Boolean)|ソース サーバーに関連する診断メッセージを出力ウィンドウに表示するかどうかを指定します。 ソース サーバーへのアクセスが有効になっていないと、このオプションは機能しません。|
|HighlightEntireLine|Get/Set (Boolean)|デバッガーでブレークポイントと現在のステートメントの行全体を強調表示するかどうかを指定します。|
|RequireSourceToMatch|Get/Set (Boolean)|デバッグ用にファイルを開いたときに、デバッガーで元のバージョンと完全に一致するソース ファイルを必要とするかどうかを指定します。|
|RedirectOutputToImmediate|Get/Set (Boolean)|出力ウィンドウの出力をイミディエイト ウィンドウにリダイレクトするかどうかを指定します。|
|ShowRawVariableStructure|Get/Set (Boolean)|変数ウィンドウ内のオブジェクトを生の形式で表示するかどうかを指定します。|
|SuppressJitOptimization|Get/Set (Boolean)|マネージド コードの場合は、ジャスト イン タイムの最適化がデバッガーで表示されないようにするかどうかを指定します。|
|WarnIfNoSymbols|Get/Set (Boolean)|プロセスの起動時にデバッグ シンボルを使用できない場合にデバッガーで警告を表示するかどうかを指定します。|
|WarnIfScriptDisabled|Get/Set (Boolean)|プロセスの起動時にスクリプトのデバッグが有効になっていない場合にデバッガーで警告を表示するかどうかを指定します。|
|ShowMarkersForAllThreads|Get/Set (Boolean)|デバッガーでスレッド マーカーを表示するかどうかを指定します。|
|StepOverPropertiesAndOperators|Get/Set (Boolean)|マネージド コードでのみプロパティおよび演算子をステップ オーバーするかどうかを指定します。|

## <a name="edit-and-continue"></a>エディット コンティニュ
 `DTE.Properties("Debugging", "EditAndContinue")`

|プロパティ項目名|[値]|説明|
|------------------------|-----------|-----------------|
|EnableEditAndContinue|Get/Set (Boolean)|エディット コンティニュを有効にするかどうかを指定します。 このオプションは、エディット コンティニュをサポートするすべての言語に適用されます。|
|InvokedByCommands|Get/Set (Boolean)|ユーザーが **[ステップ]** や **[続行]** などのデバッグ コマンドを選択したときに、エディット コンティニュでコード変更を自動的に適用するかどうかを指定します。 このオプションは、ネイティブ コードにのみ適用されます。|
|InvokedByCommandsAskFirst|Get/Set (Boolean)|ユーザーが **[ステップ]** や **[続行]** などのデバッグ コマンドを選択したときに、エディット コンティニュでコード変更の適用を確認するかどうかを指定します。 このオプションは、ネイティブ コードにのみ適用されます。|
|WarnAboutStaleCode|Get/Set (Boolean)|エディット コンティニュを行うと古いコードが実行される場合にデバッガーで警告メッセージを表示するかどうかを指定します。 このオプションは、ネイティブ コードにのみ適用されます。|
|RelinkChangesOnStop|Get/Set (Short)|アプリケーションの実行が停止したときに、エディット コンティニュで適用されたコード変更を Visual Studio で再リンクするかどうかを指定します。 このオプションは、ネイティブ コードにのみ適用されます。|
|AllowPrecompiling|Get/Set (Short)|エディット コンティニュがプリコンパイル済みヘッダーをバックグラウンドで読み込むことができるかどうかを指定します。 このオプションは、ネイティブ コードにのみ適用されます。|

## <a name="just-in-time"></a>Just-In-Time
 `DTE.Properties("Debugging", "JustInTime")`

|プロパティ項目名|[値]|説明|
|------------------------|-----------|-----------------|
|JitManaged|Get/Set (Boolean)|Just-In-Time デバッグをマネージド コード用に有効にするかどうかを指定します。|
|JitNative|Get/Set (Boolean)|Just-In-Time デバッグをネイティブ コード用に有効にするかどうかを指定します。|
|JitScript|Get/Set (Boolean)|Just-In-Time デバッグをスクリプト コード用に有効にするかどうかを指定します。|

## <a name="native"></a>ネイティブ
 `DTE.Properties("Debugging", "Native")`

|プロパティ項目名|[値]|説明|
|------------------------|-----------|-----------------|
|LoadDllExports|Get/Set (Boolean)|デバッガーで DLL エクスポート テーブルを読み込むかどうかを指定します。|
|EnableRPC|Get/Set (Boolean)|デバッガーが COM リモート プロシージャ呼び出しにステップ インできるかどうかを指定します。|

## <a name="see-also"></a>関連項目
 [オプション設定の制御](https://msdn.microsoft.com/library/a09ed242-7494-4cde-bbd1-7a8ec617965d)オプションページの[プロパティ項目の名前を決定する](https://msdn.microsoft.com/library/d450422d-47c7-4eeb-9f9f-3286264bc5aa)オプションページ[、フォントおよび色ノードプロパティ](../../ide/reference/options-page-fonts-and-colors-node-properties.md)の[オプションページ、[テキストエディター] ノードプロパティ](../../ide/reference/options-page-text-editor-node-properties.md)の[[全般] ([オプション] ダイアログボックス-[デバッグ])](../../debugger/general-debugging-options-dialog-box.md)[エディットコンティニュ] ([[オプション] ダイアログボックス](https://msdn.microsoft.com/library/009d225f-ef65-463f-a146-e4c518f86103) [-[just-in-time])](../../debugger/just-in-time-debugging-options-dialog-box.md) ([オプション] ダイアログボックス-[デバッグ])
