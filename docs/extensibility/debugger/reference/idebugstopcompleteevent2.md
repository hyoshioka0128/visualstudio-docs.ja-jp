---
title: イベント 2 を停止する |マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80719446"
---
# <a name="idebugstopcompleteevent2"></a>IDebugStopCompleteEvent2

デバッグ エンジン (DE) は、プログラムが停止したときにセッションのデバッグ マネージャー (SDM) にこの省略可能なイベントを送信できます。

## <a name="syntax"></a>構文

```
IDebugStopCompleteEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項

このインターフェイスは、Visual Studio 2005 で導入されました。 以前のリリースでは非同期停止がサポートされていませんでした。

- [停止](../../../extensibility/debugger/reference/idebugengineprogram2-stop.md)は、マルチプロセスまたはマルチプログラムのシナリオで SDM によって呼び出されます。 あるプログラムが停止イベントを SDM に送信すると、SDM は他のプログラムにも停止を要求します。

Stop は、プログラムが停止したことを SDM に非同期的に通知するために使用されます。 SDM に通知することは、デバッグプログラム内でコードが実行されていない場合もあるインタプリタのデバッグ エンジンに役[立ちます。](../../../extensibility/debugger/reference/idebugengineprogram2-stop.md) デバッグ エンジンでこの非同期通知を使用する場合は[、Stop](../../../extensibility/debugger/reference/idebugengineprogram2-stop.md)`S_ASYNC_STOP`から返す必要があります。

## <a name="requirements"></a>必要条件

ヘッダー: msdbg.h

名前空間: を使用します。

アセンブリ:
