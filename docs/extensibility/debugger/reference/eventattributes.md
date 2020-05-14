---
title: イベント属性 |マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737062"
---
# <a name="eventattributes"></a>EVENTATTRIBUTES
イベント属性を指定します。

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
イベントが非同期であり、イベントへの応答が不要であることを示します。

`EVENT_SYNCHRONOUS`\
イベントが同期的であることを示します。[同期イベントを使用](../../../extensibility/debugger/reference/idebugengine2-continuefromsynchronousevent.md)して応答します。

`EVENT_STOPPING`\
これが停止イベントであることを示します。 または`EVENT_ASYNCHRONOUS``EVENT_SYNCHRONOUS`のいずれかと組み合わせる必要があります。

`EVENT_ASYNC_STOP`\
非同期停止イベントを示します。 現在、このようなイベントはありません。 このフラグはプレースホルダーにすぎません。

`EVENT_SYNC_STOP`\
同期停止イベントを示します (`EVENT_SYNCHRONOUS`と`EVENT_STOPPING`の組み合わせ)。 この値は、停止イベントを送信するときにデバッグ エンジン (DE) によって使用されます。 応答は、[実行](../../../extensibility/debugger/reference/idebugprogram2-execute.md)、[ステップ](../../../extensibility/debugger/reference/idebugprogram2-step.md)、または続行 を呼び出すことによって行[われます](../../../extensibility/debugger/reference/idebugprogram2-continue.md)。

`EVENT_IMMEDIATE`\
IDE に即時かつ同期的に送信されるイベントを示します。 このフラグは、 、`EVENT_ASYNCHRONOUS``EVENT_SYNCHRONOUS`または`EVENT_SYNC_STOP`などの他のフラグと組み合わせて、イベントの種類と、応答メカニズム (存在する場合) が既知であることを示します。

`EVENT_EXPRESSION_EVALUATION`\
イベントは式の評価の結果です。

## <a name="remarks"></a>Remarks
これらの値は[、Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md) `dwAttrib`メソッドのパラメーターに渡されます。

これらの値はビット単位`OR`で組み合わせることができる。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: を使用します。

アセンブリ:

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [ContinueFromSynchronousEvent](../../../extensibility/debugger/reference/idebugengine2-continuefromsynchronousevent.md)
- [Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
