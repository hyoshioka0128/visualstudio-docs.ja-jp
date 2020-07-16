---
title: 'IDebugProgram2:: Continue |Microsoft Docs'
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
ms.openlocfilehash: ee73ea3a9b65635cf14d4d345bf22de4e9593989
ms.sourcegitcommit: a77158415da04e9bb8b33c332f6cca8f14c08f8c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2020
ms.locfileid: "86387084"
---
# <a name="idebugprogram2continue"></a>IDebugProgram2::Continue
このプログラムの実行を停止状態から続行します。 前の実行状態 (ステップなど) はすべて保持され、プログラムは再度実行を開始します。

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
`pThread`からスレッドを表す[IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)オブジェクト。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
 このメソッドは、デバッグされているプログラムの数や、停止イベントを生成したプログラムに関係なく、このプログラムで呼び出されます。 の実装では、前の実行状態 (ステップなど) を保持し、以前の実行を完了する前に停止していないかのように実行を継続する必要があります。 つまり、このプログラムのスレッドがステップオーバー操作を行っていて、他のプログラムが停止したために停止された場合、このメソッドが呼び出されたときには、プログラムは元のステップオーバー操作を完了する必要があります。

> [!WARNING]
> この呼び出しの処理中に、停止イベントまたは即時 (同期) イベントを[イベント](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)に送信しないでください。それ以外の場合、デバッガーは応答を停止する可能性があります。

## <a name="see-also"></a>関連項目
- [IDebugEngineProgram2](../../../extensibility/debugger/reference/idebugengineprogram2.md)
- [Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
