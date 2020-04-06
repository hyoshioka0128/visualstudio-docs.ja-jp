---
title: 関数オブジェクト::評価 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugFunctionObject::Evaluate
helpviewer_keywords:
- IDebugFunctionObject::Evaluate method
ms.assetid: 29349ea3-d5c1-4135-aa76-ced073ab9683
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 529a5f67c808efa258bc0cb9899f546dbb90d431
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80728513"
---
# <a name="idebugfunctionobjectevaluate"></a>IDebugFunctionObject::Evaluate
関数を呼び出し、結果の値をオブジェクトとして返します。

## <a name="syntax"></a>構文

```cpp
HRESULT Evaluate( 
   IDebugObject** ppParams,
   DWORD          dwParams,
   DWORD          dwTimeout,
   IDebugObject** ppResult
);
```

```csharp
int Evaluate(
   IDebugObject[]   ppParams,
   IntPtr           dwParams,
   uint             dwTimeout,
   out IDebugObject ppResult
);
```

## <a name="parameters"></a>パラメーター
`ppParams`\
[in]入力パラメーターを表す[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)オブジェクトの配列。 これらの各パラメーターは[、IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md) `Create`インターフェイスのメソッドの 1 つを使用して作成されました。

`dwParams`\
[in]配列内のパラメーターの`ppParams`数。

`dwTimeout`\
[in]このメソッドから戻るまでの最大待機時間をミリ秒単位で指定します。 無期限`INFINITE`に待機するために使用します。

`ppResult`\
[アウト]オブジェクトとして関数の値を表す[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、S_OK返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 このメソッドは[、IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md)オブジェクトによって表される関数の呼び出しを設定して実行します。

## <a name="see-also"></a>関連項目
- [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md)
