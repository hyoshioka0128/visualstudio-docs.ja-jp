---
title: イベント |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortEvents2::Event
helpviewer_keywords:
- IDebugPortEvents2::Event
ms.assetid: 5cc813f7-04a1-4462-9ea7-fbddcf0e0143
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 931be468f6321250481aec79688f7f326abcfcac
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80725242"
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
[in]イベントが発生したデバッグ サーバー (のインスタンスごとに 1 つ)[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]を表す[IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md)オブジェクト。

`pPort`\
[in]イベントが発生したポートを表す[IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)オブジェクト。

`pProcess`\
[in]イベントが発生したプロセスを表す[IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)オブジェクト。

`pProgram`\
[in]イベントが発生したプログラムを表す[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)オブジェクト。

`pEvent`\
[in]イベントを識別する[IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)オブジェクト。 考えられるイベントは次のとおりです。

- [IDebugProcessCreateEvent2](../../../extensibility/debugger/reference/idebugprocesscreateevent2.md)

- [IDebugProcessDestroyEvent2](../../../extensibility/debugger/reference/idebugprocessdestroyevent2.md)

- [IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)

- [IDebugProgramDestroyEvent2](../../../extensibility/debugger/reference/idebugprogramdestroyevent2.md)

`riidEvent`\
[in]イベントの GUID。 このメソッドを呼び出す前にイベントが[IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)にキャストされるため、この識別子を使用すると、送信されるイベントを簡単に判断できます。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDebugPortEvents2](../../../extensibility/debugger/reference/idebugportevents2.md)
- [IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md)
- [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
