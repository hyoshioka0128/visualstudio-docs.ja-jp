---
title: Iデバッグプロセス3::続行 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess3::Continue
helpviewer_keywords:
- IDebugProcess3::Continue
ms.assetid: 57506242-5763-4c08-adb9-8a78ce02cebb
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f8fa2e21e31297279a173c9c9edd087adc560903
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80723771"
---
# <a name="idebugprocess3continue"></a>IDebugProcess3::Continue
停止状態からこのプロセスを実行し続けます。 以前の実行状態 (ステップなど) は保持され、プロセスの実行が再開されます。

> [!NOTE]
> このメソッドは[、Continue](../../../extensibility/debugger/reference/idebugprogram2-continue.md)の代わりに使用する必要があります。

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
`pThread`\
[in]継続するスレッドを表す[IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)オブジェクト。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 このメソッドは、デバッグ中のプロセスの数や、停止イベントを生成したプロセスに関係なく、このプロセスで呼び出されます。 実装は、前の実行状態 (ステップなど) を保持し、前の実行を完了する前に停止したことがないかのように実行を続行する必要があります。 つまり、このプロセスのスレッドがステップ オーバー操作を実行していて、他のプロセスが停止して呼び出されたために`Continue`停止した場合、指定されたスレッドは元のステップオーバー操作を完了する必要があります。

 **警告**この呼び出しを処理する間は、停止イベントまたは即時 (同期) イベントを[Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)に送信しないでください。それ以外の場合は、デバッガーがハングする可能性があります。

## <a name="see-also"></a>関連項目
- [IDebugProcess3](../../../extensibility/debugger/reference/idebugprocess3.md)
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
