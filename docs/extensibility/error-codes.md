---
title: エラー コード |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- error codes, source control plug-ins
- source control plug-ins, error codes
- errors [Visual Studio SDK]
ms.assetid: d9cbd1c4-719b-467a-8100-333c1e146d3b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 34072f6ddbd632f83dd308c6cb63427e02bb110b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80711837"
---
# <a name="error-codes"></a>エラー コード
ソース管理プラグイン API 関数がエラーを返す場合、次のエラー コードのいずれかであると予想されます。 すべてのエラーは負のエラー、警告または情報エラーコードは正のエラーコード、成功は 0 です。

|エラー コード|[値]|説明|
|----------------|-----------|-----------------|
|`SCC_I_SHARESUBPROJOK`|7|プラグインは、2 つの手順でソース管理からファイルを追加できます。 詳細については、「 [SccSetOption](../extensibility/sccsetoption-function.md)」を参照してください。|
|`SCC_I_FILEDIFFERS`|6|ローカル ファイルは、ソース管理データベース内のファイルとは異なります (たとえば[、SccDiff](../extensibility/sccdiff-function.md)がこの値を返す場合があります)。|
|`SCC_I_RELOADFILE`|5|ローカル ファイルはソース管理操作中に変更されました。可能な場合は、ファイルを再ロードする必要があります。|
|`SCC_I_FILENOTAFFECTED`|4|ファイルは影響を受けません。|
|`SCC_I_PROJECTCREATED`|3|プロジェクトは、ソース管理操作中に作成されました (たとえば、フラグが指定されている場合は[SccOpenProject](../extensibility/sccopenproject-function.md)の呼び出し中`SCC_OP_CREATEIFNEW`)。|
|`SCC_I_OPERATIONCANCELED`|2|操作が取り消されました。|
|`SCC_I_ADV_SUPPORT`|1|プラグインは、指定されたコマンドの詳細オプションをサポートします。 詳細については、「コマンド[オプション](../extensibility/sccgetcommandoptions-function.md)」を参照してください。|
|`SCC_OK`|0|正常終了しました。|
|`SCC_E_INITIALIZEFAILED`|-1|エラー: 初期化に失敗しました。|
|`SCC_E_UNKNOWNPROJECT`|-2|エラー: プロジェクトが不明です。|
|`SCC_E_COULDNOTCREATEPROJECT`|-3|エラー: プロジェクトを作成できませんでした。|
|`SCC_E_NOTCHECKEDOUT`|-4|エラー: ファイルはチェックアウトされていません。|
|`SCC_E_ALREADYCHECKEDOUT`|-5|エラー: ファイルは既にチェックアウトされています。|
|`SCC_E_FILEISLOCKED`|-6|エラー: ファイルがロックされています。|
|`SCC_E_FILEOUTEXCLUSIVE`|-7|エラー: ファイルは排他的にチェックアウトされています。|
|`SCC_E_ACCESSFAILURE`|-8|ソース管理システムへのアクセスに問題が発生しました。 再試行することをお勧めします。|
|`SCC_E_CHECKINCONFLICT`|-9|エラー: チェックイン中に競合が発生しました。|
|`SCC_E_FILEALREADYEXISTS`|-10|エラー: ファイルは既に存在します。|
|`SCC_E_FILENOTCONTROLLED`|-11|エラー: ファイルがソース管理下にありません。|
|`SCC_E_FILEISCHECKEDOUT`|-12|エラー: ファイルがチェックアウトされています。|
|`SCC_E_NOSPECIFIEDVERSION`|-13|エラー: 指定されたバージョンがありません。|
|`SCC_E_OPNOTSUPPORTED`|-14|エラー: 操作はサポートされていません。|
|`SCC_E_NONSPECIFICERROR`|-15|非特定エラー。|
|`SCC_E_OPNOTPERFORMED`|-16|エラーが発生しました。|
|`SCC_E_TYPENOTSUPPORTED`|-17|エラー: ファイルの種類 (バイナリなど) は、ソース コード管理システムではサポートされていません。|
|`SCC_E_VERIFYMERGE`|-18|ファイルは自動マージされましたが、ユーザー検証の保留中のため、チェックされていません。|
|`SCC_E_FIXMERGE`|-19|ファイルは自動マージされましたが、手動で解決する必要があるマージの競合のためチェックインされていません。|
|`SCC_E_SHELLFAILURE`|-20|シェル障害のためエラーです。|
|`SCC_E_INVALIDUSER`|-21|エラー: ユーザーが無効です。|
|`SCC_E_PROJECTALREADYOPEN`|-22|エラー: プロジェクトは既に開いています。|
|`SCC_E_PROJSYNTAXERR`|-23|プロジェクト構文エラーです。|
|`SCC_E_INVALIDFILEPATH`|-24|エラー: ファイル パスが無効です。|
|`SCC_E_PROJNOTOPEN`|-25|エラー: プロジェクトが開かれていない。|
|`SCC_E_NOTAUTHORIZED`|-26|エラー: ユーザーがこの操作を実行する権限がありません。|
|`SCC_E_FILESYNTAXERR`|-27|ファイル構文エラーです。|
|`SCC_E_FILENOTEXIST`|-28|エラーが発生しました。|
|`SCC_E_CONNECTIONFAILURE`|-29|エラー: 接続エラーが発生しました。|
|`SCC_E_UNKNOWNERROR`|-30|不明なエラー。|
|`SCC_E_BACKGROUNDGETINPROGRESS`|-31|バックグラウンド取得操作は現在実行中です。|

## <a name="macros-provided-for-quick-checking"></a>クイックチェック用に提供されるマクロ

```cpp
IS_SCC_ERROR(rtn) (((rtn) < 0) ? TRUE : FALSE)
IS_SCC_SUCCESS(rtn) (((rtn) == SCC_OK) ? TRUE : FALSE)
IS_SCC_WARNING(rtn) (((rtn) > 0) ? TRUE : FALSE)
```

## <a name="remarks"></a>Remarks
 すべてのソース管理プラグイン API 関数[(SccAdd、SccCheckin](../extensibility/sccadd-function.md)、および[SccDiff](../extensibility/scccheckin-function.md)を除く) は、引数として渡されるローカル ファイルが作業フォルダーに存在しない場合に成功することが期待されます。 [SccDiff](../extensibility/sccdiff-function.md) たとえば、IDE は、作業フォルダーに存在しないがソース管理システムに存在するファイルに対して[、SccCheckout](../extensibility/scccheckout-function.md)または[SccUncheckout](../extensibility/sccuncheckout-function.md)に対して呼び出しを発行する場合があります。 この呼び出しは成功します。 作業フォルダーまたはソース管理システムにファイルがない場合にのみ、関数が失敗すると予想されます。

 および`SccAdd``SccCheckin`などの特定の関数は、作業フォルダー`SCC_E_FILENOTEXIST`内のファイルが存在しない場合に、具体的に返す必要があります。 ソース管理システム内の有効なファイル名を操作する場合、作業ファイルが存在しない場合は、他の関数が正常に動作すると予想されます。

 ソース管理プラグインは、ある操作中にファイルが読み取り専用に設定されていたとしても、作業フォルダー内のファイルに対する特権に関する想定を行いません。 作業フォルダー内のファイルは、プラグインのコントロールの外部で移動、削除、および変更できます。

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン](../extensibility/source-control-plug-ins.md)
