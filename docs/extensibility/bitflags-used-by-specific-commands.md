---
title: 特定のコマンドで使用されるビットフラグ |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, bitflags used by specific commands
ms.assetid: 37969977-6f7d-45c9-ba03-1306ae71f5d1
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ffa1fd8bf025d665977e87dc8b88da724ade5a8b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80740009"
---
# <a name="bitflags-used-by-specific-commands"></a>特定のコマンドで使用されるビットフラグ
ソース管理プラグイン API の複数の関数の動作は、1 つの値に 1 つ以上のビットを設定することで変更できます。 これらの値はビットフラグと呼ばれます。 ソース管理プラグイン API で使用されるさまざまなビットフラグは、それらを使用する関数ごとにグループ化された、ここでは詳しく説明されています。

## <a name="checked-out-flag"></a>チェックアウトフラグ
 このフラグは、 [SccAdd](../extensibility/sccadd-function.md)または[SccCheckin](../extensibility/scccheckin-function.md)のどちらかに設定できます。

|フラグ|[値]|説明|
|----------|-----------|-----------------|
|`SCC_KEEP_CHECKEDOUT`|0x1000|ファイルをチェックアウトしたままにします。|

## <a name="add-flags"></a>フラグを追加する
 これらのフラグは[SccAdd](../extensibility/sccadd-function.md)によって使用されます。

|フラグ|[値]|説明|
|----------|-----------|-----------------|
|`SCC_FILETYPE_AUTO`|0x00|ソース管理プラグインは、ファイルがテキストかバイナリかを自動的に検出する必要があります。|
|`SCC_FILETYPE_TEXT`|0x01|ファイルの種類はテキストです。|
|`SCC_FILETYPE_BINARY`|0x04|ファイルの種類はバイナリです。 **注:** `SCC_FILETYPE_TEXT` `SCC_FILETYPE_BINARY`フラグとフラグは相互に排他的です。   正確に 1 つまたは両方を設定します。|
|`SCC_ADD_STORELATEST`|0x02|最新バージョンのみを保存します (デルタなし)。|

## <a name="diff-flags"></a>相違フラグ
 [SccDiff](../extensibility/sccdiff-function.md)は、これらのフラグを使用して、diff 操作のスコープを定義します。 フラグ`SCC_DIFF_QD_xxx`は相互に排他的です。 それらのいずれかが指定されている場合、視覚的なフィードバックは与えなくなります。 「クイック・ディフ」(QD) では、プラグインはファイルの違いは判別されず、異なる場合に限られます。 これらのフラグが指定されていない場合は、"ビジュアル diff" が実行されます。詳細なファイルの差分が計算され、表示されます。 要求された QD がサポートされていない場合、プラグインは次に最適なバージョンに移動します。 たとえば、IDE がチェックサムを要求し、プラグインがチェックサムをサポートしていない場合、プラグインは完全なコンテンツチェックを実行します(ビジュアル表示よりもはるかに高速です)。

|フラグ|[値]|説明|
|----------|-----------|-----------------|
|`SCC_DIFF_IGNORECASE`|0x0002|大文字と小文字の違いを無視します。|
|`SCC_DIFF_IGNORESPACE`|0x0004|空白の違いを無視します。 **注:** `SCC_DIFF_IGNORECASE`フラグと`SCC_DIFF_IGNORESPACE`フラグはオプションのビットフラグです。|
|`SCC_DIFF_QD_CONTENTS`|0x0010|ファイルの内容全体を比較してQDを行います。|
|`SCC_DIFF_QD_CHECKSUM`|0x0020|チェックサムによるQD。|
|`SCC_DIFF_QD_TIME`|0x0040|QD (ファイルの日付/時刻スタンプ別)。|
|`SCC_DIFF_QUICK_DIFF`|0x0070|これは、すべての QD ビットフラグをチェックするために使用されるマスクです。 関数に渡す必要はありません。3 つの QD ビットフラグは相互に排他的です。 QD は常に UI を表示しないということを意味します。|

## <a name="populatelist-flag"></a>リストフラグを設定する
 このフラグは、パラメーター内の[SccPopulateList](../extensibility/sccpopulatelist-function.md)によって使用されます`fOptions`。

|フラグ|[値]|説明|
|----------|-----------|-----------------|
|`SCC_PL_DIR`|0x00000001L|IDE はファイルではなくディレクトリを渡しています。|

## <a name="populatedirlist-flags"></a>フラグを設定する
 これらのフラグは、`fOptions`パラメーター内の[SccPopulateDirList](../extensibility/sccpopulatedirlist-function.md)によって使用されます。

|オプション値|[値]|説明|
|------------------|-----------|-----------------|
|SCC_PDL_ONELEVEL|0x0000|ディレクトリのレベルを 1 つだけ調べます (これがデフォルトです)。|
|SCC_PDL_RECURSIVE|0x0001|指定した各ディレクトリの下にあるすべてのディレクトリを再帰的に調べます。|
|SCC_PDL_INCLUDEFILES|0x0002|検査プロセスにファイル名を含めます。|

## <a name="openproject-flags"></a>プロジェクトフラグを開く
 これらのフラグは、`dwFlags`パラメーター内の[SccOpenProject](../extensibility/sccopenproject-function.md)によって使用されます。

|オプション値|[値]|説明|
|------------------|-----------|-----------------|
|SCC_OP_CREATEIFNEW|0x00000001L|プロジェクトがソース管理に存在しない場合は、作成します。 このフラグが設定されていない場合は、プロジェクトの作成を求めるプロンプト`SCC_OP_SILENTOPEN`をユーザーに表示します (フラグが指定されていない場合)。|
|SCC_OP_SILENTOPEN|0x00000002L|プロジェクトの作成をユーザーに求めるプロンプトを表示しない。ちょうど戻`SCC_E_UNKNOWNPROJECT`る.|

## <a name="get-flags"></a>フラグを取得する
 これらのフラグは、 [SccGet](../extensibility/sccget-function.md)および[SccCheckout](../extensibility/scccheckout-function.md)で使用されます。

|フラグ|[値]|説明|
|----------|-----------|-----------------|
|`SCC_GET_ALL`|0x00000001L|IDE はファイルではなくディレクトリを渡しています: これらのディレクトリ内のすべてのファイルを取得します。|
|`SCC_GET_RECURSIVE`|0x00000002L|IDE はディレクトリを渡しています: これらのディレクトリとそのサブディレクトリをすべて取得します。|

## <a name="noption-values"></a>nオプション値
 これらのフラグは、パラメーターの[SccSetOption](../extensibility/sccsetoption-function.md) `nOption`によって使用されます。

|フラグ|[値]|説明|
|----------|-----------|-----------------|
|`SCC_OPT_EVENTQUEUE`|0x00000001L|イベント キューの状態を設定します。|
|`SCC_OPT_USERDATA`|0x00000002L|のユーザー データ`SCC_OPT_NAMECHANGEPFN`を指定します。|
|`SCC_OPT_HASCANCELMODE`|0x0000003L|IDE はキャンセルを処理できます。|
|`SCC_OPT_NAMECHANGEPFN`|0x00000004L|名前の変更に対するコールバックを設定します。|
|`SCC_OPT_SCCCHECKOUTONLY`|0x0000005L|ソース管理プラグイン UI チェックアウトを無効にし、作業ディレクトリを設定しません。|
|`SCC_OPT_SHARESUBPROJ`|0x0000006L|ソース管理システムから追加して、作業ディレクトリを指定します。 直接の子孫である場合は、関連付けられたプロジェクトに共有してみてください。|

## <a name="dwval-bitflags"></a>dwVal ビットフラグ
 これらのフラグは、パラメーターの[SccSetOption](../extensibility/sccsetoption-function.md) `dwVal`によって使用されます。

|フラグ|[値]|説明|値で`nOption`使用|
|----------|-----------|-----------------|-----------------------------|
|`SCC_OPT_EQ_DISABLE`|0x00L|イベント キューのアクティビティを中断します。|`SCC_OPT_EVENTQUEUE`|
|`SCC_OPT_EQ_ENABLE`|0x01L|イベント キューのログ記録を有効にします。|`SCC_OPT_EVENTQUEUE`|
|`SCC_OPT_HCM_NO`|0L|(デフォルト)キャンセル モードはありません。必要に応じてプラグインを指定する必要があります。|`SCC_OPT_HASCANCELMODE`|
|`SCC_OPT_HCM_YES`|1L|IDE はキャンセルを処理します。|`SCC_OPT_HASCANCELMODE`|
|`SCC_OPT_SCO_NO`|0L|(デフォルト)プラグインUIからチェックアウトOK。作業ディレクトリが設定されます。|`SCC_OPT_SCCCHECKOUTONLY`|
|`SCC_OPT_SCO_YES`|1L|プラグイン UI チェックアウト、作業ディレクトリなし。|`SCC_OPT_SCCCHECKOUTONLY`|

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン](../extensibility/source-control-plug-ins.md)
