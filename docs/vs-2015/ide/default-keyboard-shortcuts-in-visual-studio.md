---
title: 既定のキーボード ショートカット
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- shortcut keys [Visual Studio], keyboard binding schemes
- keyboard binding schemes [Visual Studio]
- Help [Visual Studio], shortcut keys
- keyboard shortcuts [Visual Studio], keyboard binding schemes
- keyboard shortcuts
ms.assetid: c2c64648-00f8-4e48-a8a0-96c67cfd968c
caps.latest.revision: 59
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 2fb9fa4d9c4faaf01ec64e9eb722af8589de5588
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85548097"
---
# <a name="default-keyboard-shortcuts-in-visual-studio"></a>Visual Studio の既定のキーボード ショートカット
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio のさまざまなコマンドやウィンドウには、該当するショートカット キーを押すことで、より簡単にアクセスできます。 このトピックでは、Visual Studio のインストール時に選択できる [全般的な開発設定] プロファイルの既定のショートカット キーを示しています。 選択したプロファイルにかかわらず、 [オプション] ダイアログ ボックスを開き、 **[環境]** ノードを展開して、 **[キーボード]** を選択することで、コマンドの**ショートカットを確認する**ことができます。 また、別のショートカット キーを任意のコマンドに割り当てることで、ショートカット キーをカスタマイズすることもできます。

 一般的なショートカット キーの一覧、およびその他の生産性向上に関する情報については、「[ヒントとテクニック](../ide/tips-and-tricks-for-visual-studio.md)」および「[生産性に関するヒント](../ide/productivity-tips-for-visual-studio.md)」を参照してください。

 次の一覧のセクションには、Visual Studio の任意の場所からキーボードショートカットを使用してアクセスできる、でグローバルなコマンドが含まれています。

- [解析](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_analyze)
- [編集](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_edit)
- [プロジェクト](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_project)
- [テスト](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_test)|
- [アーキテクチャ](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_architecture)
- [エディターコンテキストメニュー](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_editorContext)
- [プロジェクトとソリューションのコンテキストメニュー](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_projectContext)
- [テスト エクスプローラー](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_testexplorerGLOBAL)
- [ビルド](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_build)
- [ファイル](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_file)
- [リファクター](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_refactor)
- [ツール](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_tools)
- [クラスビューコンテキストメニュー](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_classview)
- [ヘルプ](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_help)
- [ソリューション エクスプローラー](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_solutionexplorerGLOBAL)
- [表示](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_view)
- [デバッグ](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_debug)
- [ロードテスト](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_loadtest)
- [チーム](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_team)
- [ウィンドウ](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_window)
- [デバッガーコンテキストメニュー](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_debugger)
- [その他のコンテキストメニュー](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_otherContext)
- [Team Foundation コンテキストメニュー](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_TFcontext)
- [Azure](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_windowsazure)
- [診断ハブ](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_diagnostics)

 次の一覧の各セクションには、セクションの名前が付けられているコンテキストに固有のキーボードショートカットのコマンドが含まれています。

- [ADO.NET Entity Data Model デザイナー](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_ADONET)
- [レイヤー図](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_layerDiagram)
- [設定デザイナー](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_SettingsDesigner)
- [VC イメージ エディター](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_vcimageeditor)
- [クラスダイアグラム](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_classDiagram)
- [マネージド リソース エディター](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_managedResources)
- [ソリューション エクスプローラー](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_SolutionExplorer)
- [VC ストリング エディター](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_vcstringeditor)
- [コード化された UI テスト エディター](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_codedUItest)
- [マージエディターウィンドウ](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_MergeEditor)
- [チーム エクスプローラー](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_TeamExplorer)
- [ビュー デザイナー](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_viewDesigner)
- [データセット エディター](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_dataset)
- [Microsoft SQL Server Data Tools、スキーマの比較](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_SchemaCompare)
- [Team Foundation ビルド詳細エディター](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_TFBuild)
- [Visual Studio](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_visualstudio)
- [相違ビューアー](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_diff)
- [Microsoft SQL Server Data Tools、テーブル デザイナー](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_TableDesigner)
- [テスト エクスプローラー](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_TestExplorer)
- [Windows フォーム デザイナー](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_wfdesigner)
- [DOM Explorer](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_DOM)
- [Microsoft SQL Server Data Tools、T-SQL エディター](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_TSQLeditor)
- [テキストエディター](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_TextEditor)
- [作業項目エディター](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_workItemEditor)
- [F# Interactive](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_FSharp)
- [Microsoft SQL Server Data Tools、T-SQL PDW エディター](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_linkfix)
- [UML アクティビティ図](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_UMLactivityDiagram)
- [作業項目クエリ ビュー](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_WIqueryview)
- [グラフ ドキュメント エディター](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_graphDoc)
- [Page Inspector](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_PageInspector)
- [UML クラス図](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_UMLclassDiagram)
- [作業項目結果ビュー](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_WIresultsview)
- [グラフィックス診断](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_graphicsDebugger)
- [クエリ デザイナー](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_QueryDesigner)
- [UML コンポーネント図](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_UMLcomponentDiagram)
- [ワークフロー デザイナー](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_workflowdesigner)
- [HTML エディター](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_HTMLeditor)
- [クエリ結果](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_QueryResults)
- [UML ユースケース図](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_UMLusecaseDiagram)
- [XAML デザイナー](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_xamluidesigner)
- [HTML エディター デザイン ビュー](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_HTMLeditorDesign)
- [レポート デザイナー](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_ReportDesigner)
- [VC アクセラレータ エディター](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_vcaccelerator)
- [XML (テキスト) エディター](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_xmlTextEditor)
- [HTML エディター ソース ビュー](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_HTMLeditorSource)
- [シーケンス図](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_SequenceDiagram)
- [VC ダイアログ エディター](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_vcdialogeditor)
- [XML スキーマ デザイナー](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_xmlSchemaDesigner)

## <a name="global"></a><a name="bkmk_global"></a> 全体

### <a name="analyze"></a><a name="bkmk_analyze"></a> 解析

|コマンド|キーボード ショートカット|
|--------------|------------------------|
|Analyze.NavigateBackward|Shift + Alt + 3|
|Analyze.NavigateForward|Shift + Alt + 4|

### <a name="architecture"></a><a name="bkmk_architecture"></a> アーキテクチャ

|コマンド|キーボード ショートカット|
|--------------|------------------------|
|Architecture.NewDiagram|Ctrl + \\、Ctrl + N|

### <a name="build"></a><a name="bkmk_build"></a> ビルド

|コマンド|キーボード ショートカット|
|--------------|------------------------|
|Build.BuildSolution|Ctrl + Shift + B|
|Build.Cancel|Ctrl + Break|
|Build.Compile|Ctrl + F7|
|Build.RunCodeAnalysisonSolution|Alt + F11|

### <a name="class-view-context-menus"></a><a name="bkmk_classview"></a> クラスビューコンテキストメニュー

|コマンド|キーボード ショートカット|
|--------------|------------------------|
|ClassViewContextMenus.ClassViewMultiselectProjectreferencesItems.Properties|Alt + Enter|

### <a name="debug"></a><a name="bkmk_debug"></a> デバッグ

|コマンド|キーボード ショートカット|
|--------------|------------------------|
|Debug.ApplyCodeChanges|Alt + F10|
|Debug.Autos|Ctrl + Alt + V、A|
|Debug.BreakAll|Ctrl + Alt + Break|
|Debug.BreakatFunction|Ctrl + B|
|Debug.Breakpoints|Ctrl+Alt+B|
|Debug.CallStack|Ctrl + Alt + C|
|Debug.DeleteAllBreakpoints|Ctrl + Shift + F9|
|Debug.DiagnosticsHub.Launch|Alt + F2|
|Debug.Disassembly|Ctrl + Alt + D|
|Debug.DOMExplorer|Ctrl + Alt + V、D|
|Debug.EnableBreakpoint|Ctrl + F9|
|Debug.Exceptions|Ctrl+Alt+E|
|Debug.GoToPreviousCallorIntelliTraceEvent|Ctrl + Shift + F11|
|Debug.Graphics.StartDiagnostics|Alt + F5|
|Debug.Immediate|Ctrl + Alt + I|
|Debug.IntelliTraceCalls|Ctrl + Alt + Y、T|
|Debug.IntelliTraceEvents|Ctrl + Alt + Y、F|
|Debug.JavaScriptConsole|Ctrl + Alt + V、C|
|Debug.Locals|Ctrl + Alt + V、L|
|Debug.LocationToolbar.ProcessCombo|Ctrl + 数字 5|
|Debug.LocationToolbar.StackFrameCombo|Ctrl + 数字 7|
|Debug.LocationToolbar.ThreadCombo|Ctrl + 数字 6|
|Debug.LocationToolbar.ToggleCurrentThreadFlaggedState|Ctrl + 数字 8|
|Debug.LocationToolbar.ToggleFlaggedThreads|Ctrl + 数字 9|
|Debug.Memory1|Ctrl + Alt + M、1|
|Debug.Memory2|Ctrl + Alt + M、2|
|Debug.Memory3|Ctrl + Alt + M、3|
|Debug.Memory4|Ctrl + Alt + M、4|
|Debug.Modules|Ctrl + Alt + U|
|Debug.ParallelStacks|Ctrl + Shift + D、S|
|Debug.ParallelWatch1|Ctrl + Shift + D、1|
|Debug.ParallelWatch2|Ctrl + Shift + D、2|
|Debug.ParallelWatch3|Ctrl + Shift + D、3|
|Debug.ParallelWatch4|Ctrl + Shift + D、4|
|Debug.Processes|Ctrl+Alt+Z|
|Debug.QuickWatch|Shift + F9<br /><br /> or<br /><br /> Ctrl+Alt+Q|
|Debug.RefreshWindowsapp|Ctrl + Shift + R|
|Debug.Registers|Ctrl + Alt + G|
|Debug.Restart|Ctrl + Shift + F5|
|Debug.RunToCursor|Ctrl + F10|
|Debug.SetNextStatement|Ctrl + Shift + F10|
|Debug.ShowCallStackonCodeMap|Ctrl + Shift + `|
|Debug.ShowNextStatement|Alt + Num *|
|Debug.Start|F5|
|Debug.StartWindowsPhoneApplicationAnalysis|Alt + F1|
|Debug.StartWithoutDebugging|Ctrl + F5|
|Debug.StepInto|F11|
|Debug.StepIntoCurrentProcess|Ctrl + Alt + F11|
|Debug.StepIntoSpecific|Shift + Alt + F11|
|Debug.StepOut|Shift + F11|
|Debug.StepOutCurrentProcess|Ctrl + Shift + Alt + F11|
|Debug.StepOver|F10|
|Debug.StepOverCurrentProcess|Ctrl + Alt + F10|
|Debug.StopDebugging|Shift + F5|
|Debug.StopPerformanceAnalysis|Shift + Alt + F2|
|Debug.Tasks|Ctrl + Shift + D、K|
|Debug.Threads|Ctrl + Alt + H|
|Debug.ToggleBreakpoint|F9|
|Debug.ToggleDisassembly|Ctrl + F11|
|Debug.Watch1|Ctrl + Alt + W、1|
|Debug.Watch2|Ctrl + Alt + W、2|
|Debug.Watch3|Ctrl + Alt + W、3|
|Debug.Watch4|Ctrl + Alt + W、4|

### <a name="debugger-context-menus"></a><a name="bkmk_debugger"></a> デバッガーコンテキストメニュー

|コマンド|キーボード ショートカット|
|--------------|------------------------|
|DebuggerContextMenus.BreakpointsWindow.Delete|Alt + F9、D|
|DebuggerContextMenus.BreakpointsWindow.GoToDisassembly|Alt + F9、A|
|DebuggerContextMenus.BreakpointsWindow.GoToSourceCode|Alt + F9、S|

### <a name="diagnostics-hub"></a><a name="bkmk_diagnostics"></a> 診断ハブ

|コマンド|ショートカット キー|
|-------------|-----------------------|
|DiagnosticsHub.StopCollection|Ctrl + Alt + F2|

### <a name="edit"></a><a name="bkmk_edit"></a> 編集

|コマンド||
|--------------|-|
|Edit.Copy|Ctrl+C<br /><br /> or<br /><br /> Ctrl + Ins|
|Edit.Cut|Ctrl + X<br /><br /> or<br /><br /> Shift + Delete|
|Edit.CycleClipboardRing|Ctrl + Shift + V<br /><br /> or<br /><br /> Ctrl + Shift + Ins|
|Edit.Delete|削除|
|Edit.Find|Ctrl + F|
|Edit.FindAllReferences|Shift + F12|
|Edit.FindinFiles|Ctrl + Shift + F|
|Edit.FindNext|F3|
|Edit.FindNextSelected|Ctrl + F3|
|Edit.FindPrevious|Shift + F3|
|Edit.FindPreviousSelected|Ctrl + Shift + F3|
|Edit.GenerateMethod|Ctrl + K、Ctrl + M|
|Edit.GoTo|Ctrl + G|
|Edit.GoToDeclaration|Ctrl + F12|
|Edit.GoToDefinition|F12|
|Edit.GoToFindCombo|Ctrl + D|
|Edit.GoToNextLocation|F8|
|Edit.GoToPrevLocation|Shift + F8|
|Edit.InsertSnippet|Ctrl + K、Ctrl + X|
|Edit.MoveControlDown|Ctrl + ↓|
|Edit.MoveControlDownGrid|↓ キー|
|Edit.MoveControlLeft|Ctrl + ←|
|Edit.MoveControlLeftGrid|←|
|Edit.MoveControlRight|Ctrl + →|
|Edit.MoveControlRightGrid|→ キー|
|Edit.MoveControlUp|Ctrl + ↑|
|Edit.MoveControlUpGrid|↑ キー|
|Edit.NavigateTo|Ctrl + ,|
|Edit.NextBookmark|Ctrl + K、Ctrl + N|
|Edit.NextBookmarkInFolder|Ctrl + Shift + K、Ctrl + Shift + N|
|Edit.OpenFile|Ctrl + Shift + G|
|Edit.Paste|Ctrl + V<br /><br /> or<br /><br /> Shift + Ins|
|Edit.PreviousBookmark|Ctrl + K、Ctrl + P|
|Edit.PreviousBookmarkInFolder|Ctrl + Shift + K、Ctrl + Shift + P|
|Edit.QuickFindSymbol|Shift + Alt + F12|
|Edit.Redo|Ctrl + Y<br /><br /> or<br /><br /> Ctrl + Shift + Z<br /><br /> or<br /><br /> Shift + Alt + Backspace|
|Edit.RefreshRemoteReferences|Ctrl + Shift + J|
|Edit.Replace|Ctrl + H|
|Edit.ReplaceinFiles|Ctrl + Shift + H|
|Edit.SelectAll|Ctrl + A|
|Edit.SelectNextControl|タブ|
|Edit.SelectPreviousControl|Shift + Tab|
|Edit.ShowTileGrid|次に、|
|Edit.SizeControlDown|Ctrl + Shift + ↓|
|Edit.SizeControlDownGrid|Shift + ↓|
|Edit.SizeControlLeft|Ctrl + Shift + ←|
|Edit.SizeControlLeftGrid|Shift + ←|
|Edit.SizeControlRight|Ctrl + Shift + →|
|Edit.SizeControlRightGrid|Shift + →|
|Edit.SizeControlUp|Ctrl + Shift + ↑|
|Edit.SizeControlUpGrid|Shift + ↑|
|Edit.StopSearch|Alt + F3、S|
|Edit.SurroundWith|Ctrl + K、Ctrl + S|
|Edit.Undo|Ctrl + Z<br /><br /> or<br /><br /> Alt + Backspace|

### <a name="editor-context-menus"></a><a name="bkmk_editorContext"></a> エディターコンテキストメニュー

|コマンド|キーボード ショートカット|
|--------------|------------------------|
|EditorContextMenus.CodeWindow.Breakpoint.BreakpointEditlabels|Alt + F9、L|
|EditorContextMenus.CodeWindow.CodeMap.ShowItem|Ctrl + `|
|EditorContextMenus.CodeWindow.Execute|Ctrl + Alt + F5|
|EditorContextMenus.CodeWindow.GoToView|Ctrl + M、Ctrl + G|
|EditorContextMenus.CodeWindow.ToggleHeaderCodeFile|Ctrl + K、Ctrl + O|
|EditorContextMenus.CodeWindow.ViewCallHierarchy|Ctrl + K、Ctrl + T<br /><br /> or<br /><br /> Ctrl + K、T|

### <a name="file"></a><a name="bkmk_file"></a> ファイル

|コマンド|キーボード ショートカット|
|--------------|------------------------|
|File.Exit|Alt + F4|
|File.NewFile|Ctrl + N|
|File.NewProject|Ctrl + Shift + N|
|File.NewWebSite|Shift + Alt + N|
|File.OpenFile|Ctrl + O|
|File.OpenProject|Ctrl + Shift + O|
|File.OpenWebSite|Shift + Alt + O|
|File.Print|Ctrl + P|
|File.SaveAll|Ctrl + Shift + S|
|File.SaveSelectedItems|Ctrl + S|
|File.ViewinBrowser|Ctrl + Shift + W|

### <a name="help"></a><a name="bkmk_help"></a> ヘルプ

|コマンド|キーボード ショートカット|
|--------------|------------------------|
|Help.AddandRemoveHelpContent|Ctrl + Alt + F1|
|Help.F1Help|F1|
|Help.ViewHelp|Ctrl + F1|
|Help.WindowHelp|Shift + F1|

### <a name="load-test"></a><a name="bkmk_loadtest"></a> ロードテスト

|コマンド|ショートカット キー|
|-------------|-----------------------|
|LoadTest.JumpToCounterPane|Ctrl + R、Q|

### <a name="other-context-menus"></a><a name="bkmk_otherContext"></a> その他のコンテキストメニュー

|コマンド|ショートカット キー|
|-------------|-----------------------|
|OtherContextMenus.MicrosoftDataEntityDesignContext.AddNewDiagram|挿入|

### <a name="project"></a><a name="bkmk_project"></a> プロジェクト

|コマンド|キーボード ショートカット|
|--------------|------------------------|
|Project.AddExistingItem|Shift + Alt + A|
|Project.AddNewItem|Ctrl + Shift + A|
|Project.ClassWizard|Ctrl + Shift + X|
|Project.Override|Ctrl + Alt + Ins|
|Project.Previewchanges|Alt + ;、Alt + C|
|Project.Publishselectedfiles|Alt + ;、Alt + P|
|Project.Replaceselectedfilesfromserver|Alt + ;、Alt + R|

### <a name="project-and-solution-context-menus"></a><a name="bkmk_projectContext"></a> プロジェクトとソリューションのコンテキストメニュー

|コマンド|キーボード ショートカット|
|--------------|------------------------|
|ProjectandSolutionContextMenus.Item.MoveDown|Alt + ↓|
|ProjectandSolutionContextMenus.Item.MoveUp|Alt + ↑|

### <a name="refactor"></a><a name="bkmk_refactor"></a> リファクター

|コマンド|キーボード ショートカット|
|--------------|------------------------|
|Refactor.EncapsulateField|Ctrl + R、Ctrl + E|
|Refactor.ExtractInterface|Ctrl + R、Ctrl + I|
|Refactor.ExtractMethod|Ctrl + R、Ctrl + M|
|Refactor.RemoveParameters|Ctrl + R、Ctrl + V|
|Refactor.Rename|Ctrl + R、Ctrl + R|
|Refactor.ReorderParameters|Ctrl + R、Ctrl + O|

### <a name="solution-explorer"></a><a name="bkmk_solutionexplorerGLOBAL"></a> ソリューション エクスプローラー

|コマンド|キーボード ショートカット|
|--------------|------------------------|
|SolutionExplorer.OpenFilesFilter|Ctrl + [、O<br /><br /> or<br /><br /> Ctrl + [、Ctrl + O|
|SolutionExplorer.PendingChangesFilter|Ctrl + [、P<br /><br /> or<br /><br /> Ctrl + [、Ctrl + P|
|SolutionExplorer.SyncWithActiveDocument|Ctrl + [、S<br /><br /> or<br /><br /> Ctrl + [、Ctrl + S|

### <a name="team"></a><a name="bkmk_team"></a> チーム

|コマンド|キーボード ショートカット|
|--------------|------------------------|
|Team.Git.GoToGitBranches|Ctrl + 0、Ctrl + N<br /><br /> or<br /><br /> Ctrl + 0、N|
|Team.Git.GoToGitChanges|Ctrl + 0、Ctrl + G<br /><br /> or<br /><br /> Ctrl + 0、G|
|Team.Git.GoToGitCommits|Ctrl + 0、Ctrl + O<br /><br /> or<br /><br /> Ctrl + 0、O|
|Team.TeamExplorerSearch|Ctrl + '|

### <a name="team-foundation-context-menus"></a><a name="bkmk_TFcontext"></a> Team Foundation コンテキストメニュー

|コマンド|キーボード ショートカット|
|--------------|------------------------|
|TeamFoundationContextMenus.Commands.GoToBuilds|Ctrl + 0、Ctrl + B<br /><br /> or<br /><br /> Ctrl + 0、B|
|TeamFoundationContextMenus.Commands.GoToConnect|Ctrl + 0、Ctrl + C<br /><br /> or<br /><br /> Ctrl + 0、C|
|TeamFoundationContextMenus.Commands.GoToDocuments|Ctrl + 0、Ctrl + D<br /><br /> or<br /><br /> Ctrl + 0、D|
|TeamFoundationContextMenus.Commands.GoToHome|Ctrl + 0、Ctrl + H<br /><br /> or<br /><br /> Ctrl + 0、H|
|TeamFoundationContextMenus.Commands.GoToMyWork|Ctrl + 0、Ctrl + M<br /><br /> or<br /><br /> Ctrl + 0、M|
|TeamFoundationContextMenus.Commands.GoToPendingChanges|Ctrl + 0、Ctrl + P<br /><br /> or<br /><br /> Ctrl + 0、P|
|TeamFoundationContextMenus.Commands.GoToReports|Ctrl + 0、Ctrl + R<br /><br /> or<br /><br /> Ctrl + 0、R|
|TeamFoundationContextMenus.Commands.GoToSettings|Ctrl + 0、Ctrl + S<br /><br /> or<br /><br /> Ctrl + 0、S|
|TeamFoundationContextMenus.Commands.GoToWebAccess|Ctrl + 0、Ctrl + A<br /><br /> or<br /><br /> Ctrl + 0、A|
|TeamFoundationContextMenus.Commands.GoToWorkItems|Ctrl + 0、Ctrl + W<br /><br /> or<br /><br /> Ctrl + 0、W|

### <a name="test"></a><a name="bkmk_test"></a> テスト

|コマンド|キーボード ショートカット|
|--------------|------------------------|
|Test.UseCodedUITestBuilder|Ctrl + \\、Ctrl + C|
|Test.UseExistingActionRecording|Ctrl + \\、Ctrl + A|

### <a name="test-explorer"></a><a name="bkmk_testexplorerGLOBAL"></a> テスト エクスプローラー

|コマンド|キーボード ショートカット|
|--------------|------------------------|
|TestExplorer.DebugAllTests|Ctrl + R、Ctrl + A|
|TestExplorer.DebugAllTestsInContext|Ctrl + R、Ctrl + T|
|TestExplorer.RepeatLastRun|Ctrl + R、L|
|TestExplorer.RunAllTests|Ctrl + R、A|
|TestExplorer.RunAllTestsInContext|Ctrl + R、T|

### <a name="tools"></a><a name="bkmk_tools"></a> ツール

|コマンド|キーボード ショートカット|
|--------------|------------------------|
|Tools.AttachtoProcess|Ctrl+Alt+P|
|Tools.CodeSnippetsManager|Ctrl + K、Ctrl + B|
|Tools.ForceGC|Ctrl + Shift + Alt + F12、Ctrl + Shift + Alt + F12|
|Tools.GoToCommandLine|Ctrl + /|

### <a name="view"></a><a name="bkmk_view"></a> 表示

|コマンド|キーボード ショートカット|
|--------------|------------------------|
|View.AllWindows|Shift + Alt + M|
|View.ArchitectureExplorer|Ctrl + \\、Ctrl + R|
|View.Backward|Alt + ← キー|
|View.BookmarkWindow|Ctrl + K、Ctrl + W|
|View.BrowseNext|Ctrl + Shift + 数字 1|
|View.BrowsePrevious|Ctrl + Shift + 数字 2|
|View.CallHierarchy|Ctrl + Alt + K|
|View.ClassView|Ctrl + Shift + C|
|View.ClassViewGoToSearchCombo|Ctrl + K、Ctrl + V|
|View.CodeDefinitionWindow|Ctrl + \\、D<br /><br /> or<br /><br /> Ctrl + \\、Ctrl + D|
|View.CommandWindow|Ctrl + Alt + A|
|View.DataSources|Shift + Alt + D|
|View.DocumentOutline|Ctrl + Alt + T|
|View.EditLabel|F2|
|View.ErrorList|Ctrl + \\、E<br /><br /> or<br /><br /> Ctrl + \\、Ctrl + E|
|View.F#Interactive|Ctrl+Alt+F|
|View.FindSymbolResults|Ctrl + Alt + F12|
|View.Forward|Alt + → キー|
|View.ForwardBrowseContext|Ctrl + Shift + 7|
|View.FullScreen|Shift + Alt + Enter|
|View.NavigateBackward|Ctrl + -|
|View.NavigateForward|Ctrl + Shift + -|
|View.NextError|Ctrl + Shift + F12|
|View.Notifications|Ctrl + W、N<br /><br /> or<br /><br /> Ctrl + W、Ctrl + N|
|View.ObjectBrowser|Ctrl + Alt + J|
|View.ObjectBrowserGoToSearchCombo|Ctrl + K、Ctrl + R|
|View.Output|Ctrl + Alt + O|
|View.PopBrowseContex|Ctrl + Shift + 8|
|View.PropertiesWindow|F4|
|View.PropertyPages|Shift + F4|
|View.ResourceView|Ctrl + Shift + E|
|View.ServerExplorer|Ctrl+Alt+S|
|View.ShowSmartTag|Shift + Alt + F10<br /><br /> or<br /><br /> Ctrl + .|
|View.SolutionExplorer|Ctrl + Alt + L|
|View.SQLServerObjectExplorer|Ctrl + \\、Ctrl + S|
|View.TaskList|Ctrl + \\、T<br /><br /> or<br /><br /> Ctrl + \\、Ctrl + T|
|View.TfsTeamExplorer|Ctrl + \\、Ctrl + M|
|View.Toolbox|Ctrl + Alt + X|
|View.UMLModelExplorer|Ctrl + \\、Ctrl + U|
|View.ViewCode|F7|
|View.ViewDesigner|Shift + F7|
|View.WebBrowser|Ctrl+Alt+R|
|View.ZoomIn|Ctrl + Shift + .|
|View.ZoomOut|Ctrl + Shift + ,|

### <a name="window"></a><a name="bkmk_window"></a> ウィンドウ

|コマンド|キーボード ショートカット|
|--------------|------------------------|
|Window.ActivateDocumentWindow|Esc|
|Window.AddTabtoSelection|Ctrl + Shift + Alt + Space|
|Window.CloseDocumentWindow|Ctrl + F4|
|Window.CloseToolWindow|Shift + Esc|
|Window.KeepTabOpen|Ctrl + Alt + Home|
|Window.MovetoNavigationBar|Ctrl + F2|
|Window.NextDocumentWindow|Ctrl + F6|
|Window.NextDocumentWindowNav|Ctrl + Tab|
|Window.NextPane|Alt + F6|
|Window.NextSplitPane|F6|
|Window.NextTab|Ctrl + Alt + PgDn<br /><br /> or<br /><br /> Ctrl + PgDn|
|Window.NextTabandAddtoSelection|Ctrl + Shift + Alt + PgDn|
|Window.NextToolWindowNav|Alt + F7|
|Window.PreviousDocumentWindow|Ctrl + Shift + F6|
|Window.PreviousDocumentWindowNav|Ctrl + Shift + Tab|
|Window.PreviousPane|Shift + Alt + F6|
|Window.PreviousSplitPane|Shift + F6|
|Window.PreviousTab|Ctrl + Alt + PgUp<br /><br /> or<br /><br /> Ctrl + PgUp|
|Window.PreviousTabandAddtoSelection|Ctrl + Shift + Alt + PgUp|
|Window.PreviousToolWindowNav|Shift + Alt + F7|
|Window.QuickLaunch|Ctrl + Q|
|Window.QuickLaunchPreviousCategory|Ctrl + Shift + Q|
|Window.ShowDockMenu|Alt + -|
|Window.ShowEzMDIFileList|Ctrl + Alt + ↓|
|Window.SolutionExplorerSearch|Ctrl + ;|
|Window.WindowSearch|Alt + `|

### <a name="azure"></a><a name="bkmk_windowsazure"></a> Azure

|コマンド|キーボード ショートカット|
|--------------|------------------------|
|WindowsAzure.RetryMobileServiceScriptOperation|Ctrl + Num *、Ctrl + R|
|WindowsAzure.ShowMobileServiceScriptErrorDetails|Ctrl + Num *、Ctrl + D|

## <a name="adonet-entity-data-model-designer"></a><a name="bkmk_ADONET"></a> ADO.NET Entity Data Model デザイナー

|コマンド|キーボード ショートカット|
|--------------|------------------------|
|OtherContextMenus.MicrosoftDataEntityDesignContext.MoveProperties.Down|Alt + ↓|
|OtherContextMenus.MicrosoftDataEntityDesignContext.MoveProperties.Down5|Alt + PgDn|
|OtherContextMenus.MicrosoftDataEntityDesignContext.MoveProperties.ToBottom|Alt + End|
|OtherContextMenus.MicrosoftDataEntityDesignContext.MoveProperties.ToTop|Alt + Home|
|OtherContextMenus.MicrosoftDataEntityDesignContext.MoveProperties.Up|Alt + ↑|
|OtherContextMenus.MicrosoftDataEntityDesignContext.MoveProperties.Up5|Alt + PgUp|
|OtherContextMenus.MicrosoftDataEntityDesignContext.Refactor.Rename|Ctrl + R、R|
|OtherContextMenus.MicrosoftDataEntityDesignContext.RemovefromDiagram|Shift + Del|
|View.EntityDataModelBrowser|Ctrl + 数字 1|
|View.EntityDataModelMappingDetails|Ctrl + 数字 2|

## <a name="class-diagram"></a><a name="bkmk_classDiagram"></a> クラスダイアグラム

|コマンド|キーボード ショートカット|
|--------------|------------------------|
|ClassDiagram.Collapse|Num -|
|ClassDiagram.Expand|Num +|
|Edit.Delete|Ctrl + Del|
|Edit.ExpandCollapseBaseTypeList|Shift + Alt + B|
|Edit.NavigateToLollipop|Shift + Alt + L|
|Edit.RemovefromDiagram|削除|
|View.ViewCode|次に、|

## <a name="coded-ui-test-editor"></a><a name="bkmk_codedUItest"></a> コード化された UI テストエディター

|コマンド|キーボード ショートカット|
|--------------|------------------------|
|OtherContextMenus.UITestEditorContextMenu.CopyReferencetoClipboard|Ctrl+C|
|OtherContextMenus.UITestEditorContextMenu.InsertDelayBefore|Ctrl + Alt + D|
|OtherContextMenus.UITestEditorContextMenu.LocateAll|Shift + Alt + L|
|OtherContextMenus.UITestEditorContextMenu.LocatetheUIControl|Ctrl + Shift + L|
|OtherContextMenus.UITestEditorContextMenu.Movecode|Ctrl + Alt + C|
|OtherContextMenus.UITestEditorContextMenu.Splitintoanewmethod|Ctrl + Shift + T|

## <a name="dataset-editor"></a><a name="bkmk_dataset"></a> データセットエディター

|コマンド|キーボード ショートカット|
|--------------|------------------------|
|OtherContextMenus.ColumnContext.InsertColumn|挿入|
|OtherContextMenus.DbTableContext.Add.Column|Ctrl+L|

## <a name="difference-viewer"></a><a name="bkmk_diff"></a> 相違ビューアー

|コマンド|キーボード ショートカット|
|-|-|
|Diff.IgnoreTrimWhitespace|Ctrl + \\、Ctrl + Spacebar|
|Diff.InlineView|Ctrl + \\、Ctrl + 1|
|Diff.LeftOnlyView|Ctrl + \\、Ctrl + 3|
|Diff.NextDifference|F8|
|Diff.PreviousDifference|Shift + F8|
|Diff.RightOnlyView|Ctrl + \\、Ctrl + 4|
|Diff.SideBySideView|Ctrl + \\、Ctrl + 2|
|Diff.SwitchBetweenLeftAndRight|Ctrl + \\、Ctrl + Tab|
|Diff.SynchronizeViewToggle|Ctrl + \\、Ctrl + ↓|
|EditorContextMenus.CodeWindow.AddComment|Ctrl + Shift + K|
|EditorContextMenus.CodeWindow.EditLocalFile|Ctrl+Shift+P|

## <a name="dom-explorer"></a><a name="bkmk_DOM"></a> DOM Explorer

|コマンド|キーボード ショートカット|
|--------------|------------------------|
|DOMExplorer.Refresh|F5|
|DOMExplorer.SelectElement|Ctrl + B|
|DOMExplorer.ShowLayout|Ctrl + Shift + I|

## <a name="f-interactive"></a><a name="bkmk_FSharp"></a> F# インタラクティブ

|コマンド|ショートカット キー|
|-------------|-----------------------|
|OtherContextMenus.FSIConsoleContext.CancelInteractiveEvaluation|Ctrl + Break|

## <a name="graph-document-editor"></a><a name="bkmk_graphDoc"></a> グラフドキュメントエディター

|コマンド|キーボード ショートカット|
|--------------|------------------------|
|ArchitectureContextMenus.DirectedGraphContextMenu.Advanced.Add.AddNode|挿入|
|ArchitectureContextMenus.DirectedGraphContextMenu.Advanced.Select.BothDependencies|B|
|ArchitectureContextMenus.DirectedGraphContextMenu.Advanced.Select.IncomingDependencies|I|
|ArchitectureContextMenus.DirectedGraphContextMenu.Advanced.Select.OutgoingDependencies|O|
|ArchitectureContextMenus.DirectedGraphContextMenu.NewComment|Ctrl + Shift + K<br /><br /> or<br /><br /> Ctrl + E、C|
|ArchitectureContextMenus.DirectedGraphContextMenu.Remove|削除|
|ArchitectureContextMenus.DirectedGraphContextMenu.Rename|F2|

## <a name="graphics-diagnostics"></a><a name="bkmk_graphicsDebugger"></a> グラフィックス診断

|コマンド|キーボード ショートカット|
|--------------|------------------------|
|Debug.Graphics.CaptureFrame|None|
|Graphics.MovePixelSelectionDown|Shift + Alt + ↓|
|Graphics.MovePixelSelectionLeft|Shift + Alt + ←|
|Graphics.MovePixelSelectionRight|Shift + Alt + →|
|Graphics.MovePixelSelectionUp|Shift + Alt + ↑|
|Graphics.ZoomToActualSize|Shift + Alt + 0|
|Graphics.ZoomToFitInWindow|Shift+Alt+9|
|Graphics.ZoomIn|Shift + Alt + =|
|Graphics.ZoomOut|Shift + Alt + -|

## <a name="html-editor"></a><a name="bkmk_HTMLeditor"></a> HTML エディター

|コマンド|ショートカット キー|
|-------------|-----------------------|
|OtherContextMenus.HTMLContext.GoToController|Ctrl + M、Ctrl + G|

## <a name="html-editor-design-view"></a><a name="bkmk_HTMLeditorDesign"></a> HTML エディターデザインビュー

|コマンド|キーボード ショートカット|
|--------------|------------------------|
|Edit.MoveControlDown|Ctrl + ↓|
|Edit.MoveControlUp|Ctrl + ↑|
|Format.Bold|Ctrl + B|
|Format.ConverttoHyperlink|Ctrl+L|
|Format.InsertBookmark|Ctrl + Shift + L|
|Format.Italic|Ctrl + I|
|Format.Underline|Ctrl + U|
|Project.AddContentPage|Ctrl + M、Ctrl + C|
|Table.ColumntotheLeft|Ctrl + Alt + ←|
|Table.ColumntotheRight|Ctrl + Alt + →|
|Table.RowAbove|Ctrl + Alt + ↑|
|Table.RowBelow|Ctrl + Alt + ↓|
|View.ASP.NETNonvisualControls|Ctrl + Shift + N|
|View.EditMaster|Ctrl + M、Ctrl + M|
|View.NextView|Ctrl + PgDn|
|View.ShowSmartTag|Shift + Alt + F10|
|View.ViewMarkup|Shift + F7|
|Window.PreviousTab|Ctrl + PgUp|

## <a name="html-editor-source-view"></a><a name="bkmk_HTMLeditorSource"></a> HTML エディターソースビュー

|コマンド|キーボード ショートカット|
|--------------|------------------------|
|OtherContextMenus.HTMLContext.GoToController|Ctrl + M、Ctrl + G|
|View.NextView|Ctrl + PgDn|
|View.SynchronizeViews|Ctrl + Shift + Y|
|View.ViewDesigner|Shift + F7|
|Window.PreviousTab|Ctrl + PgUp|

## <a name="layer-diagram"></a><a name="bkmk_layerDiagram"></a> レイヤー図

|コマンド|ショートカット キー|
|-------------|-----------------------|
|Edit.Delete|Shift + Delete|

## <a name="managed-resources-editor"></a><a name="bkmk_managedResources"></a> マネージリソースエディター

|コマンド|キーボード ショートカット|
|--------------|------------------------|
|Edit.EditCell|F2|
|Edit.Remove|削除|
|Edit.RemoveRow|Ctrl + Delete|
|Edit.SelectionCancel|エスケープ|
|Resources.Audio|Ctrl + 数字 4|
|Resources.Files|Ctrl + 数字 5|
|Resources.Icons|Ctrl + 数字 3|
|Resources.Images|Ctrl + 数字 2|
|Resources.Other|Ctrl + 数字 6|
|Resources.Strings|Ctrl + 数字 1|

## <a name="merge-editor-window"></a><a name="bkmk_MergeEditor"></a> マージエディターウィンドウ

|コマンド|キーボード ショートカット|
|--------------|------------------------|
|TeamFoundationContextMenus.MergeContextMenu.SetFocusonLeftWindow|Alt + 1|
|TeamFoundationContextMenus.MergeContextMenu.SetFocusonResultWindow|Alt + 2|
|TeamFoundationContextMenus.MergeContextMenu.SetFocusonRightWindow|Alt + 3|

## <a name="microsoft-sql-server-data-tools-schema-compare"></a><a name="bkmk_SchemaCompare"></a> Microsoft SQL Server Data Tools、スキーマ比較

|コマンド|キーボード ショートカット|
|--------------|------------------------|
|SQL.SSDTSchemaCompareCompare|Shift + Alt + C|
|SQL.SSDTSchemaCompareGenerateScript|Shift + Alt + G|
|SQL.SSDTSchemaCompareNextChange|Shift + Alt + .|
|SQL.SSDTSchemaComparePreviousChange|Shift + Alt + ,|
|SQL.SSDTSchemaCompareStop|Alt + Break|
|SQL.SSDTSchemaCompareWriteUpdates|Shift + Alt + U|

## <a name="microsoft-sql-server-data-tools-table-designer"></a><a name="bkmk_TableDesigner"></a> Microsoft SQL Server Data Tools、テーブルデザイナー

|コマンド|キーボード ショートカット|
|--------------|------------------------|
|CommitAllEdits|Shift + Alt + U|
|SQL.ExpandWildcards|Ctrl + R、E<br /><br /> or<br /><br /> Ctrl + R、Ctrl + E|
|SQL.FullyqualifyNames|Ctrl + R、Q<br /><br /> or<br /><br /> Ctrl + R、Ctrl + Q|
|SQL.MovetoSchema|Ctrl + R、M<br /><br /> or<br /><br /> Ctrl + R、Ctrl + M|
|SQL 名前の変更|F2<br /><br /> or<br /><br /> Ctrl + R、R<br /><br /> or<br /><br /> Ctrl + R、Ctrl + R|
|ViewFileInScriptPanel|Shift + Alt + PgDn|

## <a name="microsoft-sql-server-data-tools-t-sql-editor"></a><a name="bkmk_TSQLeditor"></a> Microsoft SQL Server Data Tools、T-sql エディター

|コマンド|キーボード ショートカット|
|--------------|------------------------|
|CommitAllEdits|Shift + Alt + U|
|SQL.ExecuteWithDebugger|Alt + F5|
|SQL.ExpandWildcards|Ctrl + R、E<br /><br /> or<br /><br /> Ctrl + R、Ctrl + E|
|SQL.FullyqualifyNames|Ctrl + R、Q<br /><br /> or<br /><br /> Ctrl + R、Ctrl + Q|
|SQL.MovetoSchema|Ctrl + R、M<br /><br /> or<br /><br /> Ctrl + R、Ctrl + M|
|SQL 名前の変更|F2<br /><br /> or<br /><br /> Ctrl + R、R<br /><br /> or<br /><br /> Ctrl + R、Ctrl + R|
|SQL.TSqlEditorCancelQuery|Alt + Break|
|SQL.TSqlEditorExecuteQuery|Ctrl + Shift + E|
|SQL.TSqlEditorResultsAsFile|Ctrl + D、F|
|SQL.TSqlEditorResultsAsGrid|Ctrl + D、G|
|SQL.TSqlEditorResultsAsText|Ctrl + D、T|
|SQL.TSqlEditorShowEstimatedPlan|Ctrl + D、E|
|SQL.TSqlEditorToggleExecutionPlan|Ctrl + D、A|
|SQL.TSqlEditorToggleResultsPane|Ctrl + D、R|
|TSqlEditorCloneQuery|Ctrl + Alt + N|
|TSqlEditorDatabaseCombo|Shift + Alt + PgDn|

## <a name="microsoft-sql-server-data-tools-t-sql-pdw-editor"></a><a name="bkmk_linkfix"></a> Microsoft SQL Server Data Tools、T-sql PDW エディター

|コマンド|キーボード ショートカット|
|--------------|------------------------|
|SQL.TSqlEditorCancelQuery|Alt + Break|
|SQL.TSqlEditorExecuteQuery|Ctrl + Shift + E|
|SQL.TSqlEditorResultsAsFile|Ctrl + D、F|
|SQL.TSqlEditorResultsAsGrid|Ctrl + D、G|
|SQL.TSqlEditorResultsAsText|Ctrl + D、T|
|SQL.TSqlEditorShowEstimatedPlan|Ctrl + D、E|
|SQL.TSqlEditorToggleExecutionPlan|Ctrl + D、A|
|SQL.TSqlEditorToggleResultsPane|Ctrl + D、R|
|TSqlEditorCloneQuery|Ctrl + Alt + N|
|TSqlEditorDatabaseCombo|Shift + Alt + PgDn|

## <a name="page-inspector"></a><a name="bkmk_PageInspector"></a> Page Inspector

|コマンド|ショートカット キー|
|-------------|-----------------------|
|PageInspector.Minimize|F12|

## <a name="query-designer"></a><a name="bkmk_QueryDesigner"></a> クエリデザイナー

|コマンド|キーボード ショートカット|
|--------------|------------------------|
|QueryDesigner.CancelRetrievingData|Ctrl + T|
|QueryDesigner.Criteria|Ctrl + 数字 2|
|QueryDesigner.Diagram|Ctrl + 数字 1|
|QueryDesigner.ExecuteSQL|Ctrl + R|
|QueryDesigner.GoToRow|Ctrl + G|
|QueryDesigner.JoinMode|Ctrl + Shift + J|
|QueryDesigner.Results|Ctrl + 数字 4|
|QueryDesigner.SQL|Ctrl + 数字 3|

## <a name="query-results"></a><a name="bkmk_QueryResults"></a> クエリ結果

|コマンド|キーボード ショートカット|
|--------------|------------------------|
|SQL.QueryResultsNewRow|Alt + End|
|SQL.QueryResultsRefresh|Shift + Alt + R|
|SQL.QueryResultsStop|Alt + Break|

## <a name="report-designer"></a><a name="bkmk_ReportDesigner"></a> レポート デザイナー

|コマンド|キーボード ショートカット|
|--------------|------------------------|
|Edit.BreakLine|次に、|
|Edit.CharLeft|←|
|Edit.CharLeftExtend|Shift + ←|
|Edit.CharRight|→ キー|
|Edit.CharRightExtend|Shift + →|
|Edit.InsertTab|タブ|
|Edit.LineDown|↓ キー|
|Edit.LineDownExtend|Shift + ↓|
|Edit.LineUp|↑ キー|
|Edit.LineUpExtend|Shift + ↑|
|Edit.MoveControlDown|Ctrl + ↓|
|Edit.MoveControlLeft|Ctrl + ←|
|Edit.MoveControlRight|Ctrl + →|
|Edit.MoveControlUp|Ctrl + ↑|
|Edit.SelectionCancel|Esc|
|Edit.SizeControlDown|Ctrl + Shift + ↓|
|Edit.SizeControlLeft|Ctrl + Shift + ←|
|Edit.SizeControlRight|Ctrl + Shift + →|
|Edit.SizeControlUp|Ctrl + Shift + ↑|
|Edit.TabLeft|Shift + Tab|
|View.ReportData|Ctrl + Alt + D|

## <a name="sequence-diagram"></a><a name="bkmk_SequenceDiagram"></a> シーケンス図

|コマンド|キーボード ショートカット|
|--------------|------------------------|
|ArchitectureDesigner.Sequence.NavigateToCode|F12|
|Edit.Delete|Shift + Del|

## <a name="settings-designer"></a><a name="bkmk_SettingsDesigner"></a> 設定デザイナー

|コマンド|キーボード ショートカット|
|--------------|------------------------|
|Edit.EditCell|F2|
|Edit.RemoveRow|Ctrl + Delete|
|Edit.SelectionCancel|Esc|
|View.ViewCode|F7|

## <a name="solution-explorer"></a><a name="bkmk_SolutionExplorer"></a> ソリューション エクスプローラー

|コマンド|ショートカット キー|
|-------------|-----------------------|
|ClassViewContextMenus.ClassViewProject.View.ViewinPageInspector|Ctrl + K、Ctrl + G|

## <a name="team-explorer"></a><a name="bkmk_TeamExplorer"></a> チーム エクスプローラー

|コマンド|ショートカット キー|
|-------------|-----------------------|
|Edit.Delete|削除|
|File.Rename|F2|
|TeamFoundationContextMenus.Commands.GoToTeamExplorerNavigation|Alt + Home|
|TeamFoundationContextMenus.Commands.GoToTeamExplorerNextSectionContent|Alt + ↓|
|TeamFoundationContextMenus.Commands.GoToTeamExplorerPageContent|Alt + 0|
|TeamFoundationContextMenus.Commands.GoToTeamExplorerPreviousSectionContent|Alt + ↑|
|TeamFoundationContextMenus.Commands.GoToTeamExplorerSection1Content|Alt + 1|
|TeamFoundationContextMenus.Commands.GoToTeamExplorerSection2Content|Alt + 2|
|TeamFoundationContextMenus.Commands.GoToTeamExplorerSection3Content|Alt + 3|
|TeamFoundationContextMenus.Commands.GoToTeamExplorerSection4Content|Alt + 4|
|TeamFoundationContextMenus.Commands.GoToTeamExplorerSection5Content|Alt + 5|
|TeamFoundationContextMenus.Commands.GoToTeamExplorerSection6Content|Alt + 6|
|TeamFoundationContextMenus.Commands.GoToTeamExplorerSection7Content|Alt + 7|
|TeamFoundationContextMenus.Commands.GoToTeamExplorerSection8Content|Alt + 8|
|TeamFoundationContextMenus.Commands.GoToTeamExplorerSection9Content|Alt + 9|
|TeamFoundationContextMenus.Commands.TeamExplorerNavigateBackward|Alt + ← キー|
|TeamFoundationContextMenus.Commands.TeamExplorerNavigateForward|Alt + → キー|
|TeamFoundationContextMenus.MyWorkPageInProgress.TfsContextMyWorkPageCreateCopyWI|Shift + Alt + C|
|TeamFoundationContextMenus.MyWorkPageInProgress.TfsContextMyWorkPageNewLinkedWI|Shift + Alt + L|
|View.Refresh|F5|

## <a name="team-foundation-build-detail-editor"></a><a name="bkmk_TFBuild"></a> Team Foundation ビルド詳細エディター

|コマンド|ショートカット キー|
|-------------|-----------------------|
|View.Refresh|F5|

## <a name="test-explorer"></a><a name="bkmk_TestExplorer"></a> テスト エクスプローラー

|コマンド|ショートカット キー|
|-------------|-----------------------|
|TestExplorer.OpenTest|F12|

## <a name="text-editor"></a><a name="bkmk_TextEditor"></a> テキストエディター

|                             コマンド                              |                  キーボード ショートカット                   |
|-------------------------------------------------------------------|-------------------------------------------------------|
|                          Edit.BreakLine                           |     次に、<br /><br /> or<br /><br /> Shift + Enter      |
|                           Edit.CharLeft                           |                      ←                       |
|                        Edit.CharLeftExtend                        |                   Shift + ←                    |
|                     Edit.CharLeftExtendColumn                     |                 Shift + Alt + ←                  |
|                          Edit.CharRight                           |                      → キー                      |
|                       Edit.CharRightExtend                        |                   Shift + →                   |
|                    Edit.CharRightExtendColumn                     |                 Shift + Alt + →                 |
|                        Edit.CharTranspose                         |                        Ctrl + T                         |
|                        Edit.ClearBookmarks                        |                    Ctrl + K、Ctrl + L                     |
|                     Edit.CollapseAllOutlining                     |                    Ctrl + M、Ctrl + A                     |
|                    Edit.CollapseCurrentRegion                     |                    Ctrl + M、Ctrl + S                     |
|                         Edit.CollapseTag                          |                    Ctrl + M、Ctrl + T                     |
|                    Edit.CollapsetoDefinitions                     |                    Ctrl + M、Ctrl + O                     |
|                       Edit.CommentSelection                       |                    Ctrl + K、Ctrl + C                     |
|                         Edit.CompleteWord                         | Ctrl + Space<br /><br /> or<br /><br /> Alt + → キー |
|                       Edit.CopyParameterTip                       |                   Ctrl + Shift + Alt + C                    |
|                     Edit.DecreaseFilterLevel                      |                         Alt + ,                         |
|                       Edit.DeleteBackwards                        |   バックスペース<br /><br /> or<br /><br /> Shift + Bkspce   |
|                  Edit.DeleteHorizontalWhiteSpace                  |                    Ctrl + K、Ctrl + \                     |
|                         Edit.DocumentEnd                          |                       Ctrl + End                        |
|                      Edit.DocumentEndExtend                       |                    Ctrl + Shift + End                     |
|                        Edit.DocumentStart                         |                       Ctrl + Home                       |
|                     Edit.DocumentStartExtend                      |                    Ctrl + Shift + Home                    |
|                      Edit.ExpandAllOutlining                      |                    Ctrl + M、Ctrl + X                     |
|                     Edit.ExpandCurrentRegion                      |                    Ctrl + M、Ctrl + E                     |
|                        Edit.FormatDocument                        |                    Ctrl + K、Ctrl + D                     |
|                       Edit.FormatSelection                        |                    Ctrl + K、Ctrl + F                     |
|                          Edit.GotoBrace                           |                        Ctrl + ]                         |
|                       Edit.GotoBraceExtend                        |                     Ctrl + Shift + ]                      |
|                        Edit.HideSelection                         |                    Ctrl + M、Ctrl + H                     |
|                     Edit.IncreaseFilterLevel                      |                         Alt + .                         |
|                      Edit.IncrementalSearch                       |                        Ctrl + I                         |
|                          Edit.InsertTab                           |                          タブ                          |
|                           Edit.LineCut                            |                        Ctrl+L                         |
|                          Edit.LineDelete                          |                     Ctrl + Shift + L                      |
|                           Edit.LineDown                           |                      ↓ キー                       |
|                        Edit.LineDownExtend                        |                   Shift + ↓                    |
|                     Edit.LineDownExtendColumn                     |                 Shift + Alt + ↓                  |
|                           Edit.LineEnd                            |                          End                          |
|                        Edit.LineEndExtend                         |                       Shift + End                       |
|                     Edit.LineEndExtendColumn                      |                     Shift + Alt + End                     |
|                        Edit.LineOpenAbove                         |                      Ctrl + Enter                       |
|                        Edit.LineOpenBelow                         |                   Ctrl + Shift + Enter                    |
|                          Edit.LineStart                           |                         ホーム                          |
|                       Edit.LineStartExtend                        |                      Shift + Home                       |
|                    Edit.LineStartExtendColumn                     |                    Shift + Alt + Home                     |
|                        Edit.LineTranspose                         |                      Shift + Alt + T                      |
|                            Edit.LineUp                            |                       ↑ キー                        |
|                         Edit.LineUpExtend                         |                    Shift + ↑                     |
|                      Edit.LineUpExtendColumn                      |                  Shift + Alt + ↑                   |
|                         Edit.ListMembers                          |                        Ctrl + J                         |
|                        Edit.MakeLowercase                         |                        Ctrl + U                         |
|                        Edit.MakeUppercase                         |                     Ctrl + Shift + U                      |
|                    Edit.MoveSelectedLinesDown                     |                    Alt + ↓                     |
|                     Edit.MoveSelectedLinesUp                      |                     Alt + ↑                      |
|                   Edit.NextHighlightedReference                   |                 Ctrl + Shift + ↓                 |
|                         Edit.OvertypeMode                         |                        挿入                         |
|                           Edit.PageDown                           |                         PgDn                          |
|                        Edit.PageDownExtend                        |                      Shift + PgDn                       |
|                            Edit.PageUp                            |                         PgUp                          |
|                         Edit.PageUpExtend                         |                      Shift + PgUp                       |
|                        Edit.ParameterInfo                         |                  Ctrl + Shift + Spacebar                  |
|                      Edit.PasteParameterTip                       |                   Ctrl + Shift + Alt + P                    |
|                         Edit.PeekBackward                         |                      Ctrl + Alt + -                       |
|                        Edit.PeekDefinition                        |                        Alt + F12                        |
|                         Edit.PeekForward                          |                      Ctrl + Alt + =                       |
|                 Edit.PreviousHighlightedReference                 |                  Ctrl + Shift + ↑                  |
|                          Edit.QuickInfo                           |                    Ctrl + K、Ctrl + I                     |
|                   Edit.ReverseIncrementalSearch                   |                     Ctrl + Shift + I                      |
|                        Edit.ScrollLineDown                        |                    Ctrl + ↓                    |
|                         Edit.ScrollLineUp                         |                     Ctrl + ↑                     |
|                      Edit.SelectCurrentWord                       |                        Ctrl+W                         |
|                       Edit.SelectionCancel                        |                        エスケープ                         |
|                      Edit.SelectToLastGoBack                      |                        Ctrl + =                         |
|                       Edit.ShowCodeLensMenu                       |                        Alt + \`                         |
|                      Edit.StopHidingCurrent                       |                    Ctrl + M、Ctrl + U                     |
|                        Edit.StopOutlining                         |                    Ctrl + M、Ctrl + P                     |
|                          Edit.SwapAnchor                          |                    Ctrl + K、Ctrl + A                     |
|                           Edit.TabLeft                            |                       Shift + Tab                       |
|                      Edit.ToggleAllOutlining                      |                    Ctrl + M、Ctrl + L                     |
|                        Edit.ToggleBookmark                        |                    Ctrl + K、Ctrl + K                     |
|                     Edit.ToggleCompletionMode                     |                    Ctrl + Alt + Space                     |
|                   Edit.ToggleOutliningExpansion                   |                    Ctrl + M、Ctrl + M                     |
|                    Edit.ToggleTaskListShortcut                    |                    Ctrl + K、Ctrl + H                     |
|                        Edit.ToggleWordWrap                        |                    Ctrl + E、Ctrl + W                     |
|                      Edit.UncommentSelection                      |                    Ctrl + K、Ctrl + U                     |
|                          Edit.ViewBottom                          |                       Ctrl + PgDn                       |
|                       Edit.ViewBottomExtend                       |                    Ctrl + Shift + PgDn                    |
|                           Edit.ViewTop                            |                       Ctrl + PgUp                       |
|                        Edit.ViewTopExtend                         |                    Ctrl + Shift + PgUp                    |
|                        Edit.ViewWhiteSpace                        |                    Ctrl + R、Ctrl + W                     |
|                       Edit.WordDeleteToEnd                        |                      Ctrl + Delete                      |
|                      Edit.WordDeleteToStart                       |                    Ctrl + Backspace                     |
|                           Edit.WordNext                           |                   Ctrl + →                    |
|                        Edit.WordNextExtend                        |                Ctrl + Shift + →                 |
|                     Edit.WordNextExtendColumn                     |              Ctrl + Shift + Alt + →               |
|                         Edit.WordPrevious                         |                    Ctrl + ←                    |
|                      Edit.WordPreviousExtend                      |                 Ctrl + Shift + ←                 |
|                   Edit.WordPreviousExtendColumn                   |               Ctrl + Shift + Alt + ←               |
|                        Edit.WordTranspose                         |                     Ctrl + Shift + T                      |
|        EditorContextMenus.CodeWindow.ExecuteInInteractive         |                       Alt + Enter                       |
|      EditorContextMenus.CodeWindow.ExecuteLineInInteractive       |                         Alt + '                         |
|         OtherContextMenus.HTMLContext.ViewinPageInspector         |                    Ctrl + K、Ctrl + G                     |
|   TeamFoundationContextMenus.Annotate.TfsAnnotateMoveNextRegion   |                       Alt + PgDn                        |
| TeamFoundationContextMenus.Annotate.TfsAnnotateMovePreviousRegion |                       Alt + PgUp                        |

## <a name="uml-activity-diagram"></a><a name="bkmk_UMLactivityDiagram"></a> UML アクティビティ図

|コマンド|ショートカット キー|
|-------------|-----------------------|
|Edit.Delete|Shift + Del|

## <a name="uml-class-diagram"></a><a name="bkmk_UMLclassDiagram"></a> UML クラス図

|コマンド|ショートカット キー|
|-------------|-----------------------|
|Edit.DeleteFromModel|Shift + Del|

## <a name="uml-component-diagram"></a><a name="bkmk_UMLcomponentDiagram"></a> UML コンポーネント図

|コマンド|ショートカット キー|
|-------------|-----------------------|
|Edit.DeleteFromModel|Shift + Del|

## <a name="uml-use-case-diagram"></a><a name="bkmk_UMLusecaseDiagram"></a> UML ユースケース図

|コマンド|ショートカット キー|
|-------------|-----------------------|
|Edit.DeleteFromModel|Shift + Del|

## <a name="vc-accelerator-editor"></a><a name="bkmk_vcaccelerator"></a> VC アクセラレータエディター

|コマンド|ショートカット キー|
|--------------|------------------------|
|Edit.NewAccelerator|挿入|
|Edit.NextKeyTyped|Ctrl+W|

## <a name="vc-dialog-editor"></a><a name="bkmk_vcdialogeditor"></a> VC ダイアログエディター

|コマンド|ショートカット キー|
|--------------|------------------------|
|Edit.MoveControlDown|↓ キー|
|Edit.MoveControlLeft|←|
|Edit.MoveControlRight|→ キー|
|Edit.MoveControlUp|↑ キー|
|Edit.ScrollColumnLeft|Ctrl + ←|
|Edit.ScrollColumnRight|Ctrl + →|
|Edit.ScrollLineDown|Ctrl + ↓|
|Edit.ScrollLineUp|Ctrl + ↑|
|Edit.SizeControlDown|Shift + ↓|
|Edit.SizeControlLeft|Shift + ←|
|Edit.SizeControlRight|Shift + →|
|Edit.SizeControlUp|Shift + ↑|
|Format.AlignBottoms|Ctrl + Shift + ↓|
|Format.AlignCenters|Shift + F9|
|Format.AlignLefts|Ctrl + Shift + ←|
|Format.AlignMiddles|F9|
|Format.AlignRights|Ctrl + Shift + →|
|Format.AlignTops|Ctrl + Shift + ↑|
|Format.ButtonBottom|Ctrl + B|
|Format.ButtonRight|Ctrl + R|
|Format.CenterHorizontal|Ctrl + Shift + F9|
|Format.CenterVertical|Ctrl + F9|
|Format.CheckMnemonics|Ctrl + M|
|Format.SizetoContent|Shift + F7|
|Format.SpaceAcross|Alt + → キー<br /><br /> or<br /><br /> Alt + ← キー|
|Format.SpaceDown|Alt + ↑<br /><br /> or<br /><br /> Alt + ↓|
|Format.TabOrder|Ctrl + D|
|Format.TestDialog|Ctrl + T|
|Format.ToggleGuides|Ctrl + G|

## <a name="vc-image-editor"></a><a name="bkmk_vcimageeditor"></a> VC イメージエディター

|コマンド|キーボード ショートカット|
|--------------|------------------------|
|Image.AirbrushTool|Ctrl + A|
|Image.BrushTool|Ctrl + B|
|Image.CopyandOutlineSelection|Ctrl + Shift + U|
|Image.DrawOpaque|Ctrl + J|
|Image.EllipseTool|Alt + P|
|Image.EraseTool|Ctrl + Shift + I|
|Image.FilledEllipseTool|Ctrl + Shift + Alt + P|
|Image.FilledRectangleTool|Ctrl + Shift + Alt + R|
|Image.FilledRoundedRectangleTool|Ctrl + Shift + Alt + W|
|Image.FillTool|Ctrl + F|
|Image.FlipHorizontal|Ctrl + H|
|Image.FlipVertical|Shift + Alt + H|
|Image.LargerBrush|Ctrl + =|
|Image.LineTool|Ctrl+L|
|Image.MagnificationTool|Ctrl + M|
|Image.Magnify|Ctrl + Shift + M|
|Image.NewImageType|挿入|
|Image.NextColor|Ctrl + ]<br /><br /> or<br /><br /> Ctrl + →|
|Image.NextRightColor|Ctrl + Shift + ]<br /><br /> or<br /><br /> Ctrl + Shift + →|
|Image.OutlinedEllipseTool|Shift + Alt + P|
|Image.OutlinedRectangleTool|Shift + Alt + R|
|Image.OutlinedRoundedRectangleTool|Shift + Alt + W|
|Image.PencilTool|Ctrl + I|
|Image.PreviousColor|Ctrl + [<br /><br /> or<br /><br /> Ctrl + ←|
|Image.PreviousRightColor|Ctrl + Shift + [<br /><br /> or<br /><br /> Ctrl + Shift + ←|
|Image.RectangleSelectionTool|Shift + Alt + S|
|Image.RectangleTool|Alt + R|
|Image.Rotate90Degrees|Ctrl + Shift + H|
|Image.RoundedRectangleTool|Alt + W|
|Image.ShowGrid|Ctrl+Alt+S|
|Image.ShowTileGrid|Ctrl + Shift + Alt + S|
|Image.SmallBrush|Ctrl + .|
|Image.SmallerBrush|Ctrl + -|
|Image.TextTool|Ctrl + T|
|Image.UseSelectionasBrush|Ctrl + U|
|Image.ZoomIn|Ctrl + Shift + .<br /><br /> or<br /><br /> Ctrl + ↑|
|Image.ZoomOut|Ctrl + Shift + ,<br /><br /> or<br /><br /> Ctrl + ↓|

## <a name="vc-string-editor"></a><a name="bkmk_vcstringeditor"></a> VC 文字列エディター

|コマンド|ショートカット キー|
|-------------|-----------------------|
|Edit.NewString|挿入|

## <a name="view-designer"></a><a name="bkmk_viewDesigner"></a> ビューデザイナー

|コマンド|キーボード ショートカット|
|--------------|------------------------|
|QueryDesigner.CancelRetrievingData|Ctrl + T|
|QueryDesigner.Criteria|Ctrl + 数字 2|
|QueryDesigner.Diagram|Ctrl + 数字 1|
|QueryDesigner.ExecuteSQL|Ctrl + R|
|QueryDesigner.GoToRow|Ctrl + G|
|QueryDesigner.JoinMode|Ctrl + Shift + J|
|QueryDesigner.Results|Ctrl + 数字 4|
|QueryDesigner.SQL|Ctrl + 数字 3|

## <a name="visual-studio"></a><a name="bkmk_visualstudio"></a> Visual Studio

|コマンド|ショートカット キー|
|-------------|-----------------------|
|OtherContextMenus.ORDesignerContext.HideMethodsPane|Ctrl + 数字 1|

## <a name="windows-forms-designer"></a><a name="bkmk_wfdesigner"></a> Windows フォーム デザイナー

|コマンド|キーボード ショートカット|
|--------------|------------------------|
|Edit.BreakLine|次に、|
|Edit.CharLeft|←|
|Edit.CharLeftExtend|Shift + ←|
|Edit.CharRight|→ キー|
|Edit.CharRightExtend|Shift + →|
|Edit.DocumentEnd|End|
|Edit.DocumentEndExtend|Shift + End|
|Edit.DocumentStart|ホーム|
|Edit.DocumentStartExtend|Shift + Home|
|Edit.InsertTab|タブ|
|Edit.LineDown|↓ キー|
|Edit.LineDownExtend|Shift + ↑|
|Edit.LineUp|↑ キー|
|Edit.LineUpExtend|Shift + ↓|
|Edit.MoveControlDown|Ctrl + ↓|
|Edit.MoveControlLeft|Ctrl + ←|
|Edit.MoveControlRight|Ctrl + →|
|Edit.MoveControlUp|Ctrl + ↑|
|Edit.SelectionCancel|エスケープ|
|Edit.SizeControlDown|Ctrl + Shift + ↓|
|Edit.SizeControlLeft|Ctrl + Shift + ←|
|Edit.SizeControlRight|Ctrl + Shift + →|
|Edit.SizeControlUp|Ctrl + Shift + ↑|
|Edit.TabLeft|Shift + Tab|

## <a name="work-item-editor"></a><a name="bkmk_workItemEditor"></a> 作業項目エディター

|コマンド|キーボード ショートカット|
|--------------|------------------------|
|Edit.CreateCopyofWorkItem|Shift + Alt + C|
|Edit.RefreshWorkItem|F5|
|Team.NewLinkedWorkItem|Shift + Alt + L|

## <a name="work-item-query-view"></a><a name="bkmk_WIqueryview"></a> 作業項目クエリビュー

|コマンド|キーボード ショートカット|
|--------------|------------------------|
|Edit.CreateCopyofWorkItem|Shift + Alt + C|
|Edit.Indent|Shift + Alt + →|
|Edit.Outdent|Shift + Alt + ←|
|Team.NewLinkedWorkItem|Shift + Alt + L|
|Team.Refresh|F5|
|Window.Toggle|Shift + Alt + V|

## <a name="work-item-results-view"></a><a name="bkmk_WIresultsview"></a> 作業項目の結果ビュー

|コマンド|キーボード ショートカット|
|--------------|------------------------|
|Edit.CreateCopyofWorkItem|Shift + Alt + C|
|Edit.Indent|Shift + Alt + →|
|Edit.Outdent|Shift + Alt + ←|
|Team.GotoNextWorkItem|Shift + Alt + N|
|Team.GotoPreviousWorkItem|Shift + Alt + P|
|Team.NewLinkedWorkItem|Shift + Alt + L|
|Team.Refresh|F5|
|Window.Toggle|Shift + Alt + V|

## <a name="workflow-designer"></a><a name="bkmk_workflowdesigner"></a> ワークフロー デザイナー

|コマンド|キーボード ショートカット|
|--------------|------------------------|
|Edit.CompleteWord|Ctrl + K、W<br /><br /> or<br /><br /> Ctrl + K、Ctrl + W<br /><br /> or<br /><br /> Ctrl + Space<br /><br /> or<br /><br /> Alt + → キー|
|Edit.DecreaseFilterLevel|Alt + ,|
|Edit.IncreaseFilterLevel|Alt + .|
|Edit.ListMembers|Ctrl + K、L<br /><br /> or<br /><br /> Ctrl + K、Ctrl + L<br /><br /> or<br /><br /> Ctrl + J|
|Edit.ParameterInfo|Ctrl + K、P<br /><br /> or<br /><br /> Ctrl + K、Ctrl + P<br /><br /> or<br /><br /> Ctrl + Shift + Spacebar|
|Edit.QuickInfo|Ctrl + K、I<br /><br /> or<br /><br /> Ctrl + K、Ctrl + I|
|WorkflowDesigner.Collapse|Ctrl + E、Ctrl + C<br /><br /> or<br /><br /> Ctrl + E、C|
|WorkflowDesigner.CollapseAll|or|
|WorkflowDesigner.ConnectNodes|Ctrl + E、Ctrl + F<br /><br /> or<br /><br /> Ctrl + E、F|
|WorkflowDesigner.CreateVariable|Ctrl + E、Ctrl + N<br /><br /> or<br /><br /> Ctrl + E、N|
|WorkflowDesigner.ExpandAll|Ctrl + E、Ctrl + X<br /><br /> or<br /><br /> Ctrl + E、X|
|WorkflowDesigner.ExpandInPlace|Ctrl + E、Ctrl + E<br /><br /> or<br /><br /> Ctrl + E、E|
|WorkflowDesigner.GoToParent|Ctrl + E、Ctrl + P<br /><br /> or<br /><br /> Ctrl + E、P|
|WorkflowDesigner.MoveFocus|Ctrl + E、Ctrl + M<br /><br /> or<br /><br /> Ctrl + E、M|
|WorkflowDesigner.NavigateThroughDesigner|Ctrl + Alt + F6|
|WorkflowDesigner.Restore|Ctrl + E、Ctrl + R<br /><br /> or<br /><br /> Ctrl + E、R|
|WorkflowDesigner.ShowHideArgumentDesigner|Ctrl + E、Ctrl + A<br /><br /> or<br /><br /> Ctrl + E、A|
|WorkflowDesigner.ShowHideImportsDesigner|Ctrl + E、Ctrl + I<br /><br /> or<br /><br /> Ctrl + E、I|
|WorkflowDesigner.ShowHideOverviewMap|Ctrl + E、Ctrl + O<br /><br /> or<br /><br /> Ctrl + E、O|
|WorkflowDesigner.ShowHideVariableDesigner|Ctrl + E、Ctrl + V<br /><br /> or<br /><br /> Ctrl + E、V|
|WorkflowDesigner.ToggleSelection|Ctrl + E、Ctrl + S<br /><br /> or<br /><br /> Ctrl + E、S|
|WorkflowDesigner.ZoomIn|Ctrl + Num  + |
|WorkflowDesigner.ZoomOut|Ctrl + Num -|

## <a name="xaml-ui-designer"></a><a name="bkmk_xamluidesigner"></a> XAML UI デザイナー

|コマンド|キーボード ショートカット|
|--------------|------------------------|
|Design.FitAll|Ctrl + 数字 0|
|Design.ShowHandles|F9|
|Design.ZoomIn|Ctrl + Alt + =|
|Design.ZoomOut|Ctrl + Alt + -|
|Format.EditText|F2|
|Format.ResetLayout.All|Ctrl + Shift + R|
|View.EdgeLeftMoveLeft|Ctrl + Shift + ,|
|View.EdgeLeftMoveRight|Ctrl + Shift + .|
|View.EdgeRightMoveLeft|Ctrl + Shift + Alt + ,|
|View.EdgeRightMoveRight|Ctrl + Shift + Alt + .|
|プロジェクト コードの実行|Ctrl + F9|

## <a name="xml-text-editor"></a><a name="bkmk_xmlTextEditor"></a> XML (テキスト) エディター

|コマンド|キーボード ショートカット|
|--------------|------------------------|
|XML.StartXSLTDebugging|Alt + F5|
|XML.StartXSLTWithoutDebugging|Ctrl + Alt + F5|

## <a name="xml-schema-designer"></a><a name="bkmk_xmlSchemaDesigner"></a> XML スキーマデザイナー

|コマンド|キーボード ショートカット|
|--------------|------------------------|
|GraphView.BottomtoTop|Alt + ↑|
|GraphView.LefttoRight|Alt + → キー|
|GraphView.RighttoLeft|Alt + ← キー|
|GraphView.ToptoBottom|Alt + ↓|
|OtherContextMenus.GraphView.RemovefromWorkspace|削除|
|XsdDesigner.ShowContentModelView|Ctrl + 数字 2|
|XsdDesigner.ShowGraphView|Ctrl + 数字 3|
|XsdDesigner.ShowStartView|Ctrl + 数字 1|

## <a name="see-also"></a>参照
 [アイコン用イメージ エディター](https://msdn.microsoft.com/library/586d2b8b-0348-4883-a85d-1ff0ddbf14dd) [IntelliSense の使用](../ide/using-intellisense.md)
