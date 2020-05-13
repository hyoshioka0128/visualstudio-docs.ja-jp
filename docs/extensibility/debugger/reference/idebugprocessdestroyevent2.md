---
title: イベントの実行マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcessDestroyEvent2
helpviewer_keywords:
- IDebugProcessDestroyEvent2
ms.assetid: 1b8e0528-95bc-48fa-9653-2cea66c8dc3a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7d7c93c1e5811ec3aed5d44f3c306de1c09cced9
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80723450"
---
# <a name="idebugprocessdestroyevent2"></a>IDebugProcessDestroyEvent2
このインターフェースは、プロセスが終了するか、非定型で終了するか、またはデタッチされたときに送信されます。

## <a name="syntax"></a>構文

```
IDebugProcessDestroyEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 デバッグ エンジン (DE) またはカスタム ポート サプライヤーは、プロセスが終了したことを報告するこのインターフェイスを実装します。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)インターフェイスは、このインターフェイスと同じオブジェクトに実装する必要があります。 SDM は[、インターフェイス](/cpp/atl/queryinterface)にアクセスするのに`IDebugEvent2`クエリ インターフェイスを使用します。

## <a name="notes-for-callers"></a>発信者向けのメモ
 DE またはカスタム ポート サプライヤーは、プロセスの終了を報告するために、このイベント オブジェクトを作成して送信します。 DE は、デバッグ中のプログラムにアタッチされるときに、SDM によって提供される[IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)コールバック関数を使用して、このイベントを送信します。 カスタム ポート サプライヤーは[、IDebugPortEvents2](../../../extensibility/debugger/reference/idebugportevents2.md)インターフェイスを使用してこのイベントを送信します。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [IDebugPortEvents2](../../../extensibility/debugger/reference/idebugportevents2.md)
