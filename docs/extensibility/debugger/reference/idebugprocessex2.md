---
description: このインターフェイスを使用すると、セッションデバッグマネージャー (SDM) は、プロセスにアタッチするプロセスまたはプロセスからデタッチするプロセスを通知できます。
title: IDebugProcessEx2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcessEx2
helpviewer_keywords:
- IDebugProcessEx2 interface
ms.assetid: 44e309ba-1d6f-499b-aa7e-9b34858a6d57
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 1bd22a779cd0a474b5df03d2315402dbe1a25239
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105081517"
---
# <a name="idebugprocessex2"></a>IDebugProcessEx2
このインターフェイスを使用すると、セッションデバッグマネージャー (SDM) は、プロセスにアタッチするプロセスまたはプロセスからデタッチするプロセスを通知できます。

## <a name="syntax"></a>Syntax

```
IDebugProcessEx2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 カスタムポートサプライヤーは、次の目的で、 [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md) インターフェイスと同じオブジェクトにこのインターフェイスを実装します。

- プロセスに接続されているセッションの追跡をサポートする

- 複数のデバッグエンジン間での自動アタッチをサポートする

  カスタムポート供給業者は、選択した場合、このインターフェイスを実装できます。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項

- SDM は、インターフェイスの [QueryInterface](/cpp/atl/queryinterface) を呼び出して、 `IDebugProcess2` このインターフェイスを取得します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、のメソッドを示し `IDebugProcessEx2` ます。

|メソッド|説明|
|------------|-----------------|
|[[アタッチ]](../../../extensibility/debugger/reference/idebugprocessex2-attach.md)|セッションがプロセスをデバッグ中であることをプロセスに通知します。|
|[[デタッチ]](../../../extensibility/debugger/reference/idebugprocessex2-detach.md)|セッションがプロセスのデバッグを終了したことをプロセスに通知します。|
|[AddImplicitProgramNodes](../../../extensibility/debugger/reference/idebugprocessex2-addimplicitprogramnodes.md)|デバッグエンジンの一覧のプログラムノードを追加します。|

## <a name="remarks"></a>注釈
 このインターフェイスは、SDM とプロセスとの間でプライベートです。

## <a name="requirements"></a>要件
 ヘッダー: Portpriv. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>こちらもご覧ください
- [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
