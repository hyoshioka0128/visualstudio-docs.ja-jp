---
title: イベントコールバック2::イベント |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEventCallback2::Event
helpviewer_keywords:
- IDebugEventCallback2::Event
ms.assetid: e5a3345b-d460-4e40-8f5b-3111c56a2ed9
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 0b60c09b21d531326e343dddd2f1cc69cfb0e5d2
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80729896"
---
# <a name="idebugeventcallback2event"></a>IDebugEventCallback2::Event
デバッグ イベントの通知を送信します。

## <a name="syntax"></a>構文

```cpp
HRESULT Event( 
   IDebugEngine2*  pEngine,
   IDebugProcess2* pProcess,
   IDebugProgram2* pProgram,
   IDebugThread2*  pThread,
   IDebugEvent2*   pEvent,
   REFIID          riidEvent,
   DWORD           dwAttrib
);
```

```csharp
int Event( 
   IDebugEngine2  pEngine,
   IDebugProcess2 pProcess,
   IDebugProgram2 pProgram,
   IDebugThread2  pThread,
   IDebugEvent2   pEvent,
   ref Guid       riidEvent,
   uint           dwAttrib
);
```

## <a name="parameters"></a>パラメーター
`pEngine`\
[in]このイベントを送信するデバッグ エンジン (DE) を表す[IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)オブジェクト。 このパラメータを入力するには DE が必要です。

`pProcess`\
[in]イベントが発生するプロセスを表す[IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)オブジェクト。 このパラメーターは、セッションデバッグ マネージャー (SDM) によって入力されます。 DE は、常にこのパラメーターに null 値を渡します。

`pProgram`\
[in]このイベントが発生するプログラムを表す[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)オブジェクト。 ほとんどのイベントでは、このパラメーターは null 値ではありません。

`pThread`\
[in]このイベントが発生するスレッドを表す[IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)オブジェクト。 停止イベントの場合、スタック フレームはこのパラメーターから取得されるので、このパラメーターを null 値にすることはできません。

`pEvent`\
[in]デバッグ イベントを表す[IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)オブジェクト。

`riidEvent`\
[in]パラメーターから取得するイベント インターフェイスを識別する`pEvent`GUID。

`dwAttrib`\
[in][イベント属性](../../../extensibility/debugger/reference/eventattributes.md)列挙体のフラグの組み合わせ。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 このメソッドを呼び出`dwAttrib`すとき、パラメーターは、パラメーターで渡されたイベント オブジェクトで呼び出される[GetAttributes](../../../extensibility/debugger/reference/idebugevent2-getattributes.md)メソッドから返される値と一致する`pEvent`必要があります。

 すべてのデバッグ イベントは、イベント自体が非同期かどうかに関係なく、非同期でポストされます。 DE がこのメソッドを呼び出すとき、戻り値はイベントが処理されたかどうかを示すものではなく、イベントが受信されたかどうかのみを示します。 実際、ほとんどの場合、このメソッドが返されるときにイベントは処理されていません。

## <a name="see-also"></a>関連項目
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [EVENTATTRIBUTES](../../../extensibility/debugger/reference/eventattributes.md)
