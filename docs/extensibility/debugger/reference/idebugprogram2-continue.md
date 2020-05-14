---
title: プログラム 2::続行 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::Continue
helpviewer_keywords:
- IDebugProgram2::Continue
ms.assetid: e5a6e02a-d21b-4a03-a034-e8de1f71ce2e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 6d04445a7a1c444f30a0ef5c156dcd7ad744c6f1
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80723078"
---
# <a name="idebugprogram2continue"></a>IDebugProgram2::Continue
停止状態からこのプログラムを実行し続けます。 以前の実行状態 (ステップなど) は保持され、プログラムの実行は再び開始されます。

> [!NOTE]
> このメソッドは非推奨とされます。 代わりに[Continue](../../../extensibility/debugger/reference/idebugprocess3-continue.md)メソッドを使用してください。

## <a name="syntax"></a>構文

```cpp
HRESULT Continue( 
   IDebugThread2* pThread
);
```

```csharp
int Continue( 
   IDebugThread2 pThread
);
```

## <a name="parameters"></a>パラメーター
`pThread`[in]スレッドを表す[IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)オブジェクト。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 このメソッドは、デバッグ中のプログラムの数や停止イベントを生成したプログラムに関係なく、このプログラムで呼び出されます。 実装は、前の実行状態 (ステップなど) を保持し、前の実行を完了する前に停止したことがないかのように実行を続行する必要があります。 つまり、このプログラムのスレッドがステップ オーバー操作を行っていて、他のプログラムが停止したために停止し、このメソッドが呼び出された場合、プログラムは元のステップオーバー操作を完了する必要があります。

> [!WARNING]
> この呼び出しを処理する間は、停止イベントまたは即時 (同期) イベントを[Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)に送信しないでください。それ以外の場合は、デバッガーがハングする可能性があります。

## <a name="see-also"></a>関連項目
- [IDebugEngineProgram2](../../../extensibility/debugger/reference/idebugengineprogram2.md)
- [Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
