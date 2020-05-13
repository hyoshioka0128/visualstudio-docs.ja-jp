---
title: イベントを作成するイベント 2 を作成するマイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80723529"
---
# <a name="idebugprocesscreateevent2"></a>IDebugProcessCreateEvent2
このインターフェイスは、プロセスが起動されたときに送信されます。

## <a name="syntax"></a>構文

```
IDebugProcessCreateEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 デバッグ エンジン (DE) またはカスタム ポート サプライヤーは、プロセスが作成されたことを報告するこのインターフェイスを実装します。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)インターフェイスは、このインターフェイスと同じオブジェクトに実装する必要があります。 SDM は[、インターフェイス](/cpp/atl/queryinterface)にアクセスするのに`IDebugEvent2`クエリ インターフェイスを使用します。

## <a name="notes-for-callers"></a>発信者向けのメモ
 DE またはカスタム ポート サプライヤーは、プロセスの作成を報告するために、このイベント オブジェクトを作成して送信します。 DE は、デバッグ中のプログラムにアタッチされるときに、SDM によって提供される[IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)コールバック関数を使用して、このイベントを送信します。 カスタム ポート サプライヤーは[、IDebugPortEvents2](../../../extensibility/debugger/reference/idebugportevents2.md)インターフェイスを使用してこのイベントを送信します。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [IDebugPortEvents2](../../../extensibility/debugger/reference/idebugportevents2.md)
