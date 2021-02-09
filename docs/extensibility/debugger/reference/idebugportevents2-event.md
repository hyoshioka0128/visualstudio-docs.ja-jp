---
title: 'IDebugPortEvents2:: Event |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortEvents2::Event
helpviewer_keywords:
- IDebugPortEvents2::Event
ms.assetid: 5cc813f7-04a1-4462-9ea7-fbddcf0e0143
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: bcf8a827f09c1b8d0e83b92f7729635cbb0f7f18
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99896176"
---
# <a name="idebugportevents2event"></a>IDebugPortEvents2::Event
このメソッドは、ポート上のプロセスとプログラムの作成と破棄を示すイベントを送信します。

## <a name="syntax"></a>構文

```cpp
HRESULT Event(
   IDebugCoreServer2* pServer,
   IDebugPort2*       pPort,
   IDebugProcess2*    pProcess,
   IDebugProgram2*    pProgram,
   IDebugEvent2*      pEvent,
   REFIID             riidEvent
);
```

```csharp
int Event(
   IDebugCoreServer2 pServer,
   IDebugPort2       pPort,
   IDebugProcess2    pProcess,
   IDebugProgram2    pProgram,
   IDebugEvent2      pEvent,
   ref Guid          riidEvent
);
```

## <a name="parameters"></a>パラメーター
`pMachine`\
からイベントが発生した (のすべてのインスタンスに対して1つの) デバッグサーバーを表す [IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md) オブジェクトです [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] 。

`pPort`\
からイベントが発生したポートを表す [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md) オブジェクト。

`pProcess`\
からイベントが発生したプロセスを表す [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md) オブジェクト。

`pProgram`\
からイベントが発生したプログラムを表す [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) オブジェクト。

`pEvent`\
からイベントを識別する [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) オブジェクト。 考えられるイベントは次のとおりです。

- [IDebugProcessCreateEvent2](../../../extensibility/debugger/reference/idebugprocesscreateevent2.md)

- [IDebugProcessDestroyEvent2](../../../extensibility/debugger/reference/idebugprocessdestroyevent2.md)

- [IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)

- [IDebugProgramDestroyEvent2](../../../extensibility/debugger/reference/idebugprogramdestroyevent2.md)

`riidEvent`\
からイベントの GUID。 このイベントは、このメソッドを呼び出す前に [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) にキャストされるため、この識別子を使用すると、送信されるイベントを簡単に判断できます。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="see-also"></a>関連項目
- [IDebugPortEvents2](../../../extensibility/debugger/reference/idebugportevents2.md)
- [IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md)
- [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
