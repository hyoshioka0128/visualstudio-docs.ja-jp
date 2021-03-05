---
description: このインターフェイスは、デバッグエンジン (DE) を表します。
title: IDebugEngine2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine2
helpviewer_keywords:
- IDebugEngine2 interface
ms.assetid: 1f0e9ac0-6dfb-461a-976c-888d82144cdb
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ce76ccdc444dafc4b6b8ee6afb3c9ded8adcf3d0
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102153834"
---
# <a name="idebugengine2"></a>IDebugEngine2
このインターフェイスは、デバッグエンジン (DE) を表します。 ブレークポイントの作成から例外の設定および消去まで、デバッグセッションのさまざまな側面を管理するために使用されます。

## <a name="syntax"></a>構文

```
IDebugEngine2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 このインターフェイスは、プログラムのデバッグを管理するために、カスタムの DE によって実装されます。 このインターフェイスは、DE によって実装される必要があります。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 このインターフェイスは、例外の管理、ブレークポイントの作成、DE によって送信された同期イベントへの応答など、デバッグセッションを管理するために、セッションデバッグマネージャー (SDM) によって呼び出されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、のメソッドを示し `IDebugEngine2` ます。

|メソッド|説明|
|------------|-----------------|
|[EnumPrograms](../../../extensibility/debugger/reference/idebugengine2-enumprograms.md)|DE によってデバッグされているすべてのプログラムの列挙子を作成します。|
|[[アタッチ]](../../../extensibility/debugger/reference/idebugengine2-attach.md)|プログラムに DE をアタッチします。|
|[CreatePendingBreakpoint](../../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md)|保留中のブレークポイントを DE に作成します。|
|[SetException](../../../extensibility/debugger/reference/idebugengine2-setexception.md)|DE が特定の例外を処理する方法を指定します。|
|[RemoveSetException](../../../extensibility/debugger/reference/idebugengine2-removesetexception.md)|指定された例外を削除して、デバッグエンジンによって処理されないようにします。|
|[RemoveAllSetExceptions](../../../extensibility/debugger/reference/idebugengine2-removeallsetexceptions.md)|IDE が特定のランタイムアーキテクチャまたは言語に対して設定した例外の一覧を削除します。|
|[GetEngineID](../../../extensibility/debugger/reference/idebugengine2-getengineid.md)|DE の GUID を取得します。|
|[DestroyProgram](../../../extensibility/debugger/reference/idebugengine2-destroyprogram.md)|指定されたプログラムが atypically に終了したこと、および DE がプログラムへのすべての参照をクリーンアップしてプログラム破棄イベントを送信する必要があることを通知します。|
|[ContinueFromSynchronousEvent](../../../extensibility/debugger/reference/idebugengine2-continuefromsynchronousevent.md)|Sdm によって以前に送信された同期デバッグイベントが受信および処理されたことを示すために、SDM によって呼び出されます。|
|[SetLocale](../../../extensibility/debugger/reference/idebugengine2-setlocale.md)|DE のロケールを設定します。|
|[SetRegistryRoot](../../../extensibility/debugger/reference/idebugengine2-setregistryroot.md)|DE によって現在使用されているレジストリルートを設定します。|
|[SetMetric](../../../extensibility/debugger/reference/idebugengine2-setmetric.md)|メトリックを設定します。|
|[CauseBreak](../../../extensibility/debugger/reference/idebugengine2-causebreak.md)|この DE によってデバッグされているすべてのプログラムは、そのスレッドの1つが次に実行を試みたときに実行を停止するよう要求します。|

## <a name="requirements"></a>必要条件
 ヘッダー: Msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
- [GetEngine](../../../extensibility/debugger/reference/idebugenginecreateevent2-getengine.md)
