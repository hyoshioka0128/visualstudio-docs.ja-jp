---
description: この関数は、ソース管理プラグインによってサポートされている追加の機能を返します。
title: SccGetExtendedCapabilities 関数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccGetExtendedCapabilities
helpviewer_keywords:
- SccGetExtendedCapabilities function
ms.assetid: 588c6a92-2147-4d8b-a357-96ca7da0a092
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e1409753559088c0f8129ebacd17387bfb7d111e
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102220782"
---
# <a name="sccgetextendedcapabilities-function"></a>SccGetExtendedCapabilities 関数
この関数は、ソース管理プラグインによってサポートされている追加の機能を返します。

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

からソース管理プラグインのコンテキストポインター。

 lSccExCaps

からテストする拡張機能を指定するフラグ (使用可能なフラグについては、 [機能フラグ](../extensibility/capability-flags.md) の拡張機能コードテーブルを参照してください)。

 pbSupported

入出力指定した機能がサポートされている場合は0以外 () を返します `TRUE` 。それ以外の場合は 0 () を返し `FALSE` ます。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装では、次の値のいずれかが返されることが想定されています。

|[値]|説明|
|-----------|-----------------|
|SCC_OK|機能の取得操作が正常に完了しました。|
|SCC_E_UNKNOWNERROR<br /><br /> SCC_E_NONSPECIFICERROR|不明または特定できないエラーが発生しました。|

## <a name="remarks"></a>解説
 このメソッドは、オンデマンドで呼び出されます。つまり、機能をテストする必要がある場合は、このメソッドを呼び出して、その機能がサポートされているかどうかを判断します。 一度に1つのフラグのみが指定されています。

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [エラー コード](../extensibility/error-codes.md)
- [機能フラグ](../extensibility/capability-flags.md)
