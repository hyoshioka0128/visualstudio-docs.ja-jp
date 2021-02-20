---
title: Visual Studio メニューの Guid と Id |Microsoft Docs
description: Visual Studio 統合開発環境 (IDE) に含まれている Visual Studio のメニューバーで、メニューとグループの GUID と ID の値の一覧を表示します。
ms.custom: SEO-VS-2020
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
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: bd2bdc047ddd5a568aca01ed99b6148b0f288faa
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99970271"
---
# <a name="guids-and-ids-of-visual-studio-menus"></a>Visual Studio メニューの Guid と Id
この記事では、Visual Studio のメニューバーにあるメニューとグループの GUID と ID の値を列挙します。 これらの値は、Visual Studio SDK の一部としてインストールされる、 *vsct* ファイルで定義されています。 詳細については、「 [IDE で定義されたコマンド、メニュー、およびグループ](../../extensibility/internals/ide-defined-commands-menus-and-groups.md)」を参照してください。

 *Vsct* ファイルで定義されている統合開発環境 (IDE) オブジェクトを使用する方法の詳細については、「[メニューとコマンドの拡張](../../extensibility/extending-menus-and-commands.md)」を参照してください。

 Visual Studio のメニューバーのメニューとグループは、GUID を使用し `guidSHLMainMenu` ます。 メニューバー自体の ID は `IDM_VS_TOOL_MAINMENU` です。

## <a name="groups-on-the-visual-studio-menu-bar"></a>Visual Studio のメニューバーのグループ
 メニューバーにメニューを追加するには、これらのグループのいずれかを親として設定します。

|Group|id|
|-----------|--------|
|ファイル/編集/表示|IDG_VS_MM_FILEEDITVIEW|
|リファクタリング|IDG_VS_MM_REFACTORING:|
|Project|IDG_VS_MM_PROJECT|
|ビルド|IDG_VS_MM_BUILDDEBUGRUN|
|形式/ツール|IDG_VS_MM_TOOLSADDINS|
|ウィンドウ/ヘルプ/コミュニティ|IDG_VS_MM_WINDOWHELP|
|Addins|IDG_VS_MM_MACROS|
|FullScreenBar|IDG_VS_MM_FULLSCREENBAR|

## <a name="menus-on-the-visual-studio-menu-bar"></a>Visual Studio のメニューバーのメニュー
 既存の Visual Studio メニューにグループを追加するには、次のいずれかのメニューを親として設定します。 サブメニューは、この一覧には含まれていません。

|メニュー|id|
|----------|--------|
|ファイル|IDM_VS_MENU_FILE|
|[編集]|IDM_VS_MENU_EDIT|
|表示|IDM_VS_MENU_VIEW|
|リファクター|IDM_VS_MENU_REFACTORING|
|Project|IDM_VS_MENU_PROJECT|
|ビルド|IDM_VS_MENU_BUILD|
|フォーマット|IDM_VS_MENU_FORMAT|
|ツール|IDM_VS_MENU_TOOLS|
|Extensions|IDM_VS_MENU_EXTENSIONS|
|ウィンドウ|IDM_VS_MENU_WINDOW|
|Addins|IDM_VS_MENU_ADDINS|
|コミュニティ|IDM_VS_MENU_COMMUNITY|
|Help|IDM_VS_MENU_HELP|

## <a name="groups-on-visual-studio-menus"></a>Visual Studio メニューのグループ
 次の一覧は、Visual Studio のメニューバーのメニューから直接表示されるグループを示しています。 Visual Studio のメニューにコマンドを追加する最も簡単な方法は、これらのグループのいずれかを親として設定することです。 サブメニューから降下したグループは、このセクションには表示されません。

### <a name="file-menu-groups"></a>[ファイル] メニューグループ

|Group|id|
|-----------|--------|
|新規/オープン|IDG_VS_FILE_FILE|
|追加|IDG_VS_FILE_ADD|
|解決策|IDG_VS_FILE_SOLUTION|
|その他|IDG_VS_FILE_MISC|
|保存|IDG_VS_FILE_SAVE|
|[名前の変更]|IDG_VS_FILE_RENAME|
|ブラウザー|IDG_VS_FILE_BROWSER|
|印刷|IDG_VS_FILE_PRINT|
|最近使用|IDG_VS_FILE_MRU|
|詳細ビュー|IDG_VS_FILE_MOVE|
|終了|IDG_VS_FILE_EXIT|

### <a name="edit-menu-groups"></a>メニューグループの編集

|Group|id|
|-----------|--------|
|元に戻す/やり直し|IDG_VS_EDIT_UNDOREDO|
|切り取り/コピー/貼り付け|IDG_VS_EDIT_CUTCOPY|
|Select|IDG_VS_EDIT_SELECT|
|GoTo|IDG_VS_EDIT_GOTO|
|Find|IDG_VS_EDIT_FIND|
|オブジェクト|IDG_VS_EDIT_OBJECTS|
|OLE 動詞|IDG_VS_EDIT_OLEVERBS|
|コマンドウェル|IDG_VS_EDIT_COMMANDWELL|

### <a name="refactor-menu-groups"></a>[リファクター] メニューグループ

|Group|id|
|-----------|--------|
|共通|IDG_REFACTORING_COMMON|
|詳細設定|IDG_REFACTORING_ADVANCED|

### <a name="view-menu-groups"></a>メニューグループの表示

|Group|id|
|-----------|--------|
|フォームコード|IDG_VS_VIEW_FORMCODE|
|ブラウザー|IDG_VS_VIEW_BROWSER|
|ビューの定義|IDG_VS_VIEW_DEFINEVIEWS|
|Windows|IDG_VS_VIEW_WINDOWS|
|Windows の設計|IDG_VS_VIEW_ARCH_WINDOWS|
|組織のウィンドウ|IDG_VS_VIEW_ORG_WINDOWS|
|コードブラウザー|IDG_VS_VIEW_CODEBROWSENAV_WINDOWS|
|開発用ウィンドウ|IDG_VS_VIEW_DEV_WINDOWS|
|ツールバー|IDG_VS_VIEW_TOOLBARS|
|Symbols|IDG_VS_VIEW_SYMBOLNAVIGATE|
|Navigate|IDG_VS_VIEW_NAVIGATE|
|小さいナビゲーション|IDG_VS_VIEW_SMALLNAVIGATE|
|オブジェクト ブラウザー|IDG_VS_VIEW_OBJBRWSR|
|コマンドウェル|IDG_VS_VIEW_COMMANDWELL|
|[プロパティ ページ]|IDG_VS_VIEW_PROPPAGES|
|更新|IDG_VS_VIEW_REFRESH|

### <a name="project-menu-groups"></a>[プロジェクト] メニューグループ

|Group|id|
|-----------|--------|
|その他の追加|IDG_VS_PROJ_MISCADD|
|追加|IDG_VS_PROJ_ADD|
|Folder|IDG_VS_PROJ_FOLDER|
|アンロード/再読み込み|IDG_VS_PROJ_UNLOADRELOAD|
|リファレンス|IDG_VS_PROJ_REFERENCE|
|オプション|IDG_VS_PROJ_OPTIONS|
|設定|IDG_VS_PROJ_SETTINGS|

### <a name="build-menu-groups"></a>ビルドメニューグループ

|Group|id|
|-----------|--------|
|解決策|IDG_VS_BUILD_SOLUTION|
|選択|IDG_VS_BUILD_SELECTION|
|ガイド付き最適化のプロファイル|IDG_VS_PGO_SELECTION|
|その他|IDG_VS_BUILD_MISC|
|キャンセル|IDG_VS_BUILD_CANCEL|

### <a name="tools-menu-groups"></a>[ツール] メニューグループ

|Group|id|
|-----------|--------|
|コマンド ライン|IDG_VS_TOOLS_CMDLINE|
|スニペット|IDG_VS_TOOLS_SNIPPETS|
|オブジェクトのサブセット|IDG_VS_TOOLS_OBJSUBSET|
|オプション|IDG_VS_TOOLS_OPTIONS|
|その他2|IDG_VS_TOOLS_OTHER2|
|[外部ツール]|IDG_VS_TOOLS_EXT_TOOLS|
|外部のカスタマイズ|IDG_VS_TOOLS_EXT_CUST|

### <a name="window-menu-groups"></a>ウィンドウメニューグループ

|Group|id|
|-----------|--------|
|新規|IDG_VS_WINDOW_NEW|
|Dock/Close|IDG_VS_DOCKCLOSE|
|Dock/Hide|IDG_VS_DOCKHIDE|
|整列|IDG_VS_WINDOW_ARRANGE|
|［ナビゲーション］|IDG_VS_WINDOW_NAVIGATION|
|List|IDG_VS_WINDOW_LIST|

### <a name="help-menu-groups"></a>ヘルプメニューグループ

|Group|id|
|-----------|--------|
|サンプル|IDG_VS_HELP_SAMPLES|
|サポート|IDG_VS_HELP_SUPPORT|
|バージョン情報|IDG_VS_HELP_ABOUT|

## <a name="submenus-of-visual-studio-menus"></a>Visual Studio メニューのサブメニュー
 次の階層は、Visual Studio のメニューバーのメニューに関連付けられているサブメニューを示しています。 親としてメニューを持つことができるのはグループのみなので、すべてのサブメニューは、メニューから直接ではなく、メニュー上のグループから降下する必要があります。 メニュー、グループ、サブメニュー間の関係の詳細については、「 [メニューへのサブメニューの追加](../../extensibility/adding-a-submenu-to-a-menu.md)」を参照してください。

> [!NOTE]
> Visual Studio のメニューバーのメニュー名は、次のように IDE のグループの名前付け規則から推論できるため、この階層では個別に表示されません: *IDG_VS_ \<Menu Name\> _ \<Group Name\>*。

|[親グループ]|揃える|子グループ|
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
|||IDG_VS_WNDO_OTRWNDWS1...4/6|
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
- [Visual Studio ツールバーの Guid と Id](../../extensibility/internals/guids-and-ids-of-visual-studio-toolbars.md)
- [Visual Studio コマンドの Guid と Id](../../extensibility/internals/guids-and-ids-of-visual-studio-commands.md)
- [Visual Studio コマンドテーブル (vsct) ファイル](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
