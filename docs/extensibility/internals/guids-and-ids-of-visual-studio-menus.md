---
title: ビジュアルスタジオメニューのGUIDとID |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- visual studio menus
- visual studio groups
- id
- existing menus
- guid
- menus
ms.assetid: 84639d86-dd21-4b35-9988-6bb654162488
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a656d5cb9a126a9dc3988d70a290fceb3e56439e
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80708243"
---
# <a name="guids-and-ids-of-visual-studio-menus"></a>Visual Studio メニューの GUID と ID
この資料では、Visual Studio のメニュー バーのメニューとグループの GUID と ID の値を列挙します。 これらの値は、Visual Studio SDK の一部としてインストールされる *.vsct*ファイルで定義されます。 詳細については[、「IDE で定義されたコマンド、メニュー、およびグループ](../../extensibility/internals/ide-defined-commands-menus-and-groups.md)」を参照してください。

 *vsct*ファイルで定義されている統合開発環境 (IDE) オブジェクトを操作する方法の詳細については、「[メニューとコマンドの拡張](../../extensibility/extending-menus-and-commands.md)」を参照してください。

 Visual Studio のメニュー バーのメニューとグループでは`guidSHLMainMenu`、 GUID を使用します。 メニュー バー自体の ID`IDM_VS_TOOL_MAINMENU`は、 です。

## <a name="groups-on-the-visual-studio-menu-bar"></a>Visual Studio のメニュー バーのグループ
 メニュー バーにメニューを追加するには、これらのグループの 1 つを親グループとして設定します。

|グループ|id|
|-----------|--------|
|ファイル/編集/表示|IDG_VS_MM_FILEEDITVIEW|
|Refactoring|IDG_VS_MM_REFACTORING:|
|Project|IDG_VS_MM_PROJECT|
|ビルド|IDG_VS_MM_BUILDDEBUGRUN|
|フォーマット/ツール|IDG_VS_MM_TOOLSADDINS|
|ウィンドウ/ヘルプ/コミュニティ|IDG_VS_MM_WINDOWHELP|
|Addins|IDG_VS_MM_MACROS|
|フルスクリーンバー|IDG_VS_MM_FULLSCREENBAR|

## <a name="menus-on-the-visual-studio-menu-bar"></a>Visual Studio メニュー バーのメニュー
 既存の Visual Studio メニューにグループを追加するには、次のいずれかのメニューを親として設定します。 サブメニューはこのリストには含まれません。

|メニュー|id|
|----------|--------|
|ファイル|IDM_VS_MENU_FILE|
|[編集]|IDM_VS_MENU_EDIT|
|View|IDM_VS_MENU_VIEW|
|リファクター|IDM_VS_MENU_REFACTORING|
|Project|IDM_VS_MENU_PROJECT|
|ビルド|IDM_VS_MENU_BUILD|
|Format|IDM_VS_MENU_FORMAT|
|ツール|IDM_VS_MENU_TOOLS|
|拡張機能|IDM_VS_MENU_EXTENSIONS|
|ウィンドウ|IDM_VS_MENU_WINDOW|
|Addins|IDM_VS_MENU_ADDINS|
|コミュニティ|IDM_VS_MENU_COMMUNITY|
|Help|IDM_VS_MENU_HELP|

## <a name="groups-on-visual-studio-menus"></a>ビジュアル スタジオ メニューのグループ
 次の一覧は、Visual Studio のメニュー バーのメニューから直接降りてくるグループを示しています。 Visual Studio メニューにコマンドを追加する最も簡単な方法は、これらのグループのいずれかを親として設定することです。 サブメニューから下位のグループは、このセクションには表示されません。

### <a name="file-menu-groups"></a>ファイル メニュー グループ

|グループ|id|
|-----------|--------|
|新規/オープン|IDG_VS_FILE_FILE|
|追加|IDG_VS_FILE_ADD|
|ソリューション|IDG_VS_FILE_SOLUTION|
|その他|IDG_VS_FILE_MISC|
|保存|IDG_VS_FILE_SAVE|
|名前の変更|IDG_VS_FILE_RENAME|
|Browser|IDG_VS_FILE_BROWSER|
|Print|IDG_VS_FILE_PRINT|
|最近使用した|IDG_VS_FILE_MRU|
|詳細ビュー|IDG_VS_FILE_MOVE|
|Exit|IDG_VS_FILE_EXIT|

### <a name="edit-menu-groups"></a>メニュー グループの編集

|グループ|id|
|-----------|--------|
|元に戻す/やり直し|IDG_VS_EDIT_UNDOREDO|
|切り取り/コピー/貼り付け|IDG_VS_EDIT_CUTCOPY|
|Select|IDG_VS_EDIT_SELECT|
|GoTo|IDG_VS_EDIT_GOTO|
|Find|IDG_VS_EDIT_FIND|
|Objects|IDG_VS_EDIT_OBJECTS|
|OLE 動詞|IDG_VS_EDIT_OLEVERBS|
|コマンドウェル|IDG_VS_EDIT_COMMANDWELL|

### <a name="refactor-menu-groups"></a>リファクタリング メニュー グループ

|グループ|id|
|-----------|--------|
|共通|IDG_REFACTORING_COMMON|
|詳細設定|IDG_REFACTORING_ADVANCED|

### <a name="view-menu-groups"></a>メニュー グループの表示

|グループ|id|
|-----------|--------|
|フォームコード|IDG_VS_VIEW_FORMCODE|
|Browser|IDG_VS_VIEW_BROWSER|
|ビューの定義|IDG_VS_VIEW_DEFINEVIEWS|
|Windows|IDG_VS_VIEW_WINDOWS|
|ウィンドウズの設計|IDG_VS_VIEW_ARCH_WINDOWS|
|組織ウィンドウ|IDG_VS_VIEW_ORG_WINDOWS|
|コード ブラウザー|IDG_VS_VIEW_CODEBROWSENAV_WINDOWS|
|ウィンドウズを開発する|IDG_VS_VIEW_DEV_WINDOWS|
|[ツール バー]|IDG_VS_VIEW_TOOLBARS|
|Symbols|IDG_VS_VIEW_SYMBOLNAVIGATE|
|Navigate|IDG_VS_VIEW_NAVIGATE|
|小さなナビゲート|IDG_VS_VIEW_SMALLNAVIGATE|
|オブジェクト ブラウザー|IDG_VS_VIEW_OBJBRWSR|
|コマンドウェル|IDG_VS_VIEW_COMMANDWELL|
|[プロパティ ページ]|IDG_VS_VIEW_PROPPAGES|
|更新|IDG_VS_VIEW_REFRESH|

### <a name="project-menu-groups"></a>プロジェクト メニュー グループ

|グループ|id|
|-----------|--------|
|その他の追加|IDG_VS_PROJ_MISCADD|
|追加|IDG_VS_PROJ_ADD|
|Folder|IDG_VS_PROJ_FOLDER|
|アンロード/リロード|IDG_VS_PROJ_UNLOADRELOAD|
|リファレンス|IDG_VS_PROJ_REFERENCE|
|オプション|IDG_VS_PROJ_OPTIONS|
|設定|IDG_VS_PROJ_SETTINGS|

### <a name="build-menu-groups"></a>ビルド メニュー グループ

|グループ|id|
|-----------|--------|
|ソリューション|IDG_VS_BUILD_SOLUTION|
|[選択]|IDG_VS_BUILD_SELECTION|
|ガイド付き最適化のプロファイル|IDG_VS_PGO_SELECTION|
|その他|IDG_VS_BUILD_MISC|
|Cancel|IDG_VS_BUILD_CANCEL|

### <a name="tools-menu-groups"></a>ツール メニュー グループ

|グループ|id|
|-----------|--------|
|コマンド ライン|IDG_VS_TOOLS_CMDLINE|
|スニペット|IDG_VS_TOOLS_SNIPPETS|
|オブジェクトサブセット|IDG_VS_TOOLS_OBJSUBSET|
|オプション|IDG_VS_TOOLS_OPTIONS|
|その他 2|IDG_VS_TOOLS_OTHER2|
|[外部ツール]|IDG_VS_TOOLS_EXT_TOOLS|
|外部カスタマイズ|IDG_VS_TOOLS_EXT_CUST|

### <a name="window-menu-groups"></a>ウィンドウ メニュー グループ

|グループ|id|
|-----------|--------|
|新規作成|IDG_VS_WINDOW_NEW|
|ドック/クローズ|IDG_VS_DOCKCLOSE|
|ドック/非表示|IDG_VS_DOCKHIDE|
|整列|IDG_VS_WINDOW_ARRANGE|
|「ナビゲーション」|IDG_VS_WINDOW_NAVIGATION|
|List|IDG_VS_WINDOW_LIST|

### <a name="help-menu-groups"></a>ヘルプ メニュー グループ

|グループ|id|
|-----------|--------|
|サンプル|IDG_VS_HELP_SAMPLES|
|サポート|IDG_VS_HELP_SUPPORT|
|概要|IDG_VS_HELP_ABOUT|

## <a name="submenus-of-visual-studio-menus"></a>ビジュアル スタジオ メニューのサブメニュー
 次の階層は、Visual Studio のメニュー バーのメニューに関連付けられているサブメニューを示しています。 グループだけが親としてメニューを持つことができるので、すべてのサブメニューはメニューから直接ではなく、メニュー上のグループから降りる必要があります。 メニュー、グループ、およびサブメニュー間の関係の詳細については、「[メニューへのサブメニューの追加」を](../../extensibility/adding-a-submenu-to-a-menu.md)参照してください。

> [!NOTE]
> Visual Studio のメニュー バーのメニューの名前は*\<\>IDG_VS_、IDE\<\>* のグループの名前付け規則から推測できるため、この階層では個別に表示されません。

|[親グループ]|サブメニュー|子グループ|
|------------------|-------------|------------------|
|IDG_VS_FILE_FILE|IDM_VS_CSCD_NEW|IDG_VS_FILE_NEW_CASCADE|
||IDM_VS_CSCD_OPEN|IDG_VS_FILE_OPENP_CASCADE|
|||IDG_VS_FILE_OPENF_CASCADE|
|IDG_VS_FILE_ADD|IDM_VS_CSCD_ADD|IDG_VS_FILE_ADD_PROJECT_NEW|
|||IDG_VS_FILE_ADD_PROJECT_EXI|
|IDG_VS_FILE_MRU|IDM_VS_CSCD_FILEMRU|IDG_VS_FILE_FMRU_CASCADE|
||IDM_VS_CSCD_PROJMRU|IDG_VS_FILE_PMRU_CASCADE|
|IDG_VS_FILE_MOVE|IDM_VS_CSCD_MOVETOPRJ|IDG_VS_FILE_MOVE_CASCADE|
|||IDG_VS_FILE_MOVE_PICKER|
|IDG_VS_VIEW_DEV_WINDOWS|IDM_VS_CSCD_FINDRESULTS|IDG_VS_WNDO_FINDRESULTS|
||IDM_VS_CSCD_WINDOWS|IDG_VS_VIEW_CALLBROWSER|
|||IDG_VS_WNDO_OTRWNDWS1.6|
|||IDG_VS_WNDO_WINDOWS2|
|IDG_VS_VIEW_TOOLBARS|IDM_VS_CSCD_COMMANDBARS||
|IDG_VS_EDIT_GOTO|IDM_VS_EDITOR_FIND_MENU||
|IDG_VS_EDIT_OBJECTS|IDM_VS_CSCD_MNUDES|IDG_VS_MNUDES_INSERT|
|||IDG_VS_MNUDES_EDITNAMES|
||IDM_VS_CSCD_OLEVERBS|IDG_VS_EDIT_OLEVERBS|
|IDG_VS_BUILD_SELECTION|IDM_VS_CSCD_BUILD|IDG_VS_BUILD_CASCADE|
|||IDG_VS_BUILD_PROJPICKER|
||IDM_VS_CSCD_REBUILD|IDG_VS_REBUILD_CASCADE|
|||IDG_VS_REBUILD_PROJPICKER|
||IDM_VS_CSCD_PROJONLY|IDG_VS_PROJONLY_CASCADE|
||IDM_VS_CSCD_CLEAN|IDG_VS_CLEAN_CASCADE|
|||IDG_VS_CLEAN_PROJPICKER|
||IDM_VS_CSCD_DEPLOY|IDG_VS_DEPLOY_CASCADE|
|||IDG_VS_DEPLOY_PROJPICKER|
|IDG_VS_PGO_SELECTION|IDM_VS_CSCD_PGO_BUILD|IDG_VS_PGO_BUILD_CASCADE_BUILD|
|||IDG_VS_PGO_BUILD_CASCADE_RUN|

## <a name="see-also"></a>関連項目
- [Visual Studio ツール バーの GUID と ID](../../extensibility/internals/guids-and-ids-of-visual-studio-toolbars.md)
- [Visual Studio コマンドの GUID と ID](../../extensibility/internals/guids-and-ids-of-visual-studio-commands.md)
- [Visual Studio コマンド テーブル (.vsct) ファイル](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
