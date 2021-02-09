---
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
ms.openlocfilehash: e6085e974f58346eba7b38e76e5588b34fc3ff2c
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99929989"
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
