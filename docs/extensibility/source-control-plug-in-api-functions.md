---
title: ソース管理プラグイン API 関数 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, functions
ms.assetid: 4b0536dd-4f92-4ef2-9031-4548281f37aa
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ce685729dda8750d772e244398b736cff4951b72
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80699923"
---
# <a name="source-control-plug-in-api-functions"></a>ソース管理プラグインの API 関数
ソース管理プラグイン API には、この API に従ってソース管理プラグインによって実装する必要がある次の関数が用意されています。 各関数のシグネチャ、およびビット フラグおよびその他のパラメーターに関連付けられたセマンティクスについては、このリファレンスで詳しく説明します。

## <a name="initialization-and-housekeeping-functions"></a>初期化およびハウスキーピング機能

|機能|説明|
|--------------|-----------------|
|[SccCloseProject](../extensibility/scccloseproject-function.md)|プロジェクトを閉じます。|
|[SccGetCommandOptions](../extensibility/sccgetcommandoptions-function.md)|指定したコマンドの詳細オプションをユーザーに求めます。|
|[SccGetVersion](../extensibility/sccgetversion-function.md)|ソース管理プラグインのバージョンを返します。|
|[SccInitialize](../extensibility/sccinitialize-function.md)|ソース管理プラグインを初期化します。 プラグインの各インスタンスに対して 1 回呼び出されます。|
|[SccOpenProject](../extensibility/sccopenproject-function.md)|プロジェクトを開きます。|
|[SccSetOption](../extensibility/sccsetoption-function.md)|さまざまなオプションを設定するために使用される汎用関数。 各オプションは、`SCC_OPT_xxx`最初に、独自に定義された値のセットを持ちます。|
|[SccUninitialize](../extensibility/sccuninitialize-function.md)|ソース管理プラグインを取り外す必要がある場合に 1 回呼び出されます。|

## <a name="core-source-control-functions"></a>コア ソースコントロール関数

|機能|説明|
|--------------|-----------------|
|[SccAdd](../extensibility/sccadd-function.md)|完全修飾パス名で指定されたファイルの配列をソース管理システムに追加します。|
|[SccAddFromScc](../extensibility/sccaddfromscc-function.md)|ユーザーは、ソース管理システムに既に存在するファイルを参照し、それらのファイルを現在のプロジェクトの一部にできます。|
|[SccCheckin](../extensibility/scccheckin-function.md)|ファイルの配列をチェックインします。|
|[SccCheckout](../extensibility/scccheckout-function.md)|ファイルの配列をチェックアウトします。|
|[SccDiff](../extensibility/sccdiff-function.md)|完全修飾パス名で指定されたローカル ユーザーのファイルとソース管理下のバージョンの違いを示します。|
|[SccGet](../extensibility/sccget-function.md)|ファイルのセットの読み取り専用コピーを取得します。|
|[SccGetEvents](../extensibility/sccgetevents-function.md)|呼び出し元が (を介して)`SccQueryInfo`要求したファイルの状態をチェックします。|
|[SccGetProjPath](../extensibility/sccgetprojpath-function.md)|ソース管理プラグインに、プラグインにとって意味のあるプロジェクト パスを求めるメッセージを表示します。|
|[SccHistory](../extensibility/scchistory-function.md)|完全修飾ローカルファイル名の配列の履歴を表示します。|
|[SccPopulateList](../extensibility/sccpopulatelist-function.md)|ファイルのリストで現在のステータスを調べます。 また、ファイルが`pfnPopulate`の条件に一致しない場合に、この関数を使用して呼`nCommand`び出し元に通知します。|
|[SccProperties](../extensibility/sccproperties-function.md)|完全修飾ファイルのプロパティを表示します。|
|[SccQueryInfo](../extensibility/sccqueryinfo-function.md)|現在の状態に関する完全修飾ファイルの一覧を調べます。|
|[SccRemove](../extensibility/sccremove-function.md)|ソース管理システムから完全修飾ファイルの配列を削除します。|
|[SccRename](../extensibility/sccrename-function.md)|指定したファイルの名前をソース管理システムの新しい名前に変更します。|
|[SccRunScc](../extensibility/sccrunscc-function.md)|ソース管理システムの機能の全範囲にアクセスします。|
|[SccUncheckout](../extensibility/sccuncheckout-function.md)|ファイルの配列のチェックアウトを取り消します。|

## <a name="functions-that-support-additional-capability-version-12-of-the-source-control-plug-in-api"></a>追加機能をサポートする機能 (ソース管理プラグイン API のバージョン 1.2)
 この関数グループは、ソース管理プラグイン API のバージョン 1.2 に含まれる追加機能を定義します。 これらの機能により、より高度なソース管理機能にアクセスできます。

|機能|説明|
|--------------|-----------------|
|[SccBeginBatch](../extensibility/sccbeginbatch-function.md)|バッチ操作を開始します。|
|[SccCreateSubProject](../extensibility/scccreatesubproject-function.md)|既存の親プロジェクトの下に指定した名前のサブプロジェクトを作成します。|
|[SccDirDiff](../extensibility/sccdirdiff-function.md)|完全修飾パス名で指定されたローカル ユーザーのディレクトリとソース管理データベースの場所の違いを示します。|
|[SccDirQueryInfo](../extensibility/sccdirqueryinfo-function.md)|現在の状態に関する完全修飾ディレクトリの一覧を調べます。|
|[SccEndBatch](../extensibility/sccendbatch-function.md)|バッチ操作を終了します。|
|[SccGetParentProjectPath](../extensibility/sccgetparentprojectpath-function.md)|指定されたプロジェクトの親パスを返します (プロジェクトが存在している必要があります)。|
|[SccIsMultiCheckoutEnabled](../extensibility/sccismulticheckoutenabled-function.md)|ファイルに対して複数のチェックアウトが許可されているかどうかをチェックします。|
|[SccWillCreateSccFile](../extensibility/sccwillcreatesccfile-function.md)|プラグインが MSSCCPRJ を作成するかどうかを確認します。SCC ファイル。|

## <a name="functions-that-support-advanced-capability-version-13-of-the-source-control-plug-in-api"></a>高度な機能をサポートする機能 (ソース管理プラグイン API のバージョン 1.3)
 この関数グループは、ソース管理プラグイン API のバージョン 1.3 に含まれる追加機能を定義します。 これらの機能により、より高度なソース管理機能にアクセスできます。

|機能|説明|
|--------------|-----------------|
|[SccAddFilesFromSCC](../extensibility/sccaddfilesfromscc-function.md)|ソース管理から現在のプロジェクトにファイルの一覧を追加します。|
|[SccBackgroundGet](../extensibility/sccbackgroundget-function.md)|ユーザー インターフェイスを使用せずに、ソース管理からファイルの一覧を取得します。|
|[SccEnumChangedFiles](../extensibility/sccenumchangedfiles-function.md)|ソース管理内のローカル ファイルとは異なるファイルの一覧を取得します。|
|[SccGetExtendedCapabilities](../extensibility/sccgetextendedcapabilities-function.md)|ソース管理プラグインでサポートされる拡張機能を指定するフラグを取得します。|
|[SccGetUserOption](../extensibility/sccgetuseroption-function.md)|ユーザー固有のオプションを取得します。|
|[SccPopulateDirList](../extensibility/sccpopulatedirlist-function.md)|ソース管理下にあるプロジェクト内のディレクトリとファイルの一覧を調べます。 見つかった各ディレクトリとファイル名は、コールバック関数に渡されます。|
|[SccQueryChanges](../extensibility/sccquerychanges-function.md)|ファイルの一覧に対して行われた名前の変更を調べます。 各ファイル名は、変更ステータスを持つコールバック関数に渡されます。|

## <a name="requirements"></a>必要条件
 ヘッダー: scc.h

 (環境 SDK コモン フォルダーで提供される既定で *[ドライブ]* \プログラム ファイル\VSIP 8.0\EnvSDK\common\inc; MSSCCI サンプル [*ドライブ]* \プログラム ファイル\VSIP 8.0\MSSCCI と共に VSIP フォルダーにも提供されます。

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン](../extensibility/source-control-plug-ins.md)
- [ソース管理プラグインの作成](../extensibility/internals/creating-a-source-control-plug-in.md)
