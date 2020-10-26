---
title: EVENTATTRIBUTES |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- EVENTATTRIBUTES
helpviewer_keywords:
- EVENTATTRIBUTES enumeration
ms.assetid: 04db10f7-df31-4464-98e8-b3777428179e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c479058a5e6abb61fb419425706d2a8b26858d04
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80737062"
---
# <a name="eventattributes"></a>EVENTATTRIBUTES
イベントの属性を指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_EVENTATTRIBUTES {
    EVENT_ASYNCHRONOUS          = 0x0000,
    EVENT_SYNCHRONOUS           = 0x0001,
    EVENT_STOPPING              = 0x0002,
    EVENT_ASYNC_STOP            = 0x0002,
    EVENT_SYNC_STOP             = 0x0003,
    EVENT_IMMEDIATE             = 0x0004,
    EVENT_EXPRESSION_EVALUATION = 0x0008
};
typedef DWORD EVENTATTRIBUTES;
```

```csharp
public enum enum_EVENTATTRIBUTES {
    EVENT_ASYNCHRONOUS          = 0x0000,
    EVENT_SYNCHRONOUS           = 0x0001,
    EVENT_STOPPING              = 0x0002,
    EVENT_ASYNC_STOP            = 0x0002,
    EVENT_SYNC_STOP             = 0x0003,
    EVENT_IMMEDIATE             = 0x0004,
    EVENT_EXPRESSION_EVALUATION = 0x0008
};
```

## <a name="fields"></a>フィールド
`EVENT_ASYNCHRONOUS`\
イベントが非同期であり、イベントへの応答を必要としないことを示します。

`EVENT_SYNCHRONOUS`\
イベントが同期であることを示します。 [ContinueFromSynchronousEvent](../../../extensibility/debugger/reference/idebugengine2-continuefromsynchronousevent.md)を通じて返信します。

`EVENT_STOPPING`\
これが停止イベントであることを示します。 は、またはのいずれかと組み合わせる必要があり `EVENT_ASYNCHRONOUS` `EVENT_SYNCHRONOUS` ます。

`EVENT_ASYNC_STOP`\
非同期の停止イベントを示します。 現在、このようなイベントはありません。 このフラグは単なるプレースホルダーです。

`EVENT_SYNC_STOP`\
同期停止イベント (との組み合わせ) を `EVENT_SYNCHRONOUS` 示し `EVENT_STOPPING` ます。 この値は、停止イベントを送信するときにデバッグエンジン (DE) によって使用されます。 応答は、 [Execute](../../../extensibility/debugger/reference/idebugprogram2-execute.md)、 [Step](../../../extensibility/debugger/reference/idebugprogram2-step.md)、または [Continue](../../../extensibility/debugger/reference/idebugprogram2-continue.md)を呼び出すことによって行われます。

`EVENT_IMMEDIATE`\
すぐに、IDE に同期的に送信されるイベントを示します。 このフラグは、、、などの他のフラグと組み合わせて、 `EVENT_ASYNCHRONOUS` `EVENT_SYNCHRONOUS` `EVENT_SYNC_STOP` イベントの種類と、応答機構 (存在する場合) がわかっていることを示します。

`EVENT_EXPRESSION_EVALUATION`\
イベントは、式の評価の結果です。

## <a name="remarks"></a>解説
これらの値は、 `dwAttrib` [イベント](../../../extensibility/debugger/reference/idebugeventcallback2-event.md) メソッドのパラメーターで渡されます。

これらの値は、ビットごとのを使用して組み合わせることができ `OR` ます。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg. h

名前空間: VisualStudio。

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [ContinueFromSynchronousEvent](../../../extensibility/debugger/reference/idebugengine2-continuefromsynchronousevent.md)
- [Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
