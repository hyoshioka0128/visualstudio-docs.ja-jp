---
title: オブジェクトを作成する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugFunctionObject::CreateObject
helpviewer_keywords:
- IDebugFunctionObject::CreateObject method
ms.assetid: c4c99dd5-609a-4e7c-8f29-eb728f57e995
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: beb00bcf932b19ed4e489456236957c55d909ce4
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80728600"
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
[in]作成[する](../../../extensibility/debugger/reference/idebugfunctionobject.md)オブジェクトのコンストラクターを表すオブジェクト。

`dwArgs`\
[in]配列内のパラメーターの`pArg`数。 コンストラクターに渡されるパラメーターの数を表します。

`pArg`\
[in]コンストラクターに渡されるパラメーターを表す[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)オブジェクトの配列。

`ppObject`\
[アウト]新しく`IDebugObject`作成されたオブジェクトを表すを返します。

## <a name="return-value"></a>戻り値
 成功した場合は、S_OK返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 このメソッドを呼び出して、[クラス](../../../extensibility/debugger/reference/idebugfunctionobject.md)(またはコンストラクターを必要とするその他の複合型) のインスタンスを表すオブジェクトを作成します。

 オブジェクト パラメーターにコンストラクターが必要ない場合は、[メソッド](../../../extensibility/debugger/reference/idebugfunctionobject-createobjectnoconstructor.md)を呼び出します。

## <a name="see-also"></a>関連項目
- [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md)
- [CreateObjectNoConstructor](../../../extensibility/debugger/reference/idebugfunctionobject-createobjectnoconstructor.md)
