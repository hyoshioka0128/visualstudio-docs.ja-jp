---
title: 関数の機能を拡張するマイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccGetExtendedCapabilities
helpviewer_keywords:
- SccGetExtendedCapabilities function
ms.assetid: 588c6a92-2147-4d8b-a357-96ca7da0a092
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5247f2de7ffc63db7235f915c72b3274b8fee5f5
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80700725"
---
# <a name="sccgetextendedcapabilities-function"></a>関数
この関数は、ソース管理プラグインでサポートされている追加機能を返します。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccGetExtendedCapabilities(
   LPVOID pContext,
   LONG lSccExCaps,
   LPBOOL pbSupported
);
```

### <a name="parameters"></a>パラメーター
 pContext

[in]ソース管理プラグイン のコンテキスト ポインター。

 lSccExCaps

[in]テスト対象の拡張機能を指定するフラグ (可能なフラグについては、[機能フラグ](../extensibility/capability-flags.md)の拡張能力コード表を参照)。

 pbサポート

[アウト]指定された機能がサポート`TRUE`されている場合は、ゼロ以外 ( ) を返します。それ以外の場合は`FALSE`、ゼロ ( ) を返します。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装は、次のいずれかの値を返します。

|[値]|説明|
|-----------|-----------------|
|SCC_OK|機能の取得操作が正常に完了しました。|
|SCC_E_UNKNOWNERROR<br /><br /> SCC_E_NONSPECIFICERROR|不明または指定されていないエラーが発生しました。|

## <a name="remarks"></a>Remarks
 このメソッドは、要求時に呼び出されます。つまり、機能をテストする必要がある場合、このメソッドが呼び出され、その機能がサポートされているかどうかを判断します。 一度に 1 つのフラグのみが指定されます。

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [エラー コード](../extensibility/error-codes.md)
- [機能フラグ](../extensibility/capability-flags.md)
