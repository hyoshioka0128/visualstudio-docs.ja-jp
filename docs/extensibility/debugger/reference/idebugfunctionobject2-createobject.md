---
title: オブジェクト 2::オブジェクトの作成 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugFunctionObject2::CreateObject
- CreateObject
ms.assetid: 148de615-941e-4b64-ab11-75b692aae465
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 6de1a30a032919a90fbb3d760837d5eeca00feaf
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80728482"
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
[in]作成[する](../../../extensibility/debugger/reference/idebugfunctionobject.md)オブジェクトのコンストラクターを表すオブジェクト。

`dwArgs`\
[in]配列内のパラメーターの`pArg`数。 コンストラクターに渡されるパラメーターの数を表します。

`pArgs`\
[in]コンストラクターに渡されるパラメーターを表す[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)オブジェクトの配列。

`dwEvalFlags`\
[in]評価の実行方法を指定する[EVALFLAGS](../../../extensibility/debugger/reference/evalflags.md)列挙体のフラグの組み合わせ。

`dwTimeout`\
[in]このメソッドから戻るまでの最大待機時間 (ミリ秒単位)。 **無限**に待機するには INFINITE を使用します。

`ppObject`\
[アウト]新しく作成されたオブジェクトを表す**IDebugObject**を返します。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 クラスのインスタンスを表すオブジェクト、またはコンストラクターを必要とするその他の複合型を表すオブジェクトを作成します。

## <a name="see-also"></a>関連項目
- [IDebugFunctionObject2](../../../extensibility/debugger/reference/idebugfunctionobject2.md)
