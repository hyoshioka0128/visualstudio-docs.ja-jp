---
title: IDebugStopCompleteEvent2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugStopCompleteEvent2 interface
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: da3eb33d76f55310e6428a34dd09cabbc271aa68
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80719446"
---
# <a name="idebugstopcompleteevent2"></a>IDebugStopCompleteEvent2

デバッグエンジン (DE) は、プログラムが停止したときに、この省略可能なイベントをセッションデバッグマネージャー (SDM) に送信できます。

## <a name="syntax"></a>構文

```
IDebugStopCompleteEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意

このインターフェイスは、Visual Studio 2005 で導入されました。 以前のリリースでは、非同期停止はサポートされていませんでした。

- [Stop](../../../extensibility/debugger/reference/idebugengineprogram2-stop.md) は、マルチプロセスまたは複数プログラムのシナリオで SDM によって呼び出されます。 あるプログラムが SDM に停止イベントを送信すると、SDM は他のプログラムも停止するように要求します。

Stop は、プログラムが停止したことを SDM に非同期に通知するために使用されます。 SDM の通知はインタープリターデバッグエンジンに役立ちます。これは、デバッグ対象のプログラム内でコードが実行されていない場合があります。そのため、 [停止](../../../extensibility/debugger/reference/idebugengineprogram2-stop.md) を同期的に完了することはできません。 デバッグエンジンがこの非同期通知を使用する場合は、Stop から戻る必要があり `S_ASYNC_STOP` ます。 [Stop](../../../extensibility/debugger/reference/idebugengineprogram2-stop.md)

## <a name="requirements"></a>必要条件

ヘッダー: msdbg. h

名前空間: VisualStudio。

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
