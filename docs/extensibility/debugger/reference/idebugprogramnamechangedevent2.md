---
title: イベント 2 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugProgramNameChangedEvent2 interface
ms.assetid: be1f1cd5-0b2f-435c-a052-dca28a7c978d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ae58728601c3adbe6e37a00fd0694a5d71eef0b5
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80722151"
---
# <a name="idebugprogramnamechangedevent2"></a>IDebugProgramNameChangedEvent2
プログラムの名前が変更されたときに、デバッグ エンジン (DE) からセッション デバッグ マネージャー (SDM) に送信されます。

## <a name="syntax"></a>構文

```
IDebugProgramNameChangedEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 DE は、プログラムの名前が変更されたことを報告するために、このインターフェイスを実装します。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)インターフェイスは、このインターフェイスと同じオブジェクトに実装する必要があります。 SDM は[、クエリ インターフェイス](/cpp/atl/queryinterface)を使用して**IDebugEvent2**インターフェイスにアクセスします。

## <a name="notes-for-callers"></a>発信者向けのメモ
 DE は、プログラム名の変更を報告するために、このイベント オブジェクトを作成して送信します。 DE は、デバッグ中のプログラムにアタッチするときに、SDM によって提供される[IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)コールバック関数を使用して、このイベントを送信します。 カスタム ポート サプライヤーは、I インターフェイスを使用してこのイベントを送信します。

## <a name="requirements"></a>必要条件
 ヘッダー: Msdbg.h

 名前空間: を使用します。

 アセンブリ:
