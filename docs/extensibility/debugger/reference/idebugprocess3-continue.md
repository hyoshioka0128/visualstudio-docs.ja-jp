---
description: このプロセスの実行を停止状態から続行します。 前の実行状態 (ステップなど) はすべて保持され、プロセスは再度実行を開始します。
title: 'IDebugProcess3:: Continue |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess3::Continue
helpviewer_keywords:
- IDebugProcess3::Continue
ms.assetid: 57506242-5763-4c08-adb9-8a78ce02cebb
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 11f2d5b652b950976834b8ba18f71a1dc0d1b34c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105081582"
---
# <a name="idebugprocess3continue"></a>IDebugProcess3::Continue
このプロセスの実行を停止状態から続行します。 前の実行状態 (ステップなど) はすべて保持され、プロセスは再度実行を開始します。

> [!NOTE]
> このメソッドは、 [Continue](../../../extensibility/debugger/reference/idebugprogram2-continue.md)の代わりに使用する必要があります。

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
から続行するスレッドを表す [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md) オブジェクト。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>注釈
 このメソッドは、デバッグされているプロセスの数や、停止イベントを生成したプロセスに関係なく、このプロセスで呼び出されます。 の実装では、前の実行状態 (ステップなど) を保持し、以前の実行を完了する前に停止していないかのように実行を継続する必要があります。 つまり、このプロセス内のスレッドがステップオーバー操作を行っていて、他のプロセスが停止したために停止された場合は、 `Continue` 指定されたスレッドが元のステップオーバー操作を完了する必要があります。

 **警告** この呼び出しの処理中に、停止イベントまたは即時 (同期) イベントを [イベント](../../../extensibility/debugger/reference/idebugeventcallback2-event.md) に送信しないでください。それ以外の場合、デバッガーは応答を停止する可能性があります。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugProcess3](../../../extensibility/debugger/reference/idebugprocess3.md)
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
