---
title: イベントの実行マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBreakEvent2
helpviewer_keywords:
- IDebugBreakEvent2 interface
ms.assetid: 57dfdbc2-4e68-4dbf-9579-006cd6fb1c62
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1af6ce13de529fef5e16b3bc1be7053f0e1347b6
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80735392"
---
# <a name="idebugbreakevent2"></a>IDebugBreakEvent2
このインターフェイスは、セッション デバッグ マネージャー (SDM) に非同期中断が正常に完了したことを通知します。

## <a name="syntax"></a>構文

```
IDebugBreakEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 DE は、プログラムのユーザーの中断をサポートするために、このインターフェイスを実装します。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)インターフェイスは、このインターフェイスと同じオブジェクトに実装する必要があります (SDM は、インターフェイス`IDebugEvent2`にアクセスするのに[QueryInterface](/cpp/atl/queryinterface)を使用します)。

## <a name="notes-for-callers"></a>発信者向けのメモ
 SDM は、デバッグ中のプログラムを一時停止するようにユーザーが要求したときに[CauseBreak](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md)を呼び出します。 プログラムが正常に一時停止されると、DE はイベントを送信`IDebugBreakEvent2`します。 このイベントは、デバッグ中のプログラムにアタッチされたときに、SDM によって提供される[IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)コールバック関数を使用して送信されます。

## <a name="remarks"></a>Remarks
 たとえば、ユーザーは、[**デバッグ**] メニューの **[すべて中断**] を選択して、無限ループを実行しているプログラムから抜け出すことができます。 SDM は[、CauseBreak](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md)を呼び出して停止するようにプログラムに指示します。 DE は`IDebugBreakEvent2`、プログラムが最終的に停止したときに送信します。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [CauseBreak](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
