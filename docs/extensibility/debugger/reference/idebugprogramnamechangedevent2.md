---
description: プログラムの名前が変更されたときに、デバッグエンジン (DE) からセッションデバッグマネージャー (SDM) に送信されます。
title: IDebugProgramNameChangedEvent2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugProgramNameChangedEvent2 interface
ms.assetid: be1f1cd5-0b2f-435c-a052-dca28a7c978d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 60fbc8aac3fd621a8f19074682bd82fbe957ed3b
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105053699"
---
# <a name="idebugprogramnamechangedevent2"></a>IDebugProgramNameChangedEvent2
プログラムの名前が変更されたときに、デバッグエンジン (DE) からセッションデバッグマネージャー (SDM) に送信されます。

## <a name="syntax"></a>Syntax

```
IDebugProgramNameChangedEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 DE は、プログラムの名前が変更されたことを報告するために、このインターフェイスを実装します。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)インターフェイスは、このインターフェイスと同じオブジェクトに実装する必要があります。 SDM は、 [QueryInterface](/cpp/atl/queryinterface) を使用して **IDebugEvent2** インターフェイスにアクセスします。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 DE は、このイベントオブジェクトを作成して送信し、プログラム名の変更を報告します。 このイベントは、デバッグ対象のプログラムにアタッチされたときに SDM によって提供される [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) callback 関数を使用して送信されます。 カスタムポート供給業者は、I インターフェイスを使用してこのイベントを送信します。

## <a name="requirements"></a>要件
 ヘッダー: Msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
