---
title: 機能フラグ |Microsoft Docs
description: ソース管理プラグインの機能を示す SCC_CAP_xxx フラグと、拡張機能を示す SCC_EXCAP_xxx フラグについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, capability flags
ms.assetid: a3f6071c-eac8-4bcd-8ffd-8d0a2d24a252
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 12acefb99de787d55bc0f932757dde5ea928c6cb
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105094927"
---
# <a name="capability-flags"></a>機能フラグ
SCC_CAP_ *xxx* フラグは、ソース管理プラグインの機能を示すために使用されるビットフラグです。 SCC_EXCAP_ *xxx* フラグは、拡張機能を示し、整数値に解決される増分フラグです。

|機能コード|値|説明|
|---------------------|-----------|-----------------|
|`SCC_CAP_REMOVE`|0x00000001L|[Sccremove](../extensibility/sccremove-function.md)とコマンドをサポートします。|
|`SCC_CAP_RENAME`|0x00000002L|では、 [Sccrename](../extensibility/sccrename-function.md) とコマンドがサポートされています。|
|`SCC_CAP_DIFF`|0x00000004L|[Sccdiff](../extensibility/sccdiff-function.md)とコマンドをサポートします。|
|`SCC_CAP_HISTORY`|0x00000008L|では、 [SccHistory](../extensibility/scchistory-function.md) とコマンドがサポートされています。|
|`SCC_CAP_PROPERTIES`|0x00000010L|[Sccproperties](../extensibility/sccproperties-function.md)とコマンドをサポートします。|
|`SCC_CAP_RUNSCC`|0x00000020L|では、 [SccRunScc](../extensibility/sccrunscc-function.md) とコマンドがサポートされています。|
|`SCC_CAP_GETCOMMANDOPTIONS`|0x00000040L|では、 [SccGetCommandOptions](../extensibility/sccgetcommandoptions-function.md) とコマンドがサポートされています。|
|`SCC_CAP_QUERYINFO`|0x00000080L|では、 [Sccqueryinfo](../extensibility/sccqueryinfo-function.md) とコマンドがサポートされています。|
|`SCC_CAP_GETEVENTS`|0x00000100L|では、 [SccGetEvents](../extensibility/sccgetevents-function.md) とコマンドがサポートされています。|
|`SCC_CAP_GETPROJPATH`|0x00000200L|では、 [Sccgetprojpath](../extensibility/sccgetprojpath-function.md) とコマンドがサポートされています。|
|`SCC_CAP_ADDFROMSCC`|0x00000400L|[Sccaddfromscc](../extensibility/sccaddfromscc-function.md)とコマンドをサポートします。|
|`SCC_CAP_COMMENTCHECKOUT`|0x00000800L|チェックアウト時のコメントをサポートします。|
|`SCC_CAP_COMMENTCHECKIN`|0x00001000L|チェックインのコメントをサポートします。|
|`SCC_CAP_COMMENTADD`|0X00002000 l|追加のコメントをサポートしています。|
|`SCC_CAP_COMMENTREMOVE`|0x00004000L|削除時のコメントをサポートします。|
|`SCC_CAP_TEXTOUT`|0x00008000L|IDE によって提供される出力関数にテキストを書き込みます。|
|`SCC_CAP_ADD_STORELATEST`|0x00200000L|は、デルタなしのファイルの格納をサポートしています。|
|`SCC_CAP_HISTORY_MULTFILE`|0x00400000L|では、複数のファイル履歴がサポートされています。|
|`SCC_CAP_IGNORECASE`|0x00800000L|大文字と小文字を区別しないファイル比較をサポートします。|
|`SCC_CAP_IGNORESPACE`|0x01000000L|では、空白文字を無視するファイル比較がサポートされています。|
|`SCC_CAP_POPULATELIST`|0x02000000L|余分なファイルの検索をサポートします。|
|`SCC_CAP_COMMENTPROJECT`|0x04000000L|プロジェクトの作成に関するコメントをサポートします。|
|`SCC_CAP_DIFFALWAYS`|0x10000000L|コントロールの場合は、すべての状態で diff をサポートします。|
|`SCC_CAP_GET_NOUI`|0x20000000L|プラグインは Get 用の UI をサポートしていませんが、IDE が [Sccget](../extensibility/sccget-function.md)を呼び出す可能性があります。|
|`SCC_CAP_REENTRANT`|0x40000000L|プラグインは再入可能で、スレッドセーフです。 バージョン1.0 では、再入可能で、スレッドセーフであると想定されていたプラグインはありません。 1.1 プラグインでこのビットが設定されている場合、ホストは複数のプロジェクトを並行して開くことができます。|

## <a name="capability-bits-added-in-version-12"></a>バージョン1.2 で追加された機能ビット

|機能コード|値|説明|
|---------------------|-----------|-----------------|
|`SCC_CAP_CREATESUBPROJECT`|0x00010000L|[SccCreateSubProject](../extensibility/scccreatesubproject-function.md)をサポートします。|
|`SCC_CAP_GETPARENTPROJECT`|0x00020000L|[SccGetParentProjectPath](../extensibility/sccgetparentprojectpath-function.md)をサポートします。|
|`SCC_CAP_BATCH`|0x00040000L|では、 [Sccbeginbatch](../extensibility/sccbeginbatch-function.md) と [sccbeginbatch](../extensibility/sccendbatch-function.md)がサポートされています。|
|`SCC_CAP_DIRECTORYSTATUS`|0x00080000L|[Sccdirqueryinfo](../extensibility/sccdirqueryinfo-function.md)をサポートします。|
|`SCC_CAP_DIRECTORYDIFF`|0x00100000L|[Sccdirdiff](../extensibility/sccdirdiff-function.md)をサポートします。|
|`SCC_CAP_MULTICHECKOUT`|0x08000000L|では、ファイルと [SccIsMultiCheckoutEnabled](../extensibility/sccismulticheckoutenabled-function.md)で複数のチェックアウトをサポートしています。|
|`SCC_CAP_SCCFILE`|0x80000000L|では、 *mssccprj.scc* ファイル (ユーザー/管理者の上書きによる) と [Scc ccfile](../extensibility/sccwillcreatesccfile-function.md)がサポートされています。|

## <a name="capability-bits-added-in-version-13"></a>バージョン1.3 で追加された機能ビット
 これらのフラグは、機能がサポートされているかどうかを判断するために、 [Sccgetextendedcapabilities](../extensibility/sccgetextendedcapabilities-function.md) 関数に一度に1つずつ渡されます。

|拡張機能コード|値|説明|
|------------------------------|-----------|-----------------|
|`SCC_EXCAP_CHECKOUT_LOCALVER`|1|では、チェックアウトのオプションがサポートされてい `SCC_CHECKOUT_LOCALVER` ます。|
|`SCC_EXCAP_BACKGROUND_GET`|2|[Sccbackgroundget](../extensibility/sccbackgroundget-function.md)をサポートします。|
|`SCC_EXCAP_ENUM_CHANGED_FILES`|3|[Sccenumの](../extensibility/sccenumchangedfiles-function.md)すべてのファイルをサポートします。|
|`SCC_EXCAP_POPULATELIST_DIR`|4|余分なディレクトリの検索をサポートします。|
|`SCC_EXCAP_QUERYCHANGES`|5|ファイルの変更の列挙をサポートします。|
|`SCC_EXCAP_ADD_FILES_FROM_SCC`|6|[Sccaddfilesfromscc](../extensibility/sccaddfilesfromscc-function.md)をサポートします。|
|`SCC_EXCAP_GET_USER_OPTIONS`|7|[Sccgetuseroption](../extensibility/sccgetuseroption-function.md)をサポートします。|
|`SCC_EXCAP_THREADSAFE_QUERY_INFO`|8|では、複数のスレッドで SccQueryInfo を呼び出すことができます。|
|`SCC_EXCAP_REMOVE_DIR`|9|では、SccRemoveDir 関数がサポートされています。|
|`SCC_EXCAP_DELETE_CHECKEDOUT`|10|チェックアウトされたファイルを削除できます。|
|`SCC_EXCAP_RENAME_CHECKEDOUT`|11|チェックアウトされたファイルの名前を変更できます。|

## <a name="see-also"></a>こちらもご覧ください
- [ソース管理プラグイン](../extensibility/source-control-plug-ins.md)
