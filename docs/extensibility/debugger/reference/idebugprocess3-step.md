---
title: Iデバッグプロセス3::ステップ |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess3::Step
helpviewer_keywords:
- IDebugProcess3::Step
ms.assetid: 6ad9094c-27cc-4927-8a7c-1b4d97b2e436
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c5c4927f3f997b7fdbdca2b32977f2aa31a51219
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80723554"
---
# <a name="idebugprocess3step"></a>IDebugProcess3::Step
プロセスに 1 つの命令またはステートメントをステップさせます。

> [!NOTE]
> このメソッドは[、ステップ](../../../extensibility/debugger/reference/idebugprogram2-step.md)の代わりに使用する必要があります。

## <a name="syntax"></a>構文

```cpp
HRESULT Step(
   IDebugThread2* pThread,
   STEPKIND       sk,
   STEPUNIT       step,
);
```

```csharp
int Step(
   IDebugThread2 pThread,
   enum_STEPKIND sk,
   enum_STEPUNIT step
);
```

## <a name="parameters"></a>パラメーター
`pThread`\
[in]ステップされるスレッドを表す[IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)オブジェクト。

`sk`\
[in][STEPKIND](../../../extensibility/debugger/reference/stepkind.md)値の 1 つ。

`step`\
[in][STEPUNIT](../../../extensibility/debugger/reference/stepunit.md)値の 1 つ。

## <a name="return-value"></a>戻り値
 成功した場合は、S_OK返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 スレッド間でスレッドの同期や通信が行われた場合、特定のスレッドがステップ実行しているときに、プロセス内の他のスレッドを実行する必要があります。

 **警告**この呼び出しを処理する間は、停止イベントまたは即時 (同期) イベントを[Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)に送信しないでください。それ以外の場合は、デバッガーがハングする可能性があります。

## <a name="see-also"></a>関連項目
- [IDebugProcess3](../../../extensibility/debugger/reference/idebugprocess3.md)
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [STEPKIND](../../../extensibility/debugger/reference/stepkind.md)
- [STEPUNIT](../../../extensibility/debugger/reference/stepunit.md)
- [Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
