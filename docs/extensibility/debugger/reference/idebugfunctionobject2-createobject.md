---
description: 評価フラグの設定とタイムアウト値を指定したコンストラクターを使用するオブジェクトを作成します。
title: 'IDebugFunctionObject2:: CreateObject |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugFunctionObject2::CreateObject
- CreateObject
ms.assetid: 148de615-941e-4b64-ab11-75b692aae465
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b75cd2fae72d0ce8901445c3271a955100391d75
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105063566"
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

## <a name="remarks"></a>注釈
 このメソッドを呼び出して、クラスのインスタンス、またはコンストラクターを必要とする他の複合型 (パラメーター) を表すオブジェクトを作成します。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugFunctionObject2](../../../extensibility/debugger/reference/idebugfunctionobject2.md)
