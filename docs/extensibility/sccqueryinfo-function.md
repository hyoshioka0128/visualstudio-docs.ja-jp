---
title: 関数 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccQueryInfo
helpviewer_keywords:
- SccQueryInfo function
ms.assetid: 3973d336-a9b7-41a2-a4e6-bb8184a96aaf
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1efae18f15588f4dacf3409ea95e30af05397c6e
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80700473"
---
# <a name="sccqueryinfo-function"></a>SccQueryInfo 関数
この関数は、ソース管理下で選択されたファイルのセットの状態情報を取得します。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccQueryInfo(
   LPVOID  pvContext,
   LONG    nFiles,
   LPCSTR* lpFileNames,
   LPLONG  lpStatus
);
```

#### <a name="parameters"></a>パラメーター
 を行う

[in]ソース管理プラグインのコンテキスト構造。

 nファイル

[in]配列に指定されたファイルの`lpFileNames`数と配列の長さ`lpStatus`。

 ファイル名

[in]照会するファイルの名前の配列。

 lp2

[イン、アウト]ソース管理プラグインが各ファイルのステータス フラグを返す配列。 詳細については、「[ファイルステータスコード](../extensibility/file-status-code-enumerator.md)」を参照してください。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装は、次のいずれかの値を返します。

|[値]|説明|
|-----------|-----------------|
|SCC_OK|クエリは正常に実行されました。|
|SCC_E_ACCESSFAILURE|ソース管理システムへのアクセスに問題がありました。 再試行することをお勧めします。|
|SCC_E_PROJNOTOPEN|プロジェクトがソース管理下で開かれていない。|
|SCC_E_NONSPECIFICERROR|非特異的なエラー。|

## <a name="remarks"></a>Remarks
 空`lpFileName`の文字列の場合、現在更新する状態情報はありません。 それ以外の場合は、ステータス情報が変更された可能性があるファイルの完全パス名です。

 戻り値の配列はビットの`SCC_STATUS_xxxx`ビットマスクにすることができます。 詳細については、「[ファイルステータスコード](../extensibility/file-status-code-enumerator.md)」を参照してください。 ソース管理システムでは、すべてのビットの種類をサポートしていない場合があります。 たとえば、提供されていない`SCC_STATUS_OUTOFDATE`場合、ビットは設定されません。

 この機能を使用してファイルをチェックアウトする場合は、`MSSCCI`以下のステータス要件に注意してください。

- `SCC_STATUS_OUTBYUSER`は、現在のユーザーがファイルをチェックアウトしたときに設定されます。

- `SCC_STATUS_CHECKEDOUT`設定されていない限り`SCC_STATUS_OUTBYUSER`、設定できません。

- `SCC_STATUS_CHECKEDOUT`は、指定された作業ディレクトリにファイルがチェックアウトされている場合にのみ設定されます。

- 現在のユーザーが作業ディレクトリ以外のディレクトリにファイルをチェックアウトした場合は、設定されますが`SCC_STATUS_OUTBYUSER``SCC_STATUS_CHECKEDOUT`、チェックアウトされません。

## <a name="see-also"></a>関連項目
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [ファイルの状態コード](../extensibility/file-status-code-enumerator.md)
