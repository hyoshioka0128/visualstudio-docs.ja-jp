---
title: 'IDebugProgram2:: Execute |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::Execute
helpviewer_keywords:
- IDebugProgram2::Execute
ms.assetid: f7205ce8-0ac6-4fcd-b6ec-b720b4fcaccf
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 25f1544fe13c6dc44aa90b73f69854893beae14f
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99844737"
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

## <a name="remarks"></a>解説
 ユーザーが他のプログラムのスレッドで停止状態から実行を開始すると、このメソッドがこのプログラムで呼び出されます。 このメソッドは、ユーザーが IDE の [**デバッグ**] メニューから [**開始**] コマンドを選択したときにも呼び出されます。 このメソッドの実装は、プログラムの現在のスレッドで [Resume](../../../extensibility/debugger/reference/idebugthread2-resume.md) メソッドを呼び出す場合と同じように簡単に行うことができます。

> [!WARNING]
> この呼び出しの処理中に、停止イベントまたは即時 (同期) イベントを [イベント](../../../extensibility/debugger/reference/idebugeventcallback2-event.md) に送信しないでください。それ以外の場合、デバッガーは応答を停止する可能性があります。

## <a name="see-also"></a>関連項目
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
- [再開](../../../extensibility/debugger/reference/idebugthread2-resume.md)
