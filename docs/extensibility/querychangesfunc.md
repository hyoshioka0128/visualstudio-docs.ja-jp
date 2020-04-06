---
title: クエリチェンジFUNC |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- QUERYCHANGESFUNC
helpviewer_keywords:
- QUERYCHANGESFUNC callback function
- QUERYCHANGESDATA structure
ms.assetid: 9d383e2c-eee1-4996-973a-0652d4c5951c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 30864cae95672f4026084a94c5474d165b124cba
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80701634"
---
# <a name="querychangesfunc"></a>QUERYCHANGESFUNC
これは、ファイル名のコレクションを列挙し、各ファイルの状態を決定するために[SccQueryChanges](../extensibility/sccquerychanges-function.md)操作によって使用されるコールバック関数です。

 この`SccQueryChanges`関数には、ファイルのリストとコールバックへのポインタが`QUERYCHANGESFUNC`与えられます。 ソース管理プラグインは、指定されたリストを列挙し、一覧内の各ファイルの状態を (このコールバックを介して) 提供します。

## <a name="signature"></a>署名

```cpp
typedef BOOL (*QUERYCHANGESFUNC)(
   LPVOID pvCallerData,
   QUERYCHANGESDATA * pChangesData
);
```

## <a name="parameters"></a>パラメーター
 呼び出し元データ

[in]呼`pvCallerData`び出し元 (IDE) から[SccQueryChanges](../extensibility/sccquerychanges-function.md)に渡されるパラメータ。 ソース管理プラグインは、この値の内容について想定しないでください。

 データを変更します。

[in]ファイルへの変更を記述する[QUERYCHANGESDATA 構造体](#LinkQUERYCHANGESDATA)構造体へのポインター。

## <a name="return-value"></a>戻り値
 IDE は、適切なエラー コードを返します。

|[値]|説明|
|-----------|-----------------|
|SCC_OK|処理し続けます。|
|SCC_I_OPERATIONCANCELED|処理を停止します。|
|SCC_E_xxx|適切な SCC エラーは処理を停止する必要があります。|

## <a name="querychangesdata-structure"></a><a name="LinkQUERYCHANGESDATA"></a>クエリの変更データ構造
 各ファイルに渡される構造体は、次のようになります。

```cpp
struct QUERYCHANGESDATA_A
{
    DWORD  dwSize;
    LPCSTR lpFileName;
    DWORD  dwChangeType;
    LPCSTR lpLatestName;
};

typedef struct QUERYCHANGESDATA_A QUERYCHANGESDATA;

struct QUERYCHANGESDATA_W
{
    DWORD   dwSize;
    LPCWSTR lpFileName;
    DWORD   dwChangeType;
    LPCWSTR lpLatestName;
};
```

 dwSize この構造体のサイズ (バイト単位)。

 この項目の元のファイル名。

 dwChangeType ファイルの状態を示すコード:

|コード|説明|
|----------|-----------------|
|`SCC_CHANGE_UNKNOWN`|何が変わったのか分からず|
|`SCC_CHANGE_UNCHANGED`|このファイルの名前は変更されません。|
|`SCC_CHANGE_DIFFERENT`|異なる ID を持つファイルが、データベースに同じ名前が存在します。|
|`SCC_CHANGE_NONEXISTENT`|ファイルはデータベースまたはローカルに存在しません。|
|`SCC_CHANGE_DATABASE_DELETED`|データベース内のファイルが削除されました。|
|`SCC_CHANGE_LOCAL_DELETED`|ファイルはローカルで削除されますが、ファイルはデータベースに残っています。 これが特定できない場合は、`SCC_CHANGE_DATABASE_ADDED`を返します。|
|`SCC_CHANGE_DATABASE_ADDED`|データベースに追加されたファイルがローカルに存在しません。|
|`SCC_CHANGE_LOCAL_ADDED`|ファイルはデータベースに存在せず、新しいローカル ファイルです。|
|`SCC_CHANGE_RENAMED_TO`|データベース内で ファイル名が変更`lpLatestName`または移動されたファイルは、 です。|
|`SCC_CHANGE_RENAMED_FROM`|データベース内で名前が変更されたか`lpLatestName`、データベース内で移動されたファイル 。この値が高すぎて追跡が行き過ぎた場合は、`SCC_CHANGE_DATABASE_ADDED`などの別のフラグを返します。|

 この項目の現在のファイル名です。

## <a name="see-also"></a>関連項目
- [IDE によって実装されるコールバック関数](../extensibility/callback-functions-implemented-by-the-ide.md)
- [SccQueryChanges](../extensibility/sccquerychanges-function.md)
- [エラー コード](../extensibility/error-codes.md)
