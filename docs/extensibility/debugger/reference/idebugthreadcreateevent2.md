---
description: このインターフェイスは、デバッグ対象のプログラムでスレッドが作成されるときに、デバッグエンジン (DE) によってセッションデバッグマネージャー (SDM) に送信されます。
title: IDebugThreadCreateEvent2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugThreadCreateEvent2
helpviewer_keywords:
- IDebugThreadCreateEvent2
ms.assetid: aee34a14-4f9c-4ad3-845f-c96ee938cefd
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 054163732d0ca4a2b818acf948da0490ebe0f8e6
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105086964"
---
# <a name="idebugthreadcreateevent2"></a>IDebugThreadCreateEvent2
このインターフェイスは、デバッグ対象のプログラムでスレッドが作成されるときに、デバッグエンジン (DE) によってセッションデバッグマネージャー (SDM) に送信されます。

## <a name="syntax"></a>Syntax

```
IDebugThreadCreateEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 DE は、スレッドが作成されたことを報告するために、このインターフェイスを実装します。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)インターフェイスは、このインターフェイスと同じオブジェクトに実装する必要があります。 SDM は、 [QueryInterface](/cpp/atl/queryinterface) を使用してインターフェイスにアクセスし `IDebugEvent2` ます。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 DE は、スレッドが作成されたことを報告するために、このイベントオブジェクトを作成して送信します。 イベントは、デバッグ対象のプログラムにアタッチされているときに、SDM によって提供される [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) callback 関数を使用して送信されます。

## <a name="requirements"></a>要件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>こちらもご覧ください
- [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
