---
title: IDebug 前のシンボルイベント2 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugBeforeSymbolSearchEvent2 interface
ms.assetid: 679fd7b1-765a-41a8-a046-63240c09a499
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9d6f3f78e165ba2f4453131b7b459e3061243ff6
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80736115"
---
# <a name="idebugbeforesymbolsearchevent2"></a>IDebugBeforeSymbolSearchEvent2
デバッグ エンジン (DE) は、シンボルの読み込み中にステータス バー メッセージを設定するセッション デバッグ マネージャー (SDM) にこのインターフェイスを送信します。

## <a name="syntax"></a>構文

```
IDebugBeforeSymbolSearchEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 デは、シンボルの読み込み中にステータス バー メッセージを設定する必要がある場合に、このインターフェイスを実装します。 このインターフェイスは、スクリプト インタープリタの一部または一部であるデバッグ エンジンによってのみ実装されます。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)インターフェイスは、このインターフェイスと同じオブジェクトに実装する必要があります (SDM は **、IDebugEvent2**インターフェイスにアクセスするのに**はクエリ インターフェイス**を使用します)。

## <a name="notes-for-callers"></a>発信者向けのメモ
 デは、シンボルの読み込み中にステータス バー メッセージを設定する必要がある場合に、このイベント オブジェクトを作成して送信します。 イベントは、デバッグ中のプログラムにアタッチされたときに、SDM によって提供される[IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)コールバック関数を使用して送信されます。

## <a name="methods"></a>メソッド
 次の表に`IDebugBeforeSymbolSearchEvent2`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[GetModuleName](../../../extensibility/debugger/reference/idebugbeforesymbolsearchevent2-getmodulename.md)|現在デバッグ中のモジュールの名前を取得します。|

## <a name="requirements"></a>必要条件
 ヘッダー: Msdbg.h

 名前空間: を使用します。

 アセンブリ:
