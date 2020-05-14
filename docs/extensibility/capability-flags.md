---
title: 機能フラグ |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, capability flags
ms.assetid: a3f6071c-eac8-4bcd-8ffd-8d0a2d24a252
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9660cbe5a18e82974858fa4d923a38fc73e773f2
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739870"
---
# <a name="capability-flags"></a>機能フラグ
SCC_CAP_*xxx*フラグは、ソース管理プラグインの機能を示すために使用されるビット フラグです。 SCC_EXCAP_*xxx*フラグは、拡張された機能を示し、整数値に解決される増分フラグです。

|能力コード|[値]|説明|
|---------------------|-----------|-----------------|
|`SCC_CAP_REMOVE`|0x00000001L|[SccRemove](../extensibility/sccremove-function.md)およびコマンドをサポートします。|
|`SCC_CAP_RENAME`|0x00000002L|[SccRename](../extensibility/sccrename-function.md)とコマンドをサポートします。|
|`SCC_CAP_DIFF`|0x00000004L|[SccDiff](../extensibility/sccdiff-function.md)およびコマンドをサポートします。|
|`SCC_CAP_HISTORY`|0x00000008L|[SccHistory](../extensibility/scchistory-function.md)とコマンドをサポートします。|
|`SCC_CAP_PROPERTIES`|0x00000010L|[SccProperties](../extensibility/sccproperties-function.md)とコマンドをサポートします。|
|`SCC_CAP_RUNSCC`|0x0000020L|[SccRunScc](../extensibility/sccrunscc-function.md)とコマンドをサポートします。|
|`SCC_CAP_GETCOMMANDOPTIONS`|0x0000040L|コマンドをサポート[しています](../extensibility/sccgetcommandoptions-function.md)。|
|`SCC_CAP_QUERYINFO`|0x0000080L|[SccQueryInfo](../extensibility/sccqueryinfo-function.md)およびコマンドをサポートします。|
|`SCC_CAP_GETEVENTS`|0x00000100L|[SccGet イベント](../extensibility/sccgetevents-function.md)とコマンドをサポートします。|
|`SCC_CAP_GETPROJPATH`|0x00000200L|[SccGetProj パス](../extensibility/sccgetprojpath-function.md)とコマンドをサポートします。|
|`SCC_CAP_ADDFROMSCC`|0x00000400L|[SccAddFromScc](../extensibility/sccaddfromscc-function.md)とコマンドをサポートします。|
|`SCC_CAP_COMMENTCHECKOUT`|0x00000800L|チェックアウト時のコメントをサポートします。|
|`SCC_CAP_COMMENTCHECKIN`|0x00001000L|チェックイン時のコメントをサポートします。|
|`SCC_CAP_COMMENTADD`|0x00002000L|Add のコメントをサポートします。|
|`SCC_CAP_COMMENTREMOVE`|0x00004000L|削除のコメントをサポートします。|
|`SCC_CAP_TEXTOUT`|0x00008000L|IDE が提供する出力関数にテキストを書き込みます。|
|`SCC_CAP_ADD_STORELATEST`|0x00200000L|デルタのないファイルの保存をサポートします。|
|`SCC_CAP_HISTORY_MULTFILE`|0x00400000L|複数のファイル履歴をサポートします。|
|`SCC_CAP_IGNORECASE`|0x0080000L|大文字と小文字を区別しないファイル比較をサポートします。|
|`SCC_CAP_IGNORESPACE`|0x0100000L|空白を無視するファイル比較をサポートします。|
|`SCC_CAP_POPULATELIST`|0x02000000L|余分なファイルの検索をサポートします。|
|`SCC_CAP_COMMENTPROJECT`|0x0400000L|プロジェクトの作成に関するコメントをサポートします。|
|`SCC_CAP_DIFFALWAYS`|0x1000000L|制御下にある場合は、すべての状態で diff をサポートします。|
|`SCC_CAP_GET_NOUI`|0x2000000L|プラグインは Get の UI をサポートしていませんが、IDE は[SccGet](../extensibility/sccget-function.md)を呼び出す場合があります。|
|`SCC_CAP_REENTRANT`|0x4000000L|プラグインは再入可能でスレッドセーフです。 バージョン 1.0 では、再入可能でスレッド セーフであると想定されたプラグインはありません。 1.1 プラグインがこのビットを設定すると、ホストは複数のプロジェクトを並行して開くことが許可されます。|

## <a name="capability-bits-added-in-version-12"></a>バージョン 1.2 で追加された機能ビット

|能力コード|[値]|説明|
|---------------------|-----------|-----------------|
|`SCC_CAP_CREATESUBPROJECT`|0x00010000L|をサポート[しています](../extensibility/scccreatesubproject-function.md)。|
|`SCC_CAP_GETPARENTPROJECT`|0x00020000L|をサポート[しています。](../extensibility/sccgetparentprojectpath-function.md)|
|`SCC_CAP_BATCH`|0x00040000L|をサポート[しています。](../extensibility/sccbeginbatch-function.md) [SccEndBatch](../extensibility/sccendbatch-function.md)|
|`SCC_CAP_DIRECTORYSTATUS`|0x00080000L|[を](../extensibility/sccdirqueryinfo-function.md)サポートしています。|
|`SCC_CAP_DIRECTORYDIFF`|0x0010000L|[SccDirDiff](../extensibility/sccdirdiff-function.md)をサポートします。|
|`SCC_CAP_MULTICHECKOUT`|0x0800000L|1 つのファイルに対する複数のチェックアウトをサポートし[、SccIsMultiCheckoutEnabled](../extensibility/sccismulticheckoutenabled-function.md)をサポートします。|
|`SCC_CAP_SCCFILE`|0x8000000L|*MSSCCPRJ.SCC*ファイル (ユーザー/管理者のオーバーライドに従う) と[SccWillCreateSccFile](../extensibility/sccwillcreatesccfile-function.md)をサポートしています。|

## <a name="capability-bits-added-in-version-13"></a>バージョン 1.3 で追加された機能ビット
 これらのフラグは、機能がサポートされているかどうかを判断するために[、SccGetExtendedCapabilities](../extensibility/sccgetextendedcapabilities-function.md)関数に一度に 1 つずつ渡されます。

|拡張機能コード|[値]|説明|
|------------------------------|-----------|-----------------|
|`SCC_EXCAP_CHECKOUT_LOCALVER`|1|チェックアウトの`SCC_CHECKOUT_LOCALVER`オプションをサポートします。|
|`SCC_EXCAP_BACKGROUND_GET`|2|[を](../extensibility/sccbackgroundget-function.md)サポートしています。|
|`SCC_EXCAP_ENUM_CHANGED_FILES`|3|をサポート[しています。](../extensibility/sccenumchangedfiles-function.md)|
|`SCC_EXCAP_POPULATELIST_DIR`|4|余分なディレクトリの検索をサポートします。|
|`SCC_EXCAP_QUERYCHANGES`|5|ファイル変更の列挙をサポートします。|
|`SCC_EXCAP_ADD_FILES_FROM_SCC`|6|をサポートしています[。](../extensibility/sccaddfilesfromscc-function.md)|
|`SCC_EXCAP_GET_USER_OPTIONS`|7|をサポート[しています。](../extensibility/sccgetuseroption-function.md)|
|`SCC_EXCAP_THREADSAFE_QUERY_INFO`|8|複数のスレッドでの SccQueryInfo の呼び出しをサポートします。|
|`SCC_EXCAP_REMOVE_DIR`|9|関数をサポートします。|
|`SCC_EXCAP_DELETE_CHECKEDOUT`|10|チェックアウトされたファイルを削除できます。|
|`SCC_EXCAP_RENAME_CHECKEDOUT`|11|チェックアウトされたファイルの名前を変更できます。|

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン](../extensibility/source-control-plug-ins.md)
