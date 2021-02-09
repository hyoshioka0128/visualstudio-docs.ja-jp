---
title: 'IDebugFunctionObject2:: CreateObject |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugFunctionObject2::CreateObject
- CreateObject
ms.assetid: 148de615-941e-4b64-ab11-75b692aae465
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 424599d322c2c8dd4db8ff4e19bab60eceaefc08
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99920995"
---
# <a name="idebugfunctionobject2createobject"></a>IDebugFunctionObject2::CreateObject
評価フラグの設定とタイムアウト値を指定したコンストラクターを使用するオブジェクトを作成します。

## <a name="syntax"></a>構文

```cpp
HRESULT CreateObject (
   IDebugFunctionObject* pConstructor,
   DWORD                 dwArgs,
   IDebugObject*         pArgs[],
   DWORD                 dwEvalFlags,
   DWORD                 dwTimeout,
   IDebugObject**        ppObject
);
```

```csharp
int CreateObject (
   IDebugFunctionObject pConstructor,
   uint                 dwArgs,
   IDebugObject[]       pArgs,
   uint                 dwEvalFlags,
   uint                 dwTimeout,
   out IDebugObject**   ppObject
);
```

## <a name="parameters"></a>パラメーター
`pConstructor`\
から作成されるオブジェクトのコンストラクターを表す [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md) オブジェクト。

`dwArgs`\
から配列内のパラメーターの数 `pArg` 。 コンストラクターに渡されるパラメーターの数を表します。

`pArgs`\
からコンストラクターに渡されたパラメーターを表す [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) オブジェクトの配列。

`dwEvalFlags`\
から評価を実行する方法を指定する、 [Evalflags](../../../extensibility/debugger/reference/evalflags.md) 列挙のフラグの組み合わせ。

`dwTimeout`\
からこのメソッドから戻る前に待機する最大時間 (ミリ秒単位)。 無期限に待機するには、 **無制限** を使用します。

`ppObject`\
入出力新しく作成されたオブジェクトを表す **IDebugObject** を返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
 このメソッドを呼び出して、クラスのインスタンス、またはコンストラクターを必要とする他の複合型 (パラメーター) を表すオブジェクトを作成します。

## <a name="see-also"></a>関連項目
- [IDebugFunctionObject2](../../../extensibility/debugger/reference/idebugfunctionobject2.md)
