---
title: IEnumDebugThreads2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugThreads2
helpviewer_keywords:
- IEnumDebugThreads2
ms.assetid: 1854f078-3b49-42c2-b65b-33e3b506fd63
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 6e3771545d4a5fe545382344d17ed5ea929999d1
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99852779"
---
# <a name="ienumdebugthreads2"></a>IEnumDebugThreads2
このインターフェイスは、現在のデバッグセッションで実行されているスレッドを列挙します。

## <a name="syntax"></a>構文

```
IEnumDebugThreads2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 デバッグエンジン (DE) は、プログラム内のスレッドの一覧を表すために、このインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 [Enumthreads](../../../extensibility/debugger/reference/idebugprocess2-enumthreads.md)を呼び出して、プロセス内で実行されているすべてのプログラム内のすべてのスレッドの一覧を表すこのインターフェイスを取得します。 [Enumthreads](../../../extensibility/debugger/reference/idebugprogram2-enumthreads.md)を呼び出して、プログラムで実行されているスレッドの一覧を表すこのインターフェイスを取得します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、のメソッドを示し `IEnumDebugThreads2` ます。

|Method|説明|
|------------|-----------------|
|[次へ](../../../extensibility/debugger/reference/ienumdebugthreads2-next.md)|列挙シーケンス内の指定された数のスレッドを取得します。|
|[Skip](../../../extensibility/debugger/reference/ienumdebugthreads2-skip.md)|列挙シーケンス内の指定された数のスレッドをスキップします。|
|[リセット](../../../extensibility/debugger/reference/ienumdebugthreads2-reset.md)|列挙シーケンスを先頭にリセットします。|
|[複製](../../../extensibility/debugger/reference/ienumdebugthreads2-clone.md)|現在の列挙状態と同じ列挙状態を含む列挙子を作成します。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugthreads2-getcount.md)|列挙子内のスレッドの数を取得します。|

## <a name="remarks"></a>解説
 通常、Visual Studio は、[ **スレッド** ] ウィンドウを更新するためにこのインターフェイスを取得し、 [Execute](../../../extensibility/debugger/reference/idebugprocess3-execute.md)、 [Continue](../../../extensibility/debugger/reference/idebugprocess3-continue.md)、および [Step](../../../extensibility/debugger/reference/idebugprocess3-step.md)を呼び出すために、リストの最初のスレッドを取得します。

## <a name="requirements"></a>要件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [EnumThreads](../../../extensibility/debugger/reference/idebugprocess2-enumthreads.md)
- [EnumThreads](../../../extensibility/debugger/reference/idebugprogram2-enumthreads.md)
- [Step](../../../extensibility/debugger/reference/idebugprocess3-step.md)
- [続行](../../../extensibility/debugger/reference/idebugprocess3-continue.md)
- [実行](../../../extensibility/debugger/reference/idebugprocess3-execute.md)
