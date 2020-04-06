---
title: Iデバッグプログラム2::ステップ |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::Step
helpviewer_keywords:
- IDebugProgram2::Step
ms.assetid: e4c2ffce-9810-4088-8162-eac9ef04f2a9
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 194e72eba5a3f137e4650752a090d91ad7c402fa
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80722760"
---
# <a name="idebugprogram2step"></a>IDebugProgram2::Step
ステップを実行します。

> [!NOTE]
> このメソッドは非推奨とされます。 代わりに[Step](../../../extensibility/debugger/reference/idebugprocess3-step.md)メソッドを使用してください。

## <a name="syntax"></a>構文

```cpp
HRESULT Step( 
   IDebugThread2*  pThread,
   STEPKIND        sk,
   STEPUNIT        step
);
```

```csharp
int Step( 
   IDebugThread2  pThread,
   enum_STEPKIND  sk,
   enum_STEPUNIT  step
);
```

## <a name="parameters"></a>パラメーター
`pThread`\
[in]ステップされるスレッドを表す[IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)オブジェクト。

`sk`\
[in]ステップの種類を指定する[STEPKIND](../../../extensibility/debugger/reference/stepkind.md)列挙体の値。

`step`\
[in]ステップ単位を指定する[STEPUNIT](../../../extensibility/debugger/reference/stepunit.md)列挙体の値 (例えば、ステートメントまたは命令による)。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 スレッド間でスレッドの同期や通信が行われた場合、プログラム内の他のスレッドは、特定のスレッドがステップ実行しているときに実行する必要があります。

> [!WARNING]
> この呼び出しを処理する間は、停止イベントまたは即時 (同期) イベントを[Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)に送信しないでください。それ以外の場合は、デバッガーがハングする可能性があります。

## <a name="see-also"></a>関連項目
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugEngineProgram2](../../../extensibility/debugger/reference/idebugengineprogram2.md)
- [Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
