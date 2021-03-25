---
title: ソース管理プラグイン API 関数 |Microsoft Docs
description: ソース管理プラグイン API によって提供される関数について説明します。この機能は、ソース管理プラグインによって実装される必要があります。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, functions
ms.assetid: 4b0536dd-4f92-4ef2-9031-4548281f37aa
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: c28c175d53fb37cf890dad4240a84fb132f6af35
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105090123"
---
# <a name="source-control-plug-in-api-functions"></a>ソース管理プラグインの API 関数
ソース管理プラグイン API には、次の関数が用意されています。これらの関数は、この API に従ってソース管理プラグインによって実装される必要があります。 各関数のシグネチャと、ビットフラグとその他のパラメーターに関連付けられているセマンティクスについては、このリファレンスで詳しく説明します。

## <a name="initialization-and-housekeeping-functions"></a>初期化関数とハウスキーピング関数

|機能|Description|
|--------------|-----------------|
|[SccCloseProject](../extensibility/scccloseproject-function.md)|プロジェクトを閉じます。|
|[SccGetCommandOptions](../extensibility/sccgetcommandoptions-function.md)|指定されたコマンドの詳細オプションをユーザーに表示します。|
|[SccGetVersion](../extensibility/sccgetversion-function.md)|ソース管理プラグインのバージョンを返します。|
|[SccInitialize](../extensibility/sccinitialize-function.md)|ソース管理プラグインを初期化します。 このメソッドは、プラグインのインスタンスごとに1回呼び出されます。|
|[SccOpenProject](../extensibility/sccopenproject-function.md)|プロジェクトを開きます。|
|[SccSetOption](../extensibility/sccsetoption-function.md)|さまざまなオプションを設定するために使用されるジェネリック関数。 各オプションはで始まり `SCC_OPT_xxx` 、独自に定義された値のセットを持ちます。|
|[SccUninitialize](../extensibility/sccuninitialize-function.md)|ソース管理プラグインを取り外す必要があるときに1回呼び出されます。|

## <a name="core-source-control-functions"></a>コアソース管理関数

|機能|Description|
|--------------|-----------------|
|[SccAdd](../extensibility/sccadd-function.md)|完全修飾パス名によって指定されたファイルの配列をソース管理システムに追加します。|
|[SccAddFromScc](../extensibility/sccaddfromscc-function.md)|ソース管理システムに既に存在するファイルをユーザーが参照し、そのファイルを現在のプロジェクトの一部として使用できるようにします。|
|[SccCheckin](../extensibility/scccheckin-function.md)|ファイルの配列をチェックインします。|
|[SccCheckout](../extensibility/scccheckout-function.md)|ファイルの配列をチェックアウトします。|
|[SccDiff](../extensibility/sccdiff-function.md)|完全修飾パス名によって指定されたローカルユーザーのファイルと、ソース管理下のバージョンとの違いを示します。|
|[SccGet](../extensibility/sccget-function.md)|一連のファイルの読み取り専用コピーを取得します。|
|[SccGetEvents](../extensibility/sccgetevents-function.md)|呼び出し元が要求したファイルの状態を確認します (経由 `SccQueryInfo` )。|
|[SccGetProjPath](../extensibility/sccgetprojpath-function.md)|プラグインにとって意味のあるプロジェクトパスをユーザーに確認するために、ソース管理プラグインを使用します。|
|[SccHistory](../extensibility/scchistory-function.md)|完全修飾ローカルファイル名の配列の履歴を表示します。|
|[SccPopulateList](../extensibility/sccpopulatelist-function.md)|ファイルの一覧を調べて、現在の状態を確認します。 さらに、は関数を使用して、 `pfnPopulate` ファイルがの条件に一致しない場合に呼び出し元に通知し `nCommand` ます。|
|[SccProperties](../extensibility/sccproperties-function.md)|完全修飾ファイルのプロパティを表示します。|
|[SccQueryInfo](../extensibility/sccqueryinfo-function.md)|現在の状態に対する完全修飾ファイルの一覧を調べます。|
|[SccRemove](../extensibility/sccremove-function.md)|ソース管理システムから完全修飾ファイルの配列を削除します。|
|[SccRename](../extensibility/sccrename-function.md)|指定されたファイルの名前を、ソース管理システムの新しい名前に変更します。|
|[SccRunScc](../extensibility/sccrunscc-function.md)|ソース管理システムのすべての機能にアクセスします。|
|[SccUncheckout](../extensibility/sccuncheckout-function.md)|ファイルの配列のチェックアウトを元に戻します。|

## <a name="functions-that-support-additional-capability-version-12-of-the-source-control-plug-in-api"></a>追加機能をサポートする関数 (バージョン1.2 のソース管理プラグイン API)
 この関数のグループは、ソース管理プラグイン API のバージョン1.2 に含まれる追加機能を定義します。 これらは、より高度なソース管理機能へのアクセスを提供します。

|機能|Description|
|--------------|-----------------|
|[SccBeginBatch](../extensibility/sccbeginbatch-function.md)|バッチ操作を開始します。|
|[SccCreateSubProject](../extensibility/scccreatesubproject-function.md)|指定された名前のサブプロジェクトを既存の親プロジェクトの下に作成します。|
|[SccDirDiff](../extensibility/sccdirdiff-function.md)|完全修飾パス名とソース管理データベースの場所で指定されたローカルユーザーのディレクトリの違いを示します。|
|[SccDirQueryInfo](../extensibility/sccdirqueryinfo-function.md)|現在の状態の完全修飾ディレクトリの一覧を調べます。|
|[SccEndBatch](../extensibility/sccendbatch-function.md)|バッチ操作を終了します。|
|[SccGetParentProjectPath](../extensibility/sccgetparentprojectpath-function.md)|指定されたプロジェクトの親パスを返します (プロジェクトが存在している必要があります)。|
|[SccIsMultiCheckoutEnabled](../extensibility/sccismulticheckoutenabled-function.md)|ファイルに対する複数のチェックアウトが許可されているかどうかを確認します。|
|[SccWillCreateSccFile](../extensibility/sccwillcreatesccfile-function.md)|プラグインが MSSCCPRJ.SCC を作成するかどうかを確認します。SCC ファイル。|

## <a name="functions-that-support-advanced-capability-version-13-of-the-source-control-plug-in-api"></a>高度な機能をサポートする関数 (バージョン1.3 のソース管理プラグイン API)
 この関数のグループは、ソース管理プラグイン API のバージョン1.3 に含まれる追加機能を定義します。 これらは、より高度なソース管理機能へのアクセスを提供します。

|機能|Description|
|--------------|-----------------|
|[SccAddFilesFromSCC](../extensibility/sccaddfilesfromscc-function.md)|ソース管理から現在のプロジェクトにファイルの一覧を追加します。|
|[SccBackgroundGet](../extensibility/sccbackgroundget-function.md)|ユーザーインターフェイスを使用せずに、ソース管理からファイルのリストを取得します。|
|[SccEnumChangedFiles](../extensibility/sccenumchangedfiles-function.md)|ローカルファイルとは異なるソース管理内のファイルの一覧を取得します。|
|[SccGetExtendedCapabilities](../extensibility/sccgetextendedcapabilities-function.md)|ソース管理プラグインでサポートされている拡張機能を指定するフラグを取得します。|
|[SccGetUserOption](../extensibility/sccgetuseroption-function.md)|ユーザー固有のオプションを取得します。|
|[SccPopulateDirList](../extensibility/sccpopulatedirlist-function.md)|ソース管理下にあるプロジェクトまたはプロジェクト内のディレクトリとファイルの一覧を調べます。 見つかった各ディレクトリとファイル名は、コールバック関数に渡されます。|
|[SccQueryChanges](../extensibility/sccquerychanges-function.md)|ファイルの一覧に対して行われた名前の変更を調べます。 各ファイル名は、変更状態のコールバック関数に渡されます。|

## <a name="requirements"></a>要件
 ヘッダー: scc

 (環境 SDK 共通インクルードフォルダーで提供されます。既定では、 *[drive]* Files\VSIP 8.0 \ EnvSDK\common\inc; は、MSSCCI sample, *[DRIVE]*/MSSCCI) と共に VSIP フォルダーに指定されています。

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン](../extensibility/source-control-plug-ins.md)
- [ソース管理プラグインの作成](../extensibility/internals/creating-a-source-control-plug-in.md)
