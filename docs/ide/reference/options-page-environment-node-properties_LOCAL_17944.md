---
title: '[環境] ノード プロパティ ([オプション] ページ)'
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- automation [Visual Studio], controlling Tools Options
- Tools Options settings, Environment node properties
ms.assetid: 26dca41f-91fc-4ca7-9103-3da402baa1d5
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ee14cddc6a3eb4b0348b88be1d7c2b0a48b44c01
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62945621"
---
# <a name="options-page-environment-node-properties"></a>[環境] ノード プロパティ ([オプション] ページ)

この記事では、**[オプション]** ダイアログ ボックスの **[環境]** カテゴリ `DTE.Properties("Environment", <Property Page>)` に関連付けられているページ (またはプロパティ コレクション) について説明します。 各サブセクションの見出しは、Properties コレクションにアクセスするための呼び出しです。その下の表では、コレクションのプロパティを示します。

## <a name="general"></a>全般

`DTE.Properties("Environment", "General")`

|プロパティ項目名|[値]|説明|
| - |-----------|-----------------|
|ShowStatusBar|Get/Set (Boolean)|ステータス バーを表示するかどうかを指定します。|
|WindowMenuContainsNItems|Get/Set (Short)|Windows メニューの 1 番下にドキュメント ウィンドウを含める方法を指定します。|
|MRUListContainsNItems|Get/Set (Short)|"最近使用した" サブメニューに表示するファイルの数を指定します。|
|Animations|Get/Set (Boolean)|統合開発環境 (IDE: Integrated Development Environment) のステータス バーでアニメーションを使用するかどうかを指定します。|
|AnimationSpeed|Get/Set (Short)||
|AutoAdjustExperience|Get/Set (Boolean)|クライアントのパフォーマンスに基づいて視覚的効果を自動的に調整します。|
|RichClientExperienceOptions|Get/Set (Enum)|<xref:EnvDTE100.vsRichClientExperienceOptions> の値を使用して、リッチ クライアントの視覚的効果を有効にします。|
|CloseButtonActiveTabOnly|Get/Set (Boolean)|**[閉じる]** ボタンをアクティブなタブにのみ表示するかどうかを指定します。|
|AutohidePinActiveTabOnly|Get/Set (Boolean)|**[自動的に隠す]** ボタンをアクティブなタブに対してのみ実行するかどうかを指定します。|

## <a name="add-inmacros-security"></a>アドイン/マクロ セキュリティ

`DTE.Properties("Environment", "AddinMacrosSecurity")`

|プロパティ項目名|[値]|説明|
| - |-----------|-----------------|
|MacrosEnabled|Get/Set (Boolean)|マクロの実行を許可します。|
|AddinsEnabled|Get/Set (Boolean)|アドインの読み込みを許可します。|
|LoadAddinsFromTheWeb|Get/Set (Boolean)|Web 上の URL からのアドインの読み込みを許可します。|

## <a name="documents"></a>ドキュメント

`DTE.Properties("Environment", "Documents")`

|プロパティ項目名|[値]|説明|
| - |-----------|-----------------|
|ReuseSavedActiveDocWindow|Get/Set (Boolean)|現在のドキュメントが保存されている場合、新しいファイルを開くときに現在のドキュメント ウィンドウを再利用するかどうかを指定します。 `false` の場合は、ドキュメントを開くたびに、新しいドキュメント ウィンドウが開きます。|
|DetectFileChangesOutsideIDE|Get/Set (Boolean)|ファイルがディスク上で変更されていることをオペレーティング システムから通知された場合に、IDE で開かれているファイルを自動的に再読み込みするかどうかを指定します。|
|AutoloadExternalChanges|Get/Set (Boolean)|開いているドキュメントが外部で変更されていることが検出されたとき、そのドキュメントが変更されていない場合は自動的に再読み込みするかどうかを指定します。 開いているドキュメントが変更され、このプロパティが `true` の場合は、`false` に設定されている場合と同様にメッセージが表示されます。|
|InitializeOpenFileFromCurrentDocument|Get/Set (Boolean)|<xref:EnvDTE.DTEClass.OpenFile%2A> コマンドがディレクトリとファイル名を直前にアクティブだったドキュメントから取得するか、最後にファイルを開いた場所から取得するかを指定します。|
|MiscFilesProjectSavesLastNItems|Get/Set (Short)|その他のファイル プロジェクトで記録するファイル数を指定します。 結果として、次回 IDE を使用するときに、最近使用したファイルがディスク上でその他のファイルとして表示されます。|
|ShowMiscFilesProject|Get/Set (Boolean)|その他のファイル プロジェクトを表示するかどうかを指定します。|
|CheckForConsisentLineEndings|Get/Set (Boolean)|ファイルの読み込み時に行の終わりの整合性を確認します。|
|SaveDocsAsUnicodeWhenDataLoss|Get/Set (Boolean)|コードページでデータが保存できない場合、Unicode でドキュメントを保存します。|
|DontShowGlobalUndoChangeLossDialog|Get/Set (Boolean)|全体的に元に戻す操作で他の編集したファイルが変更される場合、警告を表示します。|
|AllowEditingReadOnlyFiles|Get/Set (Boolean)|読み取り専用ファイルの編集を有効にしますが、その保存時に警告を表示します。|
|DocumentDockPreference|Get/Set (Enum)|<xref:EnvDTE100.vsDocumentDockPreferenceOptions>。 開かれたドキュメントを挿入するタブ内の位置です。|

## <a name="extension-manager"></a>拡張機能マネージャー

`DTE.Properties("Environment", "ExtensionManager")`

|プロパティ項目名|[値]|説明|
| - |-----------|-----------------|
|EnableAdminExtensions|Get/Set (Boolean)|Visual Studio が管理者の資格情報で実行されている場合、ユーザー単位の拡張機能を読み込みます。 この値を変更したら、Visual Studio を再起動する必要があります。|
|EnableOnline|Get/Set (Boolean)|Visual Studio Marketplace の拡張機能にアクセスできるようにします。|
|AutomaticallyCheckForUpdates|Get/Set (Boolean)|インストール済みの拡張機能に対する更新プログラムがあるかどうかを自動的に確認します。|

## <a name="find-and-replace"></a>検索と置換

`DTE.Properties("Environment", "FindAndReplace")`

|プロパティ項目名|[値]|説明|
| - |-----------|-----------------|
|ShowWarningMessages|Get/Set (Boolean)|警告メッセージを表示します。|
|InitializeFromEditor|Get/Set (Boolean)|**[検索する文字列]** ボックスのテキストをエディターから自動的に作成します。|
|ShowMessageBoxes|Get/Set (Boolean)|情報メッセージを表示します。|
|HideWindowsAfterMatchFromQuickFindReplace|Get/Set (Boolean)|**クイック検索**または**クイック置換**で一致が見つかった後、**[検索と置換]** ウィンドウを表示しません。|

## <a name="import-and-export-settings"></a>設定のインポートとエクスポート

`DTE.Properties("Environment", "Import and Export Settings")`

|プロパティ項目名|[値]|説明|
| - |-----------|-----------------|
|TrackTeamSettings|Get/Set (Boolean)|TeamSettingsFile で指定されたファイルの設定を使用します。|
|TeamSettingsFile|Get/Set (String)|チーム設定を含むファイルの名前です。|
|AutoSaveFile|Get/Set (String)|ユーザー設定が自動的に保存されるファイルの名前です。|

## <a name="international-settings"></a>国際対応の設定

`DTE.Properties("Environment", "International")`

|プロパティ項目名|[値]|説明|
| - |-----------|-----------------|
|言語|Get/Set (String)|Visual Studio の現在の言語の LCID 値です。|

## <a name="keyboard"></a>キーボード

`DTE.Properties("Environment", "Keyboard")`

|プロパティ項目名|[値]|説明|
| - |-----------|-----------------|
|Scheme|Get/Set (String)|組み込みスキームを含む文字列、または読み込まれた .vsk ファイルの完全パスを含む文字列を返します。 .vsk ファイルが読み込まれていない場合は "(既定)" を返します。|

## <a name="projects-and-solution"></a>プロジェクトおよびソリューション

`DTE.Properties("Environment", "ProjectsAndSolution")`

|プロパティ項目名|[値]|説明|
| - |-----------|-----------------|
|OnRunOrPreview|Get/Set (String)|ビルドしたプロジェクトをプレビューまたは実行する前に IDE ですべての内容を保存するかどうかを指定します。|
|ProjectsLocation|Get/Set (String)|新しいプロジェクトが保存される既定のディレクトリを決定します。|
|ShowOutputWindowBeforeBuild|Get/Set (Boolean)|ビルドの開始時に **[出力]** ウィンドウを表示するかどうかを指定します。|
|ShowTaskListAfterBuild|Get/Set (Boolean)|ビルド完了時に、失敗したビルド操作を **[タスク一覧]** に表示するかどうかを指定します。|
|TrackFileSelectionInExplorer|Get/Set (Boolean)|**ソリューション エクスプローラー**の現在の項目を追跡するかどうかを指定します。|
|AlwaysShowSolutionNode|Get/Set (Boolean)|ソリューション ノードを表示するかどうかを指定します。|
|OnlySaveStartupProjectsAndDependencies|Get/Set (Boolean)|保存操作をスタートアップ プロジェクトとその依存ファイルに制限するかどうかを指定します。|
|ShowAdvancedBuildConfigurations|Get/Set (Boolean)|ビルド構成の詳細を表示するかどうかを指定します。|
|ConcurrentBuilds|Get/Set (String)|並行して実行できるプロジェクト ビルドの最大数を指定します。|
|SaveNewProjects|Get/Set (Boolean)|新しいプロジェクトを作成時に自動的に保存するかどうかを指定します。|
|PromptForRenameSymbol|Get/Set (Boolean)|ファイル名の変更時にシンボルの名前変更を確認するかどうかを指定します。|
|OnRunWhenErrors|Get/Set (Enum)|実行時にビルドのエラーが発生したときの動作を指定します。|
|OnRunWhenOutOfDate|Get/Set (Enum)|実行時にプロジェクトが古い形式のときの動作を指定します。|
|ProjectTemplatesLocation|Get/Set (String)|ユーザー プロジェクト テンプレートが格納されているディレクトリです。|
|ProjectItemTemplatesLocation|Get/Set (String)|ユーザー項目テンプレートが格納されているディレクトリです。|
|DefaultBehaviorForStartupProjects|Get/Set (String)||
|MSBuildOutputVerbosity|Get/Set (String)|ビルド出力の詳細出力レベルを指定します。|

## <a name="startup"></a>スタートアップ

`DTE.Properties("Environment", "Startup")`

::: moniker range="vs-2017"

|プロパティ項目名|[値]|説明|
| - |-----------|-----------------|
|OnStartUp|Get/Set (Enum)|起動時に実行するアクションです。<xref:EnvDTE.vsStartUp> から取得され、0 ～ 5 の値で示されます。<br /><br /> -   0:ホーム ページを開く<br />-   1:最後に読み込んだソリューション<br />-   2:**[プロジェクトを開く]** ダイアログ ボックスの表示<br />-   3:**[新しいプロジェクト]** ダイアログ ボックスの表示<br />-   4:空の環境の表示<br />-   5:スタート ページの表示|
|StartPageRSSUrl|Get/Set (String)|起動時に使用する RSS フィードの URL です。|
|StartPageRefreshDownloadedContent|Get/Set (Boolean)|StartPageRefreshInterval で指定された間隔が経過するたびにスタート ページを更新します。|
|StartPageRefreshInterval|Get/Set (Short)|スタート ページを更新する間隔 (分単位) です。|

::: moniker-end

::: moniker range=">=vs-2019"

|プロパティ項目名|[値]|説明|
| - |-----------|-----------------|
|OnStartUp|Get/Set (Enum)|起動時に実行するアクションです。<xref:EnvDTE.vsStartUp> から取得されます。|

::: moniker-end

## <a name="tasklist"></a>TaskList

`DTE.Properties("Environment", "TaskList")`

|プロパティ項目名|[値]|説明|
| - |-----------|-----------------|
|ConfirmTaskDeletion|Get/Set (Boolean)|**[タスク一覧]** からタスクを削除する際に確認のダイアログ ボックスを表示するかどうかを指定します。|
|WarnOnAddingHiddenItem|Get/Set (Boolean)|表示されないユーザー タスクを追加したときに警告されるようにするかどうかを指定します。|
|DontShowFilePaths|Get/Set (Boolean)|[タスク一覧] に完全ファイル パスを表示するかどうかを指定します。|
|CommentTokens|SafeArray|コメント トークン値の SafeArray を返します。 各値には、`Name` (文字列) フィールドおよび `Priority` (<xref:EnvDTE.vsTaskPriority>、High、Medium、または Low) フィールドがあります。|

## <a name="web-browser"></a>Web ブラウザー

`DTE.Properties("Environment", "WebBrowser")`

|プロパティ項目名|[値]|説明|
| - |-----------|-----------------|
|HomePage|Get/Set (String)|ホーム ページの URL を表します。|
|SearchPage|Get/Set (String)|検索ページの URL を表します。|
|ViewSourceIn|Get/Set (Enum)|<xref:EnvDTE.vsBrowserViewSource> (Source、Design、External) です。|
|ViewSourceExternalProgram|Get/Set (String)|外部ソース ビューアーのパスです。|

## <a name="see-also"></a>関連項目

- [オプション設定の制御](https://msdn.microsoft.com/Library/a09ed242-7494-4cde-bbd1-7a8ec617965d)
- [オプション ページにあるプロパティ項目名の確認](https://msdn.microsoft.com/Library/d450422d-47c7-4eeb-9f9f-3286264bc5aa)
- [[フォントおよび色] ノード プロパティ ([オプション] ページ)](../../ide/reference/options-page-fonts-and-colors-node-properties.md)
- [[テキスト エディター] ノード プロパティ ([オプション] ページ)](../../ide/reference/options-page-text-editor-node-properties.md)
- [[環境] ([オプション] ダイアログ ボックス)](../../ide/reference/environment-options-dialog-box.md)
