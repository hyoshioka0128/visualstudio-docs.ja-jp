---
title: IDebugBreakEvent2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBreakEvent2
helpviewer_keywords:
- IDebugBreakEvent2 interface
ms.assetid: 57dfdbc2-4e68-4dbf-9579-006cd6fb1c62
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 61fb53c1fc83f06c200b50b5fcf55f950a00ead6
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99943435"
---
# <a name="idebugbreakevent2"></a>IDebugBreakEvent2
このインターフェイスは、非同期中断が正常に完了したことをセッションデバッグマネージャー (SDM) に通知します。

## <a name="syntax"></a>構文

```
IDebugBreakEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 DE は、プログラムでのユーザーの中断をサポートするために、このインターフェイスを実装します。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)インターフェイスは、このインターフェイスと同じオブジェクトに実装する必要があります (SDM は[QueryInterface](/cpp/atl/queryinterface)を使用してインターフェイスにアクセスし `IDebugEvent2` ます)。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 ユーザーがデバッグ中のプログラムの一時停止を要求した場合、SDM は [Causebreak](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md) を呼び出します。 プログラムが正常に一時停止されると、DE がイベントを送信し `IDebugBreakEvent2` ます。 このイベントは、デバッグ対象のプログラムにアタッチされるときに、SDM によって提供される [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) callback 関数を使用して送信されます。

## <a name="remarks"></a>解説
 たとえば、ユーザーは、[**デバッグ**] メニューの [**すべて中断**] を選択して、無限ループを実行しているプログラムを中断できます。 SDM は、 [Causebreak](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md)を呼び出すことにより、プログラムを停止するように指示します。 `IDebugBreakEvent2`プログラムが最後に停止したときに、DE によって送信されます。

## <a name="requirements"></a>要件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [CauseBreak](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
