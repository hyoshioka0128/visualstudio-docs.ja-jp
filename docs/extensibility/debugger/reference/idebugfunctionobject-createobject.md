---
description: コンストラクターを使用してオブジェクトを作成します。
title: 'IDebugFunctionObject:: CreateObject |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugFunctionObject::CreateObject
helpviewer_keywords:
- IDebugFunctionObject::CreateObject method
ms.assetid: c4c99dd5-609a-4e7c-8f29-eb728f57e995
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 8870910e01f2afa5bff6eac461d6e80f35e6a7e0
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102150043"
---
# <a name="idebugfunctionobjectcreateobject"></a>IDebugFunctionObject::CreateObject
コンストラクターを使用してオブジェクトを作成します。

## <a name="syntax"></a>構文

```cpp
HRESULT CreateObject( 
   IDebugFunctionObject* pConstructor,
   DWORD                 dwArgs,
   IDebugObject*         pArgs[],
   IDebugObject**        ppObject
);
```

```csharp
int CreateObject(
   IDebugFunctionObject pConstructor,
   uint                 dwArgs,
   IDebugObject[]       pArgs,
   out IDebugObject     ppObject
);
```

## <a name="parameters"></a>パラメーター
`pConstructor`\
から作成されるオブジェクトのコンストラクターを表す [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md) オブジェクト。

`dwArgs`\
から配列内のパラメーターの数 `pArg` 。 コンストラクターに渡されるパラメーターの数を表します。

`pArg`\
からコンストラクターに渡されたパラメーターを表す [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) オブジェクトの配列。

`ppObject`\
入出力 `IDebugObject` 新しく作成されたオブジェクトを表すを返します。

## <a name="return-value"></a>戻り値
 成功した場合は S_OK を返します。それ以外の場合は、エラーコードを返します。

## <a name="remarks"></a>解説
 このメソッドを呼び出して、 [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md) インターフェイスによって表される関数のパラメーターであるクラス (または、コンストラクターを必要とする他の複合型) のインスタンスを表すオブジェクトを作成します。

 オブジェクトパラメーターがコンストラクターを必要としない場合は、 [Createobjectnoconstructor](../../../extensibility/debugger/reference/idebugfunctionobject-createobjectnoconstructor.md) メソッドを呼び出します。

## <a name="see-also"></a>関連項目
- [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md)
- [CreateObjectNoConstructor](../../../extensibility/debugger/reference/idebugfunctionobject-createobjectnoconstructor.md)
