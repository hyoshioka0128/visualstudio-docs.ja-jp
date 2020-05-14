---
title: を使用してプログラムを実行します。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngineProgram2::WatchForExpressionEvaluationOnThread
helpviewer_keywords:
- IDebugEngineProgram2::WatchForExpressionEvaluationOnThread
ms.assetid: 01d05e77-8cac-4d1b-b19f-25756767ed27
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e988e1d64af38a55f5d946f704e1edb4df29b1d5
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80730365"
---
# <a name="idebugengineprogram2watchforexpressionevaluationonthread"></a>IDebugEngineProgram2::WatchForExpressionEvaluationOnThread
プログラムが停止した場合でも、指定されたスレッドで式の評価を行うことを許可します (または、許可しません)。

## <a name="syntax"></a>構文

```cpp
HRESULT WatchForExpressionEvaluationOnThread( 
   IDebugProgram2*       pOriginatingProgram,
   DWORD                 dwTid,
   DWORD                 dwEvalFlags,
   IDebugEventCallback2* pExprCallback,
   BOOL                  fWatch
);
```

```csharp
int WatchForExpressionEvaluationOnThread( 
   IDebugProgram2       pOriginatingProgram,
   uint                  dwTid,
   uint                  dwEvalFlags,
   IDebugEventCallback2 pExprCallback,
   int                   fWatch
);
```

## <a name="parameters"></a>パラメーター
`pOriginatingProgram`\
[in]式を評価するプログラムを表す[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)オブジェクト。

`dwTid`\
[in]スレッドの識別子を指定します。

`dwEvalFlags`\
[in]評価の実行方法を指定する[EVALFLAGS](../../../extensibility/debugger/reference/evalflags.md)列挙体のフラグの組み合わせ。

`pExprCallback`\
[in]式の評価中に発生するデバッグ イベントを送信するために使用される[IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)オブジェクト。

`fWatch`\
[in]0 以外の場合`TRUE`( ) で識別されるスレッド`dwTid`で式の評価が可能です。それ以外の場合`FALSE`は、そのスレッドに対する式の評価を 0 ( ) に許可しません。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 セッション デバッグ マネージャー (SDM) は、`pOriginatingProgram`式を評価するパラメーターで識別されるプログラムを要求するとき、このメソッドを呼び出すことによって、他のすべての接続されたプログラムを通知します。

 あるプログラムでの式の評価により、関数の評価またはプロパティの評価により、コードが別`IDispatch`のプログラムで実行される可能性があります。 このため、このメソッドを使用すると、このプログラムでスレッドを停止しても、式の評価を実行して完了できます。

## <a name="see-also"></a>関連項目
- [IDebugEngineProgram2](../../../extensibility/debugger/reference/idebugengineprogram2.md)
- [EVALFLAGS](../../../extensibility/debugger/reference/evalflags.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
