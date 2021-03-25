---
description: 'IDebugProgram2:: Execute は、停止状態からこのプログラムの実行を続行します。 前の実行状態 (ステップなど) がすべてクリアされ、プログラムの実行が再度開始されます。'
title: 'IDebugProgram2:: Execute |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::Execute
helpviewer_keywords:
- IDebugProgram2::Execute
ms.assetid: f7205ce8-0ac6-4fcd-b6ec-b720b4fcaccf
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 6112dbf51664458bc2d592951dcc842d1352020b
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105075992"
---
# <a name="idebugprogram2execute"></a>IDebugProgram2::Execute
このプログラムの実行を停止状態から続行します。 前の実行状態 (ステップなど) がすべてクリアされ、プログラムの実行が再度開始されます。

> [!NOTE]
> このメソッドは非推奨とされます。 代わりに、 [Execute](../../../extensibility/debugger/reference/idebugprocess3-execute.md) メソッドを使用してください。

## <a name="syntax"></a>構文

```cpp
HRESULT Execute(
   void
);
```

```csharp
int Execute();
```

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>注釈
 ユーザーが他のプログラムのスレッドで停止状態から実行を開始すると、このメソッドがこのプログラムで呼び出されます。 このメソッドは、ユーザーが IDE の [**デバッグ**] メニューから [**開始**] コマンドを選択したときにも呼び出されます。 このメソッドの実装は、プログラムの現在のスレッドで [Resume](../../../extensibility/debugger/reference/idebugthread2-resume.md) メソッドを呼び出す場合と同じように簡単に行うことができます。

> [!WARNING]
> この呼び出しの処理中に、停止イベントまたは即時 (同期) イベントを [イベント](../../../extensibility/debugger/reference/idebugeventcallback2-event.md) に送信しないでください。それ以外の場合、デバッガーは応答を停止する可能性があります。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
- [再開](../../../extensibility/debugger/reference/idebugthread2-resume.md)
