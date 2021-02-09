---
title: IDebugPortEvents2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortEvents2
helpviewer_keywords:
- IDebugPortEvents2 interface
ms.assetid: 2c017094-3ba2-4067-83f9-147df1d96bce
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ba68608e09405265940686bbb235a41c53959943
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99891190"
---
# <a name="idebugportevents2"></a>IDebugPortEvents2
このインターフェイスは、特定のポートでのプロセスとプログラムの作成と破棄をリスナーに通知します (通常、セッションデバッグマネージャー (SDM) またはデバッグエンジン)。 この情報は、ポートで実行されているプロセスとプログラムのリアルタイムビューを表示するために使用できます。

## <a name="syntax"></a>構文

```
IDebugPortEvents2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 通常、Visual Studio は、プログラムの作成と破棄に関する通知を受信するために、このインターフェイスを実装します。 デバッグエンジンは、このインターフェイスを実装して、このようなポートイベントをリッスンすることもできます。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 インターフェイスに対して、すべての [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md) インターフェイスのクエリを実行でき <xref:System.Runtime.InteropServices.ComTypes.IConnectionPointContainer> ます。 次に、インターフェイスを <xref:System.Runtime.InteropServices.ComTypes.IConnectionPointContainer.FindConnectionPoint%2A> 取得するために、のメソッド `IDebugPortEvents2` がインターフェイスで呼び出され <xref:System.Runtime.InteropServices.ComTypes.IConnectionPointContainer> <xref:System.Runtime.InteropServices.ComTypes.IConnectionPoint> ます。 最後に、 <xref:System.Runtime.InteropServices.ComTypes.IConnectionPoint.Advise%2A> <xref:System.Runtime.InteropServices.ComTypes.IConnectionPoint> [イベント](../../../extensibility/debugger/reference/idebugportevents2-event.md) メソッドを介してイベントを送信するために、インターフェイスのメソッドが呼び出されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表は、のメソッドを示して `IDebugPortEvents2` います。

|Method|説明|
|------------|-----------------|
|[Event](../../../extensibility/debugger/reference/idebugportevents2-event.md)|ポートでのプロセスとプログラムの作成と破棄を説明するイベントを送信します。|

## <a name="remarks"></a>解説
 `IDebugPortEvents2` は、既にデバッグされているプロセスで実行されるプログラムをデバッグするために SDM によっても使用されます。

 ポートイベントは、このインターフェイスによって SDM に渡されます。

## <a name="requirements"></a>要件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)
