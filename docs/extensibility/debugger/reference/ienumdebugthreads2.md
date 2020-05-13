---
title: をクリックします。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugThreads2
helpviewer_keywords:
- IEnumDebugThreads2
ms.assetid: 1854f078-3b49-42c2-b65b-33e3b506fd63
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: bbbe047c08f8e91264163d028c1b40d94cde97fc
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80715088"
---
# <a name="ienumdebugthreads2"></a>IEnumDebugThreads2
このインターフェイスは、現在のデバッグ セッションで実行されているスレッドを列挙します。

## <a name="syntax"></a>構文

```
IEnumDebugThreads2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 デバッグ エンジン (DE) は、プログラム内のスレッドの一覧を表すこのインターフェイスを実装します。

## <a name="notes-for-callers"></a>発信者向けのメモ
 [EnumThreads](../../../extensibility/debugger/reference/idebugprocess2-enumthreads.md)を呼び出して、プロセスで実行されているすべてのプログラムのすべてのスレッドのリストを表すこのインターフェイスを取得します。 [EnumThreads](../../../extensibility/debugger/reference/idebugprogram2-enumthreads.md)を呼び出して、プログラムで実行されているスレッドの一覧を表すこのインターフェイスを取得します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に`IEnumDebugThreads2`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[次へ](../../../extensibility/debugger/reference/ienumdebugthreads2-next.md)|列挙体シーケンス内の指定した数のスレッドを取得します。|
|[スキップ](../../../extensibility/debugger/reference/ienumdebugthreads2-skip.md)|列挙体シーケンス内の指定した数のスレッドをスキップします。|
|[リセット](../../../extensibility/debugger/reference/ienumdebugthreads2-reset.md)|列挙シーケンスを先頭にリセットします。|
|[複製](../../../extensibility/debugger/reference/ienumdebugthreads2-clone.md)|現在の列挙状態と同じ列挙状態を含む列挙子を作成します。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugthreads2-getcount.md)|列挙子のスレッド数を取得します。|

## <a name="remarks"></a>Remarks
 Visual Studio は通常、このインターフェイスを取得して **、[スレッド**] ウィンドウを更新するほか、リストの最初のスレッドを取得して[、Execute](../../../extensibility/debugger/reference/idebugprocess3-execute.md)、 [Continue](../../../extensibility/debugger/reference/idebugprocess3-continue.md)、および[ステップ](../../../extensibility/debugger/reference/idebugprocess3-step.md)を呼び出します。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [EnumThreads](../../../extensibility/debugger/reference/idebugprocess2-enumthreads.md)
- [EnumThreads](../../../extensibility/debugger/reference/idebugprogram2-enumthreads.md)
- [Step](../../../extensibility/debugger/reference/idebugprocess3-step.md)
- [続行](../../../extensibility/debugger/reference/idebugprocess3-continue.md)
- [実行](../../../extensibility/debugger/reference/idebugprocess3-execute.md)
