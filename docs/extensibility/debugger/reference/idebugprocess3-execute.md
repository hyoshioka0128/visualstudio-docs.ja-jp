---
description: このプロセスの実行を停止状態から続行します。 前の実行状態 (ステップなど) がすべてクリアされ、プロセスが再度実行を開始します。
title: 'IDebugProcess3:: Execute |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess3::Execute
helpviewer_keywords:
- IDebugProcess3::Execute
ms.assetid: d831cd81-d7bf-4172-8517-aa699867791f
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 149497bcee5c37813e9d1134237ddb991d5893da
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102150251"
---
# <a name="idebugprocess3execute"></a>IDebugProcess3::Execute
このプロセスの実行を停止状態から続行します。 前の実行状態 (ステップなど) がすべてクリアされ、プロセスが再度実行を開始します。

> [!NOTE]
> このメソッドは、 [Execute](../../../extensibility/debugger/reference/idebugprogram2-execute.md)の代わりに使用する必要があります。

## <a name="syntax"></a>構文

```cpp
HRESULT Execute(
   IDebugThread2* pThread
);
```

```csharp
int Execute(
   IDebugThread2 pThread
);
```

## <a name="parameters"></a>パラメーター
`pThread`\
から実行するスレッドを表す [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md) オブジェクト。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
 ユーザーが他のプロセスのスレッドで停止状態から実行を開始すると、このプロセスでこのメソッドが呼び出されます。 このメソッドは、ユーザーが IDE の [**デバッグ**] メニューから [**開始**] コマンドを選択したときにも呼び出されます。 このメソッドの実装は、プロセス内の現在のスレッドで [Resume](../../../extensibility/debugger/reference/idebugthread2-resume.md) メソッドを呼び出す場合と同じように簡単に行うことができます。

> [!WARNING]
> この呼び出しの処理中に、停止イベントまたは即時 (同期) イベントを [イベント](../../../extensibility/debugger/reference/idebugeventcallback2-event.md) に送信しないでください。それ以外の場合、デバッガーは応答を停止する可能性があります。

## <a name="see-also"></a>関連項目
- [IDebugProcess3](../../../extensibility/debugger/reference/idebugprocess3.md)
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [Resume](../../../extensibility/debugger/reference/idebugthread2-resume.md)
- [Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
