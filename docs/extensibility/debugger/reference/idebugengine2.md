---
title: Iデバッグエンジン2 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine2
helpviewer_keywords:
- IDebugEngine2 interface
ms.assetid: 1f0e9ac0-6dfb-461a-976c-888d82144cdb
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5e00751db052adeefee828829ec89309a3adba4b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80730865"
---
# <a name="idebugengine2"></a>IDebugEngine2
このインターフェイスは、デバッグ エンジン (DE) を表します。 ブレークポイントの作成から例外の設定やクリアまで、デバッグ セッションのさまざまな側面を管理するために使用されます。

## <a name="syntax"></a>構文

```
IDebugEngine2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 このインターフェイスは、プログラムのデバッグを管理するカスタム DE によって実装されます。 このインターフェイスは DE によって実装される必要があります。

## <a name="notes-for-callers"></a>発信者向けのメモ
 このインターフェイスは、デバッグ セッションを管理するためにセッション デバッグ マネージャー (SDM) によって呼び出されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に`IDebugEngine2`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[EnumPrograms](../../../extensibility/debugger/reference/idebugengine2-enumprograms.md)|DE によってデバッグされているすべてのプログラムの列挙子を作成します。|
|[Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md)|DE をプログラムにアタッチします。|
|[CreatePendingBreakpoint](../../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md)|DE に保留中のブレークポイントを作成します。|
|[SetException](../../../extensibility/debugger/reference/idebugengine2-setexception.md)|DE が特定の例外を処理する方法を指定します。|
|[RemoveSetException](../../../extensibility/debugger/reference/idebugengine2-removesetexception.md)|デバッグ エンジンで処理されないように、指定した例外を削除します。|
|[RemoveAllSetExceptions](../../../extensibility/debugger/reference/idebugengine2-removeallsetexceptions.md)|IDE が特定の実行時アーキテクチャまたは言語に対して設定した例外の一覧を削除します。|
|[GetEngineID](../../../extensibility/debugger/reference/idebugengine2-getengineid.md)|DE の GUID を取得します。|
|[DestroyProgram](../../../extensibility/debugger/reference/idebugengine2-destroyprogram.md)|指定されたプログラムが異常終了し、DE がプログラムへのすべての参照をクリーンアップし、プログラム破棄イベントを送信する必要があることを DE に通知します。|
|[ContinueFromSynchronousEvent](../../../extensibility/debugger/reference/idebugengine2-continuefromsynchronousevent.md)|SDM によって呼び出され、以前に DE によって SDM に送信された同期デバッグ イベントが受信され、処理されたことを示します。|
|[SetLocale](../../../extensibility/debugger/reference/idebugengine2-setlocale.md)|DE のロケールを設定します。|
|[SetRegistryRoot](../../../extensibility/debugger/reference/idebugengine2-setregistryroot.md)|DE によって現在使用されているレジストリ ルートを設定します。|
|[SetMetric](../../../extensibility/debugger/reference/idebugengine2-setmetric.md)|メトリックを設定します。|
|[CauseBreak](../../../extensibility/debugger/reference/idebugengine2-causebreak.md)|この DE によってデバッグされているすべてのプログラムが、次にスレッドの 1 つが実行を試みるたびに実行を停止するように要求します。|

## <a name="requirements"></a>必要条件
 ヘッダー: Msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
- [GetEngine](../../../extensibility/debugger/reference/idebugenginecreateevent2-getengine.md)
