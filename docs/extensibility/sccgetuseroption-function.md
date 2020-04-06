---
title: 関数を使用する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccGetUserOption
helpviewer_keywords:
- SccGetUserOption function
ms.assetid: 17863747-1901-4c53-a2b3-ed996085e120
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: dc7b68df3331c1240ad833048940e656da034ccf
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80700682"
---
# <a name="sccgetuseroption-function"></a>SccGetUserOption 関数
この関数は、ユーザー固有のさまざまなオプションを取得します。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccGetUserOption(
   LPVOID pContext,
   LONG nOption,
   LPLONG lpVal
);
```

#### <a name="parameters"></a>パラメーター
 pContext

[in]ソース管理プラグイン のコンテキスト ポインター。

 nオプション

[in]取得するオプション (可能なオプションについては、「解説」を参照)。

 lpVal

[アウト]オプションに関連付けられた値。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装は、次のいずれかの値を返します。

|[値]|説明|
|-----------|-----------------|
|SCC_OK|オプションが正常に取得されました。|
|SCC_E_OPNOTSUPPORTED|オプションはサポートされていません。|
|SCC_E_NONSPECIFICERROR|未指定のエラーが発生しました。|

## <a name="remarks"></a>Remarks
 このコマンドでは、次のオプションがサポートされています。

|ユーザー オプション|説明|
|-----------------|-----------------|
|`SCC_USEROPT_CHECKOUT_LOCALVER`|ユーザーがファイルのローカル バージョンをチェックアウトするかどうかを決定します。 `lpVal`が割`SCC_USEROPT_COLV_YES`り当てられている (ユーザーはローカル ファイル`SCC_USEROPT_COLV_NO`をチェックアウトする) または が使用されます。|

## <a name="see-also"></a>関連項目
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [エラー コード](../extensibility/error-codes.md)
