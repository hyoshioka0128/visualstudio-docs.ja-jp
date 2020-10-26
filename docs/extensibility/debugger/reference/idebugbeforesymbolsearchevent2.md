---
title: IDebugBeforeSymbolSearchEvent2 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80736115"
---
# <a name="idebugbeforesymbolsearchevent2"></a>IDebugBeforeSymbolSearchEvent2
デバッグエンジン (DE) は、シンボルの読み込み中にステータスバーメッセージを設定するために、このインターフェイスをセッションデバッグマネージャー (SDM) に送信します。

## <a name="syntax"></a>構文

```
IDebugBeforeSymbolSearchEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 シンボルの読み込み中にステータスバーメッセージを設定する必要がある場合、DE はこのインターフェイスを実装します。 このインターフェイスは、またはで動作するスクリプトインタープリターの一部であるデバッグエンジンによってのみ実装されます。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)インターフェイスは、このインターフェイスと同じオブジェクトに実装する必要があります (SDM は**QueryInterface**を使用して**IDebugEvent2**インターフェイスにアクセスします)。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 シンボルの読み込み中にステータスバーメッセージを設定する必要がある場合、DE はこのイベントオブジェクトを作成して送信します。 イベントは、デバッグ対象のプログラムにアタッチされるときに、SDM によって提供される [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) callback 関数を使用して送信されます。

## <a name="methods"></a>メソッド
 次の表に、のメソッドを示し `IDebugBeforeSymbolSearchEvent2` ます。

|Method|説明|
|------------|-----------------|
|[GetModuleName](../../../extensibility/debugger/reference/idebugbeforesymbolsearchevent2-getmodulename.md)|現在デバッグされているモジュールの名前を取得します。|

## <a name="requirements"></a>必要条件
 ヘッダー: Msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
