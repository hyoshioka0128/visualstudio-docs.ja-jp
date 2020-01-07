---
title: コマンドのエイリアス
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- aliases, Visual Studio commands
- Visual Studio, commands
- predefined command aliases
- commands, aliases
- Visual Studio commands
- pre-defined command aliases
- command aliases
ms.assetid: de8bb378-8c1c-4087-a9a5-537fa8314c19
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f56161e1fd89ce29924368b6029ee12c17e75a65
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72747699"
---
# <a name="visual-studio-command-aliases"></a>Visual Studio Command Aliases

コマンド エイリアスを利用すると、コマンドを実行するとき、入力する文字が少なくなります。 **[検索/コマンド]** ボックスまたは **[コマンド]** ウィンドウにエイリアスを入力します。 たとえば、 **[ファイルを開く]** ダイアログ ボックスを表示するときに、「`>File.OpenFile`」ではなく、定義済みのエイリアス「`>of`」を入力できます。

**[コマンド]** ウィンドウで「`alias`」と入力すると、現在のエイリアスとその定義の一覧が表示されます。 **[コマンド]** ウィンドウの内容を消去するには、「`>cls`」と入力します。 特定のコマンドのエイリアスを表示するには、「`alias <command name>`」と入力します。

いずれかの Visual Studio コマンド (引数の有無を問わず) について、独自のエイリアスを作成する操作は簡単です。 たとえば、`File.NewFile MyFile.txt` のエイリアスを作成する構文は、「`alias MyAlias File.NewFile MyFile.txt`」です。 特定のエイリアスを削除するには、「`alias <alias name> /delete`」を使用します。

次の表は、Visual Studio コマンドの定義済みエイリアスを示しています。 一部のコマンド名には、複数の定義済みのエイリアスがあります。 表のコマンド名のリンクをクリックすると、コマンドの正しい構文、引数、スイッチについて説明したトピックが表示されます。

|コマンド名|Alias|完全な名前|
|------------------|-----------|-------------------|
|[Print コマンド](../../ide/reference/print-command.md)|?|Debug.Print|
|[QuickWatch コマンド](../../ide/reference/quick-watch-command.md)|??|Debug.QuickWatch|
|新しいプロジェクトの追加|AddProj|File.AddNewProject|
|[Alias コマンド](../../ide/reference/alias-command.md)|Alias|Tools.Alias|
|[自動変数] ウィンドウ|Autos|Debug.Autos|
|[ブレークポイント] ウィンドウ|bl|Debug.Breakpoints|
|ブレークポイントの設定/解除|bp|Debug.ToggleBreakpoint|
|[呼び出し履歴] ウィンドウ|CallStack|Debug.CallStack|
|[ブックマークをクリア]|ClearBook|Edit.ClearBookmarks|
|閉じる|閉じる|File.Close|
|[すべてのドキュメントを閉じる]|CloseAll|Window.CloseAllDocuments|
|[すべてクリア]|cls|Edit.ClearAll|
|[コマンド ウィンドウ]|cmd|View.CommandWindow|
|[コードの表示]|code|View.ViewCode|
|[ListMemory コマンド](../../ide/reference/list-memory-command.md)|d|Debug.ListMemory|
|[メモリの一覧表示コマンド](../../ide/reference/list-memory-command.md) (ANSI 形式)|da|Debug.ListMemory /Ansi|
|[メモリの一覧表示コマンド](../../ide/reference/list-memory-command.md) (1 バイト形式)|db|Debug.ListMemory /Format:OneByte|
|[メモリの一覧表示コマンド](../../ide/reference/list-memory-command.md) (4 バイトの ANSI 形式)|dc|Debug.ListMemory /Format:FourBytes /Ansi|
|[メモリの一覧表示コマンド](../../ide/reference/list-memory-command.md) (4 バイト形式)|dd|Debug.ListMemory /Format:FourBytes|
|[BOL まで削除]|DelBOL|Edit.DeleteToBOL|
|[EOL まで削除]|DelEOL|Edit.DeleteToEOL|
|[左右スペースの削除]|DelHSp|Edit.DeleteHorizontalWhitespace|
|[デザイナーの表示]|designer|View.ViewDesigner|
|[メモリの一覧表示コマンド](../../ide/reference/list-memory-command.md) (float 形式)|df|Debug.ListMemory /Format:Float|
|[逆アセンブリ] ウィンドウ|disasm|Debug.Disassembly|
|[メモリの一覧表示コマンド](../../ide/reference/list-memory-command.md) (8 バイト形式)|dq|Debug.ListMemory /Format:EightBytes|
|[メモリの一覧表示コマンド](../../ide/reference/list-memory-command.md) (Unicode 形式)|du|Debug.ListMemory /Unicode|
|[Evaluate Statement コマンド](../../ide/reference/evaluate-statement-command.md)|eval|Debug.EvaluateStatement|
|終了|終了|File.Exit|
|[書式の選択]|format|Edit.FormatSelection|
|全画面表示|FullScreen|View.FullScreen|
|[Start コマンド](../../ide/reference/start-command.md)|G|Debug.Start|
|[Go To コマンド](../../ide/reference/go-to-command.md)|GotoLn|Edit.GoTo|
|[かっこに移動]|GotoBrace|Edit.GotoBrace|
|F1 ヘルプ|ヘルプ|Help.F1Help|
|[イミディエイト モード]|immed|Tools.ImmediateMode|
|[テキストとしてファイルを挿入]|InsertFile|Edit.InsertFileAsText|
|[ListCallStack コマンド](../../ide/reference/list-call-stack-command.md)|kb|Debug.ListCallStack|
|[小文字に変換]|Lcase|Edit.MakeLowercase|
|[行の切り取り]|LineCut|Edit.LineCut|
|[行の削除]|LineDel|Edit.LineDelete|
|リスト メンバー|ListMembers|Edit.ListMembers|
|[ローカル] ウィンドウ|Locals|Debug.Locals|
|[LogCommandWindowOutput コマンド](../../ide/reference/log-command-window-output-command.md)|ログ|Tools.LogCommandWindowOutput|
|[コマンド ウィンドウ マーク モード]|mark|Tools.CommandWindowMarkMode|
|[メモリ 1] ウィンドウ|Memory Memory1|Debug.Memory1|
|[メモリ 2] ウィンドウ|Memory2|Debug.Memory2|
|[メモリ 3] ウィンドウ|Memory3|Debug.Memory3|
|[メモリ 4] ウィンドウ|Memory4|Debug.Memory4|
|[SetRadix コマンド基数の設定コマンド](../../ide/reference/set-radix-command.md)|n|Debug.SetRadix|
|[ShowWebBrowser コマンド](../../ide/reference/showwebbrowser-command.md)|nav navigate|View.ShowWebBrowser|
|[次のブックマーク]|NextBook|Edit.NextBookmark|
|[NewFile コマンド](../../ide/reference/new-file-command.md)|nf|File.NewFile|
|新しいプロジェクト|np NewProj|File.NewProject|
|[OpenFile コマンド](../../ide/reference/open-file-command.md)|of Open|File.OpenFile|
|[OpenProject コマンド](../../ide/reference/open-project-command.md)|op|File.OpenProject|
|[定義に縮小]/[アウトラインの中止]|OutlineDefs StopOutlining|Edit.CollapseToDefinitions|
|[ステップ オーバー]|p|Debug.StepOver|
|[パラメーター ヒント]|ParamInfo|Edit.ParameterInfo|
|[ステップ アウト]|pr|Debug.StepOut|
|[前のブックマーク]|PrevBook|Edit.PreviousBookmark|
|[印刷]|print|File.Print|
|プロパティ ウィンドウ|props|View.PropertiesWindow|
|停止|q|Debug.StopDebugging|
|やり直し|redo|Edit.Redo|
|[レジスタ] ウィンドウ|registers|Debug.Registers|
|[カーソル行の前まで実行]|rtc|Debug.RunToCursor|
|[選択されたファイルを上書き保存]|save|File.SaveSelectedItems|
|[Save All]|SaveAll|File.SaveAll|
|名前を付けて保存|SaveAs|File.SaveSelectedItemsAs|
|[Shell コマンド](../../ide/reference/shell-command.md)|shell|Tools.Shell|
|[検索の中止]|StopFind|Edit.FindInFiles /stop|
|[アンカー位置の交換]|SwapAnchor|Edit.SwapAnchor|
|[ステップ イン]|t|Debug.StepInto|
|[選択範囲にタブを設定]|tabify|Edit.TabifySelection|
|[タスク一覧] ウィンドウ|TaskList|View.TaskList|
|[スレッド] ウィンドウ|スレッド|Debug.Threads|
|[上下に並べて表示]|TileH|Window.TileHorizontally|
|[左右に並べて表示]|TileV|Window.TileVertically|
|[ブックマークの設定解除]|ToggleBook|Edit.ToggleBookmark|
|[ツールボックス] ウィンドウ|toolbox|View.Toolbox|
|[ListDisassembly コマンド](../../ide/reference/list-disassembly-command.md)|u|Debug.ListDisassembly|
|[大文字に変換]|Ucase|Edit.MakeUppercase|
|元に戻す|undo|Edit.Undo|
|[選択範囲のタブの設定を解除]|Untabify|Edit.UntabifySelection|
|[ウォッチ] ウィンドウ|Watch|Debug.WatchN|
|[[右端で折り返す] の設定/解除]|WordWrap|Edit.ToggleWordWrap|
|[プロセスの一覧]|&#124;|Debug.ListProcesses|
|[ListThreads コマンド](../../ide/reference/list-threads-command.md)|~ ~*k ~\*kb|Debug.ListThreads Debug.ListTheads /AllThreads|

## <a name="see-also"></a>関連項目

- [Visual Studio のコマンド](../../ide/reference/visual-studio-commands.md)
- [コマンド ウィンドウ](../../ide/reference/command-window.md)
- [検索コマンド ボックス](../../ide/find-command-box.md)
