---
title: をクリックして作業を開始する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcessEx2
helpviewer_keywords:
- IDebugProcessEx2 interface
ms.assetid: 44e309ba-1d6f-499b-aa7e-9b34858a6d57
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 743dd1aa72d9b8db6b848618c8a2ad6c8c8ecaaf
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80723331"
---
# <a name="idebugprocessex2"></a>IDebugProcessEx2
このインターフェイスを使用すると、セッション デバッグ マネージャー (SDM) は、アタッチまたはプロセスから切り離されているプロセスを通知します。

## <a name="syntax"></a>構文

```
IDebugProcessEx2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 カスタム ポート サプライヤーは[、IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)インターフェイスと同じオブジェクトにこのインターフェイスを実装して、次の操作を行います。

- プロセスに接続されたセッションの追跡をサポート

- 複数のデバッグ エンジンで自動アタッチをサポート

  カスタム ポートサプライヤーは、このインターフェイスを実装できます (選択した場合)。

## <a name="notes-for-callers"></a>発信者向けのメモ

- SDM は[QueryInterface](/cpp/atl/queryinterface)、このインターフェイスを`IDebugProcess2`取得するインターフェイスでクエリ インターフェイスを呼び出します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に`IDebugProcessEx2`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[Attach](../../../extensibility/debugger/reference/idebugprocessex2-attach.md)|セッションがプロセスをデバッグしていることをプロセスに通知します。|
|[Detach](../../../extensibility/debugger/reference/idebugprocessex2-detach.md)|セッションがプロセスをデバッグしなくなったことをプロセスに通知します。|
|[AddImplicitProgramNodes](../../../extensibility/debugger/reference/idebugprocessex2-addimplicitprogramnodes.md)|デバッグ エンジンの一覧のプログラム ノードを追加します。|

## <a name="remarks"></a>Remarks
 このインターフェイスは、SDM とプロセスの間でプライベートです。

## <a name="requirements"></a>必要条件
 ヘッダー: ポートプリフ.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
