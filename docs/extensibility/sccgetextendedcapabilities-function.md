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
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ca2f2f77c586c5c71658a8f0cab32385eb3f73d3
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105073002"
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

|値|説明|
|-----------|-----------------|
|SCC_OK|機能の取得操作が正常に完了しました。|
|SCC_E_UNKNOWNERROR<br /><br /> SCC_E_NONSPECIFICERROR|不明または特定できないエラーが発生しました。|

## <a name="remarks"></a>注釈
 このメソッドは、オンデマンドで呼び出されます。つまり、機能をテストする必要がある場合は、このメソッドを呼び出して、その機能がサポートされているかどうかを判断します。 一度に1つのフラグのみが指定されています。

## <a name="see-also"></a>こちらもご覧ください
- [ソース管理プラグイン API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [エラー コード](../extensibility/error-codes.md)
- [機能フラグ](../extensibility/capability-flags.md)
