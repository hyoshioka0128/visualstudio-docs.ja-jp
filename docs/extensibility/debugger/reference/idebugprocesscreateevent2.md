---
title: IDebugProcessCreateEvent2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcessCreateEvent2
helpviewer_keywords:
- IDebugProcessCreateEvent2
ms.assetid: c660439d-8b23-4dbb-923e-ebb5e1d7edf5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: cfc9b0bbdebde01af48ab1436dbfd17ac0c3241b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80723529"
---
# <a name="idebugprocesscreateevent2"></a>IDebugProcessCreateEvent2
このインターフェイスは、プロセスが起動されたときに送信されます。

## <a name="syntax"></a>構文

```
IDebugProcessCreateEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 デバッグエンジン (DE) またはカスタムポート供給業者は、このインターフェイスを実装して、プロセスが作成されたことを報告します。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)インターフェイスは、このインターフェイスと同じオブジェクトに実装する必要があります。 SDM は、 [QueryInterface](/cpp/atl/queryinterface) を使用してインターフェイスにアクセスし `IDebugEvent2` ます。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 DE またはカスタムポートサプライヤーがこのイベントオブジェクトを作成し、送信して、プロセスの作成を報告します。 このイベントは、デバッグ対象のプログラムにアタッチされているときに、SDM によって提供される [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) callback 関数を使用して送信されます。 カスタムポート供給業者は、 [IDebugPortEvents2](../../../extensibility/debugger/reference/idebugportevents2.md) インターフェイスを使用してこのイベントを送信します。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [IDebugPortEvents2](../../../extensibility/debugger/reference/idebugportevents2.md)
