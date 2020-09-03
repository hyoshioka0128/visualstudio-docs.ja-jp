---
title: 'IDebugProgram2:: Step |Microsoft Docs'
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
ms.openlocfilehash: c6a70a96014ebf18984c75df60cfeb75ba0d0577
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "86387240"
---
# <a name="idebugprogram2step"></a>IDebugProgram2::Step
ステップを実行します。

> [!NOTE]
> このメソッドは非推奨とされます。 代わりに、 [Step](../../../extensibility/debugger/reference/idebugprocess3-step.md) メソッドを使用してください。

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
から階段状のスレッドを表す [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md) オブジェクト。

`sk`\
からステップの種類を指定する [stepkind](../../../extensibility/debugger/reference/stepkind.md) 列挙の値です。

`step`\
からステップの単位 (ステートメントや命令など) を指定する [stepunit](../../../extensibility/debugger/reference/stepunit.md) 列挙の値です。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
 スレッド間の同期またはスレッド間の通信がある場合、プログラム内の他のスレッドは、特定のスレッドのステップ実行時に実行されます。

> [!WARNING]
> この呼び出しの処理中に、停止イベントまたは即時 (同期) イベントを [イベント](../../../extensibility/debugger/reference/idebugeventcallback2-event.md) に送信しないでください。それ以外の場合、デバッガーは応答を停止する可能性があります。

## <a name="see-also"></a>関連項目
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugEngineProgram2](../../../extensibility/debugger/reference/idebugengineprogram2.md)
- [Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
