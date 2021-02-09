---
title: 特定のコマンドで使用されるビットフラグ |Microsoft Docs
description: ソース管理プラグイン API で使用される bitflags について説明します。これは、それらを使用する関数によって整理されています。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, bitflags used by specific commands
ms.assetid: 37969977-6f7d-45c9-ba03-1306ae71f5d1
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 6e018631e24cf7e678072b6b54183fd3c619dc4a
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99890332"
---
# <a name="bitflags-used-by-specific-commands"></a>特定のコマンドで使用されるビットフラグ
ソース管理プラグイン API の多くの関数の動作は、1つの値に1つ以上のビットを設定することによって変更できます。 これらの値は bitflags と呼ばれます。 ソース管理プラグイン API で使用されるさまざまな bitflags の詳細については、こちらを使用する関数によってグループ化されています。

## <a name="checked-out-flag"></a>チェックアウトフラグ
 このフラグは、 [Sccadd](../extensibility/sccadd-function.md) または [sccadd](../extensibility/scccheckin-function.md)に対して設定できます。

|フラグ|値|説明|
|----------|-----------|-----------------|
|`SCC_KEEP_CHECKEDOUT`|0x1000|ファイルをチェックアウトしたままにします。|

## <a name="add-flags"></a>フラグの追加
 これらのフラグは [Sccadd](../extensibility/sccadd-function.md)によって使用されます。

|フラグ|値|説明|
|----------|-----------|-----------------|
|`SCC_FILETYPE_AUTO`|0x00|ソース管理プラグインは、ファイルがテキストかバイナリかを自動的に検出します。|
|`SCC_FILETYPE_TEXT`|0x01|ファイルの種類はテキストです。|
|`SCC_FILETYPE_BINARY`|0x04|ファイルの種類は binary です。 **注:** `SCC_FILETYPE_TEXT``SCC_FILETYPE_BINARY`フラグとフラグは相互に排他的です。   1つだけを設定するか、どちらも設定しません。|
|`SCC_ADD_STORELATEST`|0x02|最新バージョンのみを格納します (デルタなし)。|

## <a name="diff-flags"></a>Diff フラグ
 [Sccdiff](../extensibility/sccdiff-function.md)は、これらのフラグを使用して、diff 操作のスコープを定義します。 `SCC_DIFF_QD_xxx`フラグは相互に排他的です。 これらのいずれかが指定されている場合、視覚的なフィードバックは与えられません。 "クイック diff" (QD) では、ファイルが異なる場合にのみ、プラグインによってファイルがどのように異なるかは判断されません。 これらのフラグが指定されていない場合は、"ビジュアル diff" が実行されます。ファイルの相違点の詳細が計算されて表示されます。 要求された QD がサポートされていない場合、プラグインは次に最適なものに移動します。 たとえば、IDE がチェックサムを要求し、プラグインがそれをサポートしていない場合、プラグインはフルコンテンツチェックを行います (ビジュアル表示よりもはるかに高速)。

|フラグ|値|説明|
|----------|-----------|-----------------|
|`SCC_DIFF_IGNORECASE`|0x0002|大文字と小文字の違いを無視します。|
|`SCC_DIFF_IGNORESPACE`|0x0004|空白文字の違いを無視します。 **注:** `SCC_DIFF_IGNORECASE` フラグと `SCC_DIFF_IGNORESPACE` フラグは、省略可能なビットフラグです。|
|`SCC_DIFF_QD_CONTENTS`|0x0010|ファイルの内容全体を比較することによる QD。|
|`SCC_DIFF_QD_CHECKSUM`|0x0020|チェックサムによる QD。|
|`SCC_DIFF_QD_TIME`|0x0040|ファイルの日付/時刻スタンプによる QD。|
|`SCC_DIFF_QUICK_DIFF`|0x0070|このマスクは、QD ビットフラグをすべて確認するために使用されます。 関数に渡すことはできません。3つの QD ビットフラグは相互に排他的です。 QD は常に UI を表示しないことを意味します。|

## <a name="populatelist-flag"></a>PopulateList フラグ
 このフラグは、パラメーターの [SccPopulateList](../extensibility/sccpopulatelist-function.md) によって使用され `fOptions` ます。

|フラグ|値|説明|
|----------|-----------|-----------------|
|`SCC_PL_DIR`|0x00000001L|IDE は、ファイルではなくディレクトリを渡しています。|

## <a name="populatedirlist-flags"></a>PopulateDirList フラグ
 これらのフラグは、パラメーターの [SccPopulateDirList](../extensibility/sccpopulatedirlist-function.md) によって使用され `fOptions` ます。

|オプション値|値|説明|
|------------------|-----------|-----------------|
|SCC_PDL_ONELEVEL|0x0000|ディレクトリのディレクトリの1レベルだけを調べます (これは既定値です)。|
|SCC_PDL_RECURSIVE|0x0001|指定された各ディレクトリの下のすべてのディレクトリを再帰的に検査します。|
|SCC_PDL_INCLUDEFILES|0x0002|検査プロセスにファイル名を含めます。|

## <a name="openproject-flags"></a>OpenProject フラグ
 これらのフラグは、パラメーターの [Sccopenproject](../extensibility/sccopenproject-function.md) によって使用され `dwFlags` ます。

|オプション値|値|説明|
|------------------|-----------|-----------------|
|SCC_OP_CREATEIFNEW|0x00000001L|プロジェクトがソース管理に存在しない場合は、プロジェクトを作成します。 このフラグが設定されていない場合は、ユーザーにプロジェクトの作成を求めるプロンプトを表示 `SCC_OP_SILENTOPEN` します (フラグが指定されていない場合)。|
|SCC_OP_SILENTOPEN|0x00000002L|プロジェクトを作成するようにユーザーに要求しないでください。だけ `SCC_E_UNKNOWNPROJECT` を返します。|

## <a name="get-flags"></a>フラグを取得する
 これらのフラグは、 [Sccget](../extensibility/sccget-function.md) と [sccget](../extensibility/scccheckout-function.md)によって使用されます。

|フラグ|値|説明|
|----------|-----------|-----------------|
|`SCC_GET_ALL`|0x00000001L|IDE は、ファイルではなくディレクトリを渡しています。これらのディレクトリ内のすべてのファイルを取得します。|
|`SCC_GET_RECURSIVE`|0x00000002L|IDE はディレクトリを渡しています。これらのディレクトリとそのすべてのサブディレクトリを取得します。|

## <a name="noption-values"></a>値を指定しない
 これらのフラグは、パラメーターの [Sccsetoption](../extensibility/sccsetoption-function.md) によって使用され `nOption` ます。

|フラグ|値|説明|
|----------|-----------|-----------------|
|`SCC_OPT_EVENTQUEUE`|0x00000001L|イベントキューの状態を設定します。|
|`SCC_OPT_USERDATA`|0x00000002L|のユーザーデータを指定 `SCC_OPT_NAMECHANGEPFN` します。|
|`SCC_OPT_HASCANCELMODE`|0x00000003L|IDE はキャンセルを処理できます。|
|`SCC_OPT_NAMECHANGEPFN`|0x00000004L|名前を変更するためのコールバックを設定します。|
|`SCC_OPT_SCCCHECKOUTONLY`|0x00000005L|ソース管理プラグインの UI チェックアウトを無効にし、作業ディレクトリを設定しません。|
|`SCC_OPT_SHARESUBPROJ`|0x00000006L|作業ディレクトリを指定するには、ソース管理システムからを追加します。 直接の子孫である場合は、関連付けられているプロジェクトへの共有を試みます。|

## <a name="dwval-bitflags"></a>dwVal ビットフラグ
 これらのフラグは、パラメーターの [Sccsetoption](../extensibility/sccsetoption-function.md) によって使用され `dwVal` ます。

|フラグ|値|説明|値で使用 `nOption`|
|----------|-----------|-----------------|-----------------------------|
|`SCC_OPT_EQ_DISABLE`|0x00L|イベントキューのアクティビティを中断します。|`SCC_OPT_EVENTQUEUE`|
|`SCC_OPT_EQ_ENABLE`|0x01L|イベントキューのログ記録を有効にします。|`SCC_OPT_EVENTQUEUE`|
|`SCC_OPT_HCM_NO`|0L|標準キャンセルモードはありません。必要に応じてプラグインを指定する必要があります。|`SCC_OPT_HASCANCELMODE`|
|`SCC_OPT_HCM_YES`|1L|IDE がキャンセルを処理します。|`SCC_OPT_HASCANCELMODE`|
|`SCC_OPT_SCO_NO`|0L|標準プラグインの UI からチェックアウトしてください。作業ディレクトリが設定されています。|`SCC_OPT_SCCCHECKOUTONLY`|
|`SCC_OPT_SCO_YES`|1L|プラグインの UI チェックアウトがありません。作業ディレクトリがありません。|`SCC_OPT_SCCCHECKOUTONLY`|

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン](../extensibility/source-control-plug-ins.md)
