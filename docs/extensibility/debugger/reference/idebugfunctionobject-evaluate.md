---
title: 'IDebugFunctionObject:: Evaluate |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugFunctionObject::Evaluate
helpviewer_keywords:
- IDebugFunctionObject::Evaluate method
ms.assetid: 29349ea3-d5c1-4135-aa76-ced073ab9683
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 94285bc0ca36d4a55c3cd3a3483f6e20f6914271
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99920978"
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
から入力パラメーターを表す [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) オブジェクトの配列。 これらの各パラメーターは、IDebugFunctionObject インターフェイスのメソッドのいずれかを使用して作成されてい `Create` ます。 [](../../../extensibility/debugger/reference/idebugfunctionobject.md)

`dwParams`\
から配列内のパラメーターの数 `ppParams` 。

`dwTimeout`\
からこのメソッドから制御が戻るまでに待機する最大時間をミリ秒単位で指定します。 `INFINITE`無期限に待機するには、を使用します。

`ppResult`\
入出力関数の値をオブジェクトとして表す [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) を返します。

## <a name="return-value"></a>戻り値
 成功した場合は S_OK を返します。それ以外の場合は、エラーコードを返します。

## <a name="remarks"></a>解説
 このメソッドは、 [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md) オブジェクトによって表される関数の呼び出しを設定して実行します。

## <a name="see-also"></a>関連項目
- [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md)
