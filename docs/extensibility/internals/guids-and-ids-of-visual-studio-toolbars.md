---
title: Visual Studio のツールバーの Guid と Id |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- visual studio groups
- toolbars
- visual studio toolbar
- id
- toolgar group
- tool window toolbar
- guid
ms.assetid: c9cacd57-9225-450f-a9ac-cbf3168ea844
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: fe42821cdacc038d767e52373d45ddd7b8954323
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80708228"
---
# <a name="guids-and-ids-of-visual-studio-toolbars"></a>Visual Studio ツールバーの Guid と Id
このトピックでは、Visual Studio 統合開発環境 (IDE: integrated development environment) に含まれるツールバーの GUID と ID の値、およびそれらに含まれるグループについて説明します。 これらの値は、Visual Studio SDK の一部としてインストールされる、 *vsct* ファイルで定義されています。 詳細については、「 [IDE で定義されたコマンド、メニュー、およびグループ](../../extensibility/internals/ide-defined-commands-menus-and-groups.md)」を参照してください。

> [!NOTE]
> Visual Studio で使用できるツールバーの多くは、Visual Studio によって定義されていません。 GUID と ID の値はパブリックではありません。 このトピックでは、Visual Studio SDK の *vsct* ファイルで定義されているツールバーのみを示します。

 *Vsct*ファイルで定義されている IDE オブジェクトを操作する方法の詳細については、「[メニューとコマンドの拡張](../../extensibility/extending-menus-and-commands.md)」を参照してください。

 Visual Studio IDE によって提供される既定のツールバーでは、GUID が使用 `guidSHLMainMenu` されます。ただし、構文を使用して指定しない場合は除き `GUID:ID` ます。

## <a name="ide-toolbars"></a>IDE ツール バー
 次のツールバーは、Visual Studio IDE によって提供されます。 ツールバーを表示するには、[**ツール**] メニューの [ツール**バー** ] サブメニューからツールバーを選択します。 ツールウィンドウのツールバーは、このセクションには含まれていません。

 グループのみが、ツールバーから直接降下できます。 グループを追加するには、その親をツールバーの GUID と ID に設定します。 ツールバーにボタンを追加するには、ツールバーの [親] を [グループ] に設定します。

|ツール バー|ID|
|-------------|--------|
|Standard|IDM_VS_TOOL_STANDARD|
|Build|IDM_VS_TOOL_BUILD|
|テキスト エディター|IDM_VS_TOOL_TEXTEDITOR|
|デバッグ|guidVSDebugGroup: IDM_DEBUG_TOOLBAR|
|デバッグの場所|guidVSDebugGroup: IDM_DEBUG_CONTEXT_TOOLBAR|

### <a name="special-toolbars"></a>特殊なツールバー
 これらのツールバーは、Visual Studio IDE によって定義されていますが、特化された機能を提供し、コマンドグループをホストしません。

|ツール バー|ID|
|-------------|--------|
|Add コマンド|IDM_VS_TOOL_ADDCOMMAND|
|未定義。|IDM_VS_TOOL_UNDEFINED|
|XML スキーマ|IDM_VS_TOOL_SCHEMA|
|XML データ|IDM_VS_TOOL_DATA|

## <a name="groups-on-the-ide-toolbars"></a>IDE ツールバーのグループ
 標準ツールバーにボタンを追加するには、次のいずれかのグループを親として設定します。 グループは、親ツールバーで並べ替えられます。

### <a name="standard-toolbar-groups"></a>標準のツールバーグループ

|名前|id|
|----------|--------|
|保存/開く|IDG_VS_TOOLSB_SAVEOPEN|
|切り取り/コピー|IDG_VS_TOOLSB_CUTCOPY|
|元に戻す/やり直し|IDG_VS_TOOLSB_UNDOREDO|
|実行/ビルド|IDG_VS_TOOLSB_RUNBUILD|
|検索|IDG_VS_TOOLSB_SEARCH|
|Windows|IDG_VS_TOOLSB_WINDOWS|
|新しいウィンドウ|IDG_VS_TOOLSB_NEWWINDOWS|
|読み込み/保存|IDG_VS_WINDOWUI_LOADSAVE|
|ゲージ|IDG_VS_TOOLSB_GAUGE|

### <a name="build-toolbar-groups"></a>ツールバーグループの作成

|名前|id|
|----------|--------|
|ビルドバー|IDG_VS_BUILDBAR|
|キャンセル|IDG_VS_BUILD_CANCEL|

### <a name="text-editor-toolbar-groups"></a>テキストエディターのツールバーグループ

|名前|id|
|----------|--------|
|Completion|IDM_VS_TOOL_TEXTEDITOR|
|インデントする|IDG_VS_EDITTOOLBAR_INDENT|
|解説|IDG_VS_EDITTOOLBAR_COMMENT|
|ブックマーク|IDG_VS_EDITTOOLBAR_TEMPBOOKMARKS|

### <a name="debug-toolbar-groups"></a>デバッグツールバーグループ

|名前|id|
|----------|--------|
|実行|IDM_DEBUG_TOOLBAR|
|ステップ実行|IDG_DEBUG_TOOLBAR_STEPPING|
|Watch|IDG_DEBUG_TOOLBAR_WATCH|
|Windows|IDG_DEBUG_TOOLBAR_WINDOWS|

### <a name="debug-location-toolbar-groups"></a>デバッグの場所のツールバーグループ

|名前|id|
|----------|--------|
|デバッグの場所|IDG_DEBUG_CONTEXT_TOOLBAR|

## <a name="tool-window-toolbars"></a>ツール ウィンドウのツール バー
 ツールバーは、IDE またはツールウィンドウ ( **ソリューションエクスプローラー**など) で直接表示できます。 ツールウィンドウは *. vsct* ファイルで定義されていないため、ツールウィンドウのツールバーには定義済みの親がありません。 代わりに、コード内に配置されます。 次の表は、IDE のツールウィンドウに表示されるツールバーと、それらに含まれるコマンドグループを示しています。

> [!NOTE]
> ツールバーとグループは GUID `guidSHLMainMenu` を使用します。ただし、guid: ID 構文を使用して指定した場合を除きます。 ツールバーに対して GUID が指定されている場合は、そのツールバーから下にあるグループにも適用されます。

|ツールウィンドウ|ツール バー|グループ|
|-----------------|-------------|------------|
|ソリューション エクスプローラー|IDM_VS_TOOL_PROJWIN|IDG_VS_PROJ_TOOLBAR1..5/5|
|[サーバー エクスプローラー]|guid_SE_MenuGroup: IDM_SE_TOOLBAR_SERVEREXPLORER|IDG_SE_TOOLBAR_REFRESH|
|Properties|IDM_VS_TOOL_PROPERTIES|IDG_VS_PROPERTIES_SORT<br /><br /> IDG_VS_PROPERTIES_PAGES|
|クラス ビュー|IDM_VS_TOOL_CLASSVIEW|IDG_VS_CLASSVIEW_FOLDERS<br /><br /> IDG_VS_CLASSVIEW_SEARCH<br /><br /> IDG_VS_CLASSVIEW_SETTINGS|
|クラス ビュー|IDM_VS_TOOL_CLASSVIEW_GO|IDG_VS_CLASSVIEW_SEARCH2|
|オブジェクト ブラウザー|IDM_VS_TOOL_OBJBROWSER|IDG_VS_OBJBROWSER_SUBSETS<br /><br /> IDG_VS_OBJBROWSER_SEARCH<br /><br /> IDG_VS_OBJBROWSER_ADDREFERENCE<br /><br /> IDG_VS_OBJBROWSER_BROWSERSETTINGS|
|オブジェクト ブラウザー|IDM_VS_TOOL_OBJECT_BROWSER_GO|IDG_VS_OBJBROWSER_SEARCH2|
|出力|IDM_VS_TOOL_OUTPUTWINDOW|IDG_VS_OUTPUTWINDOW_SELECT<br /><br /> IDG_VS_OUTPUTWINDOW_GOTO<br /><br /> IDG_VS_OUTPUTWINDOW_NEXTPREV<br /><br /> IDG_VS_OUTPUTWINDOW_CLEAR<br /><br /> IDG_VS_OUTPUTWINDOW_WORDWRAP|
|検索と置換|IDM_VS_TOOL_UNIFIEDFIND|IDG_VS_FINDTAB<br /><br /> IDG_VS_REPLACETAB|
|検索結果1|IDM_VS_TOOL_FINDRESULTS1|IDG_VS_FINDRESULTS1_GOTO<br /><br /> IDG_VS_FINDRESULTS1_NEXTPREV<br /><br /> IDG_VS_FINDRESULTS1_CLEAR<br /><br /> IDG_VS_FINDRESULTS1_STOPFIND|
|検索結果2|IDM_VS_TOOL_FINDRESULTS2|IDG_VS_FINDRESULTS2_GOTO<br /><br /> IDG_VS_FINDRESULTS2_NEXTPREV<br /><br /> IDG_VS_FINDRESULTS2_CLEAR<br /><br /> IDG_VS_FINDRESULTS2_STOPFIND|
|スニペット|IDM_VS_TOOL_SNIPPETMENUS|IDG_VS_SNIPPET_REPL<br /><br /> IDG_VS_SNIPPET_REF<br /><br /> IDG_VS_SNIPPET_PROP|
|ブックマーク|IDM_VS_TOOL_BOOKMARKWIND|IDG_VS_BWNEWFOLDER<br /><br /> IDG_VS_BWNEXTBM<br /><br /> IDG_VS_BWNEXTBMF<br /><br /> IDG_VS_BWENABLE<br /><br /> IDG_VS_BWDELETE|
|タスク一覧|IDM_VS_TOOL_TASKLIST|IDG_VS_TASKLIST_PROVIDERLIST|
|ユーザー タスク|IDM_VS_TOOL_USERTASKS|IDG_VS_TASKLIST_PROVIDERLIST<br /><br /> IDG_VS_USERTASKS_EDIT|
|エラー一覧|IDM_VS_TOOL_ERRORLIST|IDG_VS_ERRORLIST_ERRORGROUP<br /><br /> IDG_VS_ERRORLIST_WARNINGGROUP<br /><br /> IDG_VS_ERRORLIST_MESSAGEGROUP|
|呼び出しブラウザー|IDM_VS_TOOL_CALLBROWSER1..まで|IDG_VS_TOOLBAR_CALLBROWSER1_ACTIONS<br /><br /> IDG_VS_TOOLBAR_CALLBROWSER1_TYPE<br /><br /> IDG_VS_TOOLBAR_CALLBROWSER1_CBSETTINGS|
|ブレークポイント|guidVSDebugGroup: IDM_BREAKPOINTS_WINDOW_TOOLBAR|IDG_BREAKPOINTS_WINDOW_NEW<br /><br /> IDG_BREAKPOINTS_WINDOW_DELETE<br /><br /> IDG_BREAKPOINTS_WINDOW_ALL<br /><br /> IDG_BREAKPOINTS_WINDOW_VIEW<br /><br /> IDG_BREAKPOINTS_WINDOW_EDIT<br /><br /> IDG_BREAKPOINTS_WINDOW_COLUMNS|
|逆アセンブリ|guidVSDebugGroup: IDM_DISASM_WINDOW_TOOLBAR|IDG_DISASM_WINDOW_TOOLBAR|
|メモリ1-4|guidVSDebugGroup: IDM_MEMORY_WINDOW_TOOLBAR1...4/4|IDG_MEMORY_EXPRESSION1..4/4<br /><br /> IDG_MEMORY_COLUMNS1..4/4|
|処理|guidVSDebugGroup: IDM_ATTACHED_PROCS_TOOLBAR|IDG_ATTACHED_PROCS_EXECCNTRL IDG_ATTACHED_PROCS_STEPPING<br /><br /> IDG_ATTACHED_PROCS_EXECCNTRL2<br /><br /> IDG_ATTACHED_PROCS_ATTACH<br /><br /> IDG_ATTACHED_PROCS_COLUMNS|

## <a name="see-also"></a>関連項目
- [ツールバーにメニューコントローラーを追加する](../../extensibility/adding-a-menu-controller-to-a-toolbar.md)
- [ツールウィンドウにツールバーを追加する](../../extensibility/adding-a-toolbar-to-a-tool-window.md)
- [Visual Studio メニューの Guid と Id](../../extensibility/internals/guids-and-ids-of-visual-studio-menus.md)
