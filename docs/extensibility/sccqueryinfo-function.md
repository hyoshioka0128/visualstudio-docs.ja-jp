---
description: この関数は、ソース管理下で選択された一連のファイルのステータス情報を取得します。
title: SccQueryInfo 関数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccQueryInfo
helpviewer_keywords:
- SccQueryInfo function
ms.assetid: 3973d336-a9b7-41a2-a4e6-bb8184a96aaf
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 911219605859025f1877d040b5932714b10f836a
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105073899"
---
# <a name="sccqueryinfo-function"></a>SccQueryInfo 関数
この関数は、ソース管理下で選択された一連のファイルのステータス情報を取得します。

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
 pvContext

からソース管理プラグインのコンテキスト構造。

 nFiles

から配列に指定されたファイルの数 `lpFileNames` と配列の長さ `lpStatus` 。

 lpFileNames 名

からクエリ対象のファイルの名前の配列。

 lpStatus

[入力、出力]ソース管理プラグインが各ファイルの状態フラグを返す配列。 詳細については、「 [ファイルのステータスコード](../extensibility/file-status-code-enumerator.md)」を参照してください。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装では、次の値のいずれかが返されることが想定されています。

|値|説明|
|-----------|-----------------|
|SCC_OK|クエリが成功しました。|
|SCC_E_ACCESSFAILURE|ネットワークまたは競合の問題が原因で、ソース管理システムへのアクセスに問題が発生しました。 再試行することをお勧めします。|
|SCC_E_PROJNOTOPEN|プロジェクトがソース管理下で開かれていません。|
|SCC_E_NONSPECIFICERROR|不特定のエラーです。|

## <a name="remarks"></a>注釈
 `lpFileName`が空の文字列の場合、現在更新する状態情報はありません。 それ以外の場合は、ステータス情報が変更された可能性があるファイルの完全なパス名です。

 戻り値の配列には、ビットのビットマスクを指定でき `SCC_STATUS_xxxx` ます。 詳細については、「 [ファイルのステータスコード](../extensibility/file-status-code-enumerator.md)」を参照してください。 ソース管理システムは、すべてのビット型をサポートしていない場合があります。 たとえば、が提供されていない場合、 `SCC_STATUS_OUTOFDATE` ビットは設定されません。

 この関数を使用してファイルをチェックアウトする場合は、次の状態の要件に注意して `MSSCCI` ください。

- `SCC_STATUS_OUTBYUSER` は、現在のユーザーがファイルをチェックアウトしたときに設定されます。

- `SCC_STATUS_CHECKEDOUT` を設定しない限り、を設定することはできません `SCC_STATUS_OUTBYUSER` 。

- `SCC_STATUS_CHECKEDOUT` は、指定された作業ディレクトリにファイルがチェックアウトされている場合にのみ設定されます。

- ファイルが現在のユーザーによって作業ディレクトリ以外のディレクトリにチェックアウトされている場合、は設定されますが、 `SCC_STATUS_OUTBYUSER` は設定され `SCC_STATUS_CHECKEDOUT` ません。

## <a name="see-also"></a>こちらもご覧ください
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [ファイルの状態コード](../extensibility/file-status-code-enumerator.md)
