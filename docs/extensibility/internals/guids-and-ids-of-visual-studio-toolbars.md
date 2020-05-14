---
title: Visual Studio ツール バーの GUID と ID |マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80708228"
---
# <a name="guids-and-ids-of-visual-studio-toolbars"></a>Visual Studio ツール バーの GUID と ID
このトピックでは、Visual Studio 統合開発環境 (IDE) に含まれるツール バーの GUID と ID の値、および含まれるグループの値を列挙します。 これらの値は、Visual Studio SDK の一部としてインストールされる *.vsct*ファイルで定義されます。 詳細については[、「IDE で定義されたコマンド、メニュー、およびグループ](../../extensibility/internals/ide-defined-commands-menus-and-groups.md)」を参照してください。

> [!NOTE]
> Visual Studio で使用できるツール バーの多くは Visual Studio で定義されておらず、GUID と ID の値はパブリックではありません。 このトピックでは、Visual Studio SDK *.vsct*ファイルで定義されているツール バーのみを一覧表示します。

 *vsct*ファイルで定義されている IDE オブジェクトを操作する方法の詳細については、「[メニューとコマンドを拡張](../../extensibility/extending-menus-and-commands.md)する」を参照してください。

 Visual Studio IDE によって提供される既定のツール`guidSHLMainMenu`バーは、構文を使用`GUID:ID`して指定されている場合を除き、 GUID を使用します。

## <a name="ide-toolbars"></a>IDE ツール バー
 次のツール バーは、Visual Studio IDE によって提供されます。 ツールバーは、[**ツール**] メニューの **[ツールバー** ] サブメニューで選択して表示できます。 ツール ウィンドウのツールバーは、このセクションには含まれません。

 ツールバーから直接降りることができるのはグループだけです。 グループを追加するには、親グループをツールバーの GUID と ID に設定します。 ボタンをツールバーに追加するには、その親をツールバーのグループに設定します。

|ツール バー|id|
|-------------|--------|
|標準|IDM_VS_TOOL_STANDARD|
|ビルド|IDM_VS_TOOL_BUILD|
|テキスト エディター|IDM_VS_TOOL_TEXTEDITOR|
|デバッグ|IDM_DEBUG_TOOLBAR|
|デバッグの場所|IDM_DEBUG_CONTEXT_TOOLBAR|

### <a name="special-toolbars"></a>特別なツールバー
 これらのツール バーは Visual Studio IDE によって定義されますが、特殊な機能を提供し、コマンド グループをホストしません。

|ツール バー|id|
|-------------|--------|
|Add コマンド|IDM_VS_TOOL_ADDCOMMAND|
|未定義。|IDM_VS_TOOL_UNDEFINED|
|XML スキーマ|IDM_VS_TOOL_SCHEMA|
|XML データ|IDM_VS_TOOL_DATA|

## <a name="groups-on-the-ide-toolbars"></a>IDE ツールバーのグループ
 標準ツールバーにボタンを追加するには、次のグループのいずれかを親として設定します。 グループは親ツール バーで並べ替えられます。

### <a name="standard-toolbar-groups"></a>標準ツールバー グループ

|名前|id|
|----------|--------|
|保存/開く|IDG_VS_TOOLSB_SAVEOPEN|
|カット/コピー|IDG_VS_TOOLSB_CUTCOPY|
|元に戻す/やり直し|IDG_VS_TOOLSB_UNDOREDO|
|実行/ビルド|IDG_VS_TOOLSB_RUNBUILD|
|検索|IDG_VS_TOOLSB_SEARCH|
|Windows|IDG_VS_TOOLSB_WINDOWS|
|新しいウィンドウ|IDG_VS_TOOLSB_NEWWINDOWS|
|読み込み/保存|IDG_VS_WINDOWUI_LOADSAVE|
|ゲージ|IDG_VS_TOOLSB_GAUGE|

### <a name="build-toolbar-groups"></a>ツール バー グループの作成

|名前|id|
|----------|--------|
|ビルドバー|IDG_VS_BUILDBAR|
|Cancel|IDG_VS_BUILD_CANCEL|

### <a name="text-editor-toolbar-groups"></a>テキスト エディタ のツール バー グループ

|名前|id|
|----------|--------|
|Completion|IDM_VS_TOOL_TEXTEDITOR|
|Indent|IDG_VS_EDITTOOLBAR_INDENT|
|解説|IDG_VS_EDITTOOLBAR_COMMENT|
|ブックマーク|IDG_VS_EDITTOOLBAR_TEMPBOOKMARKS|

### <a name="debug-toolbar-groups"></a>ツール バー グループのデバッグ

|名前|id|
|----------|--------|
|実行|IDM_DEBUG_TOOLBAR|
|ステップ実行|IDG_DEBUG_TOOLBAR_STEPPING|
|ウォッチ|IDG_DEBUG_TOOLBAR_WATCH|
|Windows|IDG_DEBUG_TOOLBAR_WINDOWS|

### <a name="debug-location-toolbar-groups"></a>デバッグ場所ツールバー グループ

|名前|id|
|----------|--------|
|デバッグの場所|IDG_DEBUG_CONTEXT_TOOLBAR|

## <a name="tool-window-toolbars"></a>ツール ウィンドウのツール バー
 ツール バーは、IDE または**ソリューション エクスプローラ**などのツール ウィンドウに直接表示できます。 ツール ウィンドウは *.vsct*ファイルで定義されていないため、ツール ウィンドウのツール バーには親が定義されていません。 代わりに、コードに配置されます。 次の表は、IDE のツール ウィンドウに表示されるツール バーと、そのツール に含まれるコマンド グループを示しています。

> [!NOTE]
> ツールバーとグループは、 GUID`guidSHLMainMenu`を使用します。 GUID がツール バーに指定されている場合、そのツール バーから降りてくるグループにも適用されます。

|ツール ウィンドウ|ツール バー|グループ|
|-----------------|-------------|------------|
|ソリューション エクスプローラー|IDM_VS_TOOL_PROJWIN|IDG_VS_PROJ_TOOLBAR1.5|
|[サーバー エクスプローラー]|guid_SE_MenuGroup:IDM_SE_TOOLBAR_SERVEREXPLORER|IDG_SE_TOOLBAR_REFRESH|
|Properties|IDM_VS_TOOL_PROPERTIES|IDG_VS_PROPERTIES_SORT<br /><br /> IDG_VS_PROPERTIES_PAGES|
|クラス ビュー|IDM_VS_TOOL_CLASSVIEW|IDG_VS_CLASSVIEW_FOLDERS<br /><br /> IDG_VS_CLASSVIEW_SEARCH<br /><br /> IDG_VS_CLASSVIEW_SETTINGS|
|クラス ビュー|IDM_VS_TOOL_CLASSVIEW_GO|IDG_VS_CLASSVIEW_SEARCH2|
|オブジェクト ブラウザー|IDM_VS_TOOL_OBJBROWSER|IDG_VS_OBJBROWSER_SUBSETS<br /><br /> IDG_VS_OBJBROWSER_SEARCH<br /><br /> IDG_VS_OBJBROWSER_ADDREFERENCE<br /><br /> IDG_VS_OBJBROWSER_BROWSERSETTINGS|
|オブジェクト ブラウザー|IDM_VS_TOOL_OBJECT_BROWSER_GO|IDG_VS_OBJBROWSER_SEARCH2|
|Output|IDM_VS_TOOL_OUTPUTWINDOW|IDG_VS_OUTPUTWINDOW_SELECT<br /><br /> IDG_VS_OUTPUTWINDOW_GOTO<br /><br /> IDG_VS_OUTPUTWINDOW_NEXTPREV<br /><br /> IDG_VS_OUTPUTWINDOW_CLEAR<br /><br /> IDG_VS_OUTPUTWINDOW_WORDWRAP|
|検索と置換|IDM_VS_TOOL_UNIFIEDFIND|IDG_VS_FINDTAB<br /><br /> IDG_VS_REPLACETAB|
|結果の検索 1|IDM_VS_TOOL_FINDRESULTS1|IDG_VS_FINDRESULTS1_GOTO<br /><br /> IDG_VS_FINDRESULTS1_NEXTPREV<br /><br /> IDG_VS_FINDRESULTS1_CLEAR<br /><br /> IDG_VS_FINDRESULTS1_STOPFIND|
|結果の検索 2|IDM_VS_TOOL_FINDRESULTS2|IDG_VS_FINDRESULTS2_GOTO<br /><br /> IDG_VS_FINDRESULTS2_NEXTPREV<br /><br /> IDG_VS_FINDRESULTS2_CLEAR<br /><br /> IDG_VS_FINDRESULTS2_STOPFIND|
|スニペット|IDM_VS_TOOL_SNIPPETMENUS|IDG_VS_SNIPPET_REPL<br /><br /> IDG_VS_SNIPPET_REF<br /><br /> IDG_VS_SNIPPET_PROP|
|ブックマーク|IDM_VS_TOOL_BOOKMARKWIND|IDG_VS_BWNEWFOLDER<br /><br /> IDG_VS_BWNEXTBM<br /><br /> IDG_VS_BWNEXTBMF<br /><br /> IDG_VS_BWENABLE<br /><br /> IDG_VS_BWDELETE|
|タスク一覧|IDM_VS_TOOL_TASKLIST|IDG_VS_TASKLIST_PROVIDERLIST|
|ユーザー タスク|IDM_VS_TOOL_USERTASKS|IDG_VS_TASKLIST_PROVIDERLIST<br /><br /> IDG_VS_USERTASKS_EDIT|
|エラー一覧|IDM_VS_TOOL_ERRORLIST|IDG_VS_ERRORLIST_ERRORGROUP<br /><br /> IDG_VS_ERRORLIST_WARNINGGROUP<br /><br /> IDG_VS_ERRORLIST_MESSAGEGROUP|
|呼び出しブラウザー|IDM_VS_TOOL_CALLBROWSER1.16|IDG_VS_TOOLBAR_CALLBROWSER1_ACTIONS<br /><br /> IDG_VS_TOOLBAR_CALLBROWSER1_TYPE<br /><br /> IDG_VS_TOOLBAR_CALLBROWSER1_CBSETTINGS|
|ブレークポイント|IDM_BREAKPOINTS_WINDOW_TOOLBAR|IDG_BREAKPOINTS_WINDOW_NEW<br /><br /> IDG_BREAKPOINTS_WINDOW_DELETE<br /><br /> IDG_BREAKPOINTS_WINDOW_ALL<br /><br /> IDG_BREAKPOINTS_WINDOW_VIEW<br /><br /> IDG_BREAKPOINTS_WINDOW_EDIT<br /><br /> IDG_BREAKPOINTS_WINDOW_COLUMNS|
|逆アセンブリ|IDM_DISASM_WINDOW_TOOLBAR|IDG_DISASM_WINDOW_TOOLBAR|
|メモリ 1-4|IDM_MEMORY_WINDOW_TOOLBAR1.4|IDG_MEMORY_EXPRESSION1.4<br /><br /> IDG_MEMORY_COLUMNS1.4|
|処理|IDM_ATTACHED_PROCS_TOOLBAR|IDG_ATTACHED_PROCS_EXECCNTRLIDG_ATTACHED_PROCS_STEPPING<br /><br /> IDG_ATTACHED_PROCS_EXECCNTRL2<br /><br /> IDG_ATTACHED_PROCS_ATTACH<br /><br /> IDG_ATTACHED_PROCS_COLUMNS|

## <a name="see-also"></a>関連項目
- [メニュー コントローラをツールバーに追加する](../../extensibility/adding-a-menu-controller-to-a-toolbar.md)
- [ツール ウィンドウにツール バーを追加する](../../extensibility/adding-a-toolbar-to-a-tool-window.md)
- [Visual Studio メニューの GUID と ID](../../extensibility/internals/guids-and-ids-of-visual-studio-menus.md)
