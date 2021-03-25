---
description: このインターフェイスは、現在のコードの場所で停止するかどうかをセッションデバッグマネージャー (SDM) に要求するために使用されます。
title: IDebugCanStopEvent2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCanStopEvent2
helpviewer_keywords:
- IDebugBreakpointRequest2 interface
ms.assetid: 784bd5b1-4a3f-4455-b313-c4c9a82555a5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e73d881b1aef09d13d7b7138348d5198c8322694
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105085014"
---
# <a name="idebugcanstopevent2"></a>IDebugCanStopEvent2
このインターフェイスは、現在のコードの場所で停止するかどうかをセッションデバッグマネージャー (SDM) に要求するために使用されます。

## <a name="syntax"></a>Syntax

```
IDebugCanStopEvent2 : IUknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 デバッグエンジン (DE) は、ソースコードのステップ実行をサポートするために、このインターフェイスを実装します。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)インターフェイスは、このインターフェイスと同じオブジェクトに実装する必要があります (SDM は[QueryInterface](/cpp/atl/queryinterface)を使用してインターフェイスにアクセスし `IDebugEvent2` ます)。

 このインターフェイスの実装では、SDM の [Canstop](../../../extensibility/debugger/reference/idebugcanstopevent2-canstop.md) の呼び出しがデバッグエンジンに伝達される必要があります。 たとえば、これは、デバッグエンジンのメッセージ処理スレッドにポストされたメッセージを使用して実行できます。また、このインターフェイスを実装しているオブジェクトは、デバッグエンジンへの参照を保持し、に渡されたフラグを使用してデバッグエンジンにコールバックすることもでき `IDebugCanStopEvent2::CanStop` ます。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 De は、実行を継続するように求められ、DE がコードをステップ実行するたびに、このメソッドを送信できます。 このイベントは、デバッグ対象のプログラムにアタッチされるときに、SDM によって提供される [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) callback 関数を使用して送信されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、のメソッドを示し `IDebugCanStopEvent2` ます。

|メソッド|説明|
|------------|-----------------|
|[GetReason](../../../extensibility/debugger/reference/idebugcanstopevent2-getreason.md)|このイベントの理由を取得します。|
|[CanStop](../../../extensibility/debugger/reference/idebugcanstopevent2-canstop.md)|デバッグ中のプログラムをこのイベントの場所で停止するか (停止の理由を説明するイベントを送信する)、または実行を継続するかを指定します。|
|[GetDocumentContext](../../../extensibility/debugger/reference/idebugcanstopevent2-getdocumentcontext.md)|このイベントの場所を記述するドキュメントコンテキストを取得します。|
|[GetCodeContext](../../../extensibility/debugger/reference/idebugcanstopevent2-getcodecontext.md)|このイベントの場所を記述するコードコンテキストを取得します。|

## <a name="remarks"></a>注釈
 ユーザーが関数にステップインし、逆にデバッグ情報がない場合やデバッグ情報が存在するが、その場所にソースコードを表示できるかどうかが不明である場合、de はこのインターフェイスを送信します。

## <a name="requirements"></a>要件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>こちらもご覧ください
- [IDebugStepCompleteEvent2](../../../extensibility/debugger/reference/idebugstepcompleteevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
