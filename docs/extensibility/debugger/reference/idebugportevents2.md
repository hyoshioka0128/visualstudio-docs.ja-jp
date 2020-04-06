---
title: をクリックして、ポートイベント 2 を実行する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortEvents2
helpviewer_keywords:
- IDebugPortEvents2 interface
ms.assetid: 2c017094-3ba2-4067-83f9-147df1d96bce
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9c611eb531bdabb633b11ac2e8ca2d0d11f52005
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80725176"
---
# <a name="idebugportevents2"></a>IDebugPortEvents2
このインターフェイスは、特定のポートでのプロセスとプログラムの作成と破棄のリスナー (通常はセッション デバッグ マネージャー [SDM] またはデバッグ エンジン) に通知します。 この情報を使用して、ポートで実行されているプロセスとプログラムをリアルタイムで表示できます。

## <a name="syntax"></a>構文

```
IDebugPortEvents2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 Visual Studio は通常、プログラムの作成と破棄に関する通知を受信するために、このインターフェイスを実装します。 デバッグ エンジンは、このようなポート イベントをリッスンするこのインターフェイスを実装することもできます。

## <a name="notes-for-callers"></a>発信者向けのメモ
 すべての[IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)インターフェイスを照会<xref:System.Runtime.InteropServices.ComTypes.IConnectionPointContainer>できます。 その後<xref:System.Runtime.InteropServices.ComTypes.IConnectionPointContainer.FindConnectionPoint%2A>、`IDebugPortEvents2`<xref:System.Runtime.InteropServices.ComTypes.IConnectionPointContainer>インターフェイスを取得するために、インターフェイスでのメソッド<xref:System.Runtime.InteropServices.ComTypes.IConnectionPoint>が呼び出されます。 最後に<xref:System.Runtime.InteropServices.ComTypes.IConnectionPoint.Advise%2A>、<xref:System.Runtime.InteropServices.ComTypes.IConnectionPoint>インターフェイスのメソッドが呼び出され[、Event](../../../extensibility/debugger/reference/idebugportevents2-event.md)メソッドを介してイベントが送信されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、 の`IDebugPortEvents2`方法を示します。

|Method|説明|
|------------|-----------------|
|[Event](../../../extensibility/debugger/reference/idebugportevents2-event.md)|ポート上のプロセスとプログラムの作成と破棄を記述するイベントを送信します。|

## <a name="remarks"></a>Remarks
 `IDebugPortEvents2`は、すでにデバッグ中のプロセスで実行されるプログラムをデバッグするために SDM によっても使用されます。

 ポート イベントは、このインターフェイスによって SDM に渡されます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)
