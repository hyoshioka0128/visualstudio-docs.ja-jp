---
title: をクリックして、イベントを終了します。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCanStopEvent2
helpviewer_keywords:
- IDebugBreakpointRequest2 interface
ms.assetid: 784bd5b1-4a3f-4455-b313-c4c9a82555a5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f0a3710756f02d7c622be94bab6c3056fb051827
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80734513"
---
# <a name="idebugcanstopevent2"></a>IDebugCanStopEvent2
このインターフェイスは、セッションデバッグ マネージャー (SDM) が現在のコードの場所で停止するかどうかを確認するために使用されます。

## <a name="syntax"></a>構文

```
IDebugCanStopEvent2 : IUknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 デバッグ エンジン (DE) は、ソース コードのステップ実行をサポートするには、このインターフェイスを実装します。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)インターフェイスは、このインターフェイスと同じオブジェクトに実装する必要があります (SDM は、インターフェイス`IDebugEvent2`にアクセスするのに[QueryInterface](/cpp/atl/queryinterface)を使用します)。

 このインターフェイスの実装は、SDM の[CanStop](../../../extensibility/debugger/reference/idebugcanstopevent2-canstop.md)の呼び出しをデバッグ エンジンに通信する必要があります。 たとえば、この処理は、デバッグ エンジンのメッセージ処理スレッドにポストされたメッセージ、またはこのインターフェイスを実装するオブジェクトが、デバッグ エンジンへの参照を保持し、フラグが渡されたデバッグ エンジンにコールバックすることで行うことができます`IDebugCanStopEvent2::CanStop`。

## <a name="notes-for-callers"></a>発信者向けのメモ
 DE は、実行を続行するように求め、DE がコードをステップ実行するたびにこのメソッドを送信できます。 このイベントは、デバッグ中のプログラムにアタッチされたときに、SDM によって提供される[IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)コールバック関数を使用して送信されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に`IDebugCanStopEvent2`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[GetReason](../../../extensibility/debugger/reference/idebugcanstopevent2-getreason.md)|このイベントの理由を取得します。|
|[CanStop](../../../extensibility/debugger/reference/idebugcanstopevent2-canstop.md)|デバッグ中のプログラムがこのイベントの場所で停止するか (および停止の理由を説明するイベントを送信するか) または実行を継続するかを指定します。|
|[GetDocumentContext](../../../extensibility/debugger/reference/idebugcanstopevent2-getdocumentcontext.md)|このイベントの場所を記述するドキュメント コンテキストを取得します。|
|[GetCodeContext](../../../extensibility/debugger/reference/idebugcanstopevent2-getcodecontext.md)|このイベントの場所を記述するコード コンテキストを取得します。|

## <a name="remarks"></a>Remarks
 ユーザーが関数にステップ インし、DE がデバッグ情報を見つけていない場合、またはデバッグ情報が存在するが、DE はソース コードがその場所に表示できるかどうかわからない場合、DE はこのインターフェイスを送信します。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [IDebugStepCompleteEvent2](../../../extensibility/debugger/reference/idebugstepcompleteevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
