---
description: プロセスで1つの命令またはステートメントをステップ実行します。
title: 'IDebugProcess3:: Step |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess3::Step
helpviewer_keywords:
- IDebugProcess3::Step
ms.assetid: 6ad9094c-27cc-4927-8a7c-1b4d97b2e436
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 0d5c9e43676751a97baf0bf664c3da17dcf9aca5
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105076525"
---
# <a name="idebugprocess3step"></a>IDebugProcess3::Step
プロセスで1つの命令またはステートメントをステップ実行します。

> [!NOTE]
> このメソッドは、 [ステップ](../../../extensibility/debugger/reference/idebugprogram2-step.md)の代わりに使用する必要があります。

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
からステップ処理中のスレッドを表す [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md) オブジェクト。

`sk`\
から [Stepkind](../../../extensibility/debugger/reference/stepkind.md) 値の1つ。

`step`\
から [Stepunit](../../../extensibility/debugger/reference/stepunit.md) 値の1つ。

## <a name="return-value"></a>戻り値
 成功した場合は S_OK を返します。それ以外の場合は、エラーコードを返します。

## <a name="remarks"></a>注釈
 スレッド間の同期またはスレッド間の通信がある場合、プロセス内の他のスレッドは、特定のスレッドがステップ実行されているときに実行する必要があります。

 **警告** この呼び出しの処理中に、停止イベントまたは即時 (同期) イベントを [イベント](../../../extensibility/debugger/reference/idebugeventcallback2-event.md) に送信しないでください。それ以外の場合、デバッガーは応答を停止する可能性があります。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugProcess3](../../../extensibility/debugger/reference/idebugprocess3.md)
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [STEPKIND](../../../extensibility/debugger/reference/stepkind.md)
- [STEPUNIT](../../../extensibility/debugger/reference/stepunit.md)
- [Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
