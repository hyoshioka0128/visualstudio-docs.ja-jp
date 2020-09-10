---
title: IDebugEngineProgram2::WatchForExpressionEvaluationOnThread
titleSuffix: ''
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
ms.openlocfilehash: c1328423cd81db6e55964795ef9da23c5bb29811
ms.sourcegitcommit: 2a201c93ed526b0f7e5848657500f1111b08ac2a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2020
ms.locfileid: "89737001"
---
# <a name="idebugengineprogram2watchforexpressionevaluationonthread"></a>IDebugEngineProgram2::WatchForExpressionEvaluationOnThread
プログラムが停止している場合でも、指定したスレッドで式の評価を実行できるようにします (または禁止します)。

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
から式を評価しているプログラムを表す [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) オブジェクト。

`dwTid`\
からスレッドの識別子を指定します。

`dwEvalFlags`\
から評価を実行する方法を指定する、 [Evalflags](../../../extensibility/debugger/reference/evalflags.md) 列挙のフラグの組み合わせ。

`pExprCallback`\
から式の評価中に発生するデバッグイベントを送信するために使用される [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) オブジェクト。

`fWatch`\
から0以外 ( `TRUE` ) の場合、で識別されるスレッドで式の評価が許可さ `dwTid` れます。それ以外の場合、ゼロ ( `FALSE` ) はそのスレッドで式の評価を許可しません。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
 セッションデバッグマネージャー (SDM) が、パラメーターで識別されるプログラムに対して、式を評価するように要求すると `pOriginatingProgram` 、このメソッドを呼び出すことによって、添付されている他のすべてのプログラムに通知します。

 1つのプログラムでの式の評価では、関数の評価やプロパティの評価により、コードが別のプログラムで実行される場合があり `IDispatch` ます。 このため、このメソッドでは、このプログラムでスレッドが停止していても、式の評価を実行して完了することができます。

## <a name="see-also"></a>関連項目
- [IDebugEngineProgram2](../../../extensibility/debugger/reference/idebugengineprogram2.md)
- [EVALFLAGS](../../../extensibility/debugger/reference/evalflags.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
