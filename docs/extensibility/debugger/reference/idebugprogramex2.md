---
title: プログラムの数2 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramEx2
helpviewer_keywords:
- IDebugProgramEx2 interface
ms.assetid: 663359ed-635a-4539-addb-0cc52f19d1bd
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b8961ea105779674aab0b67c9ad6339ce1c282f9
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80722332"
---
# <a name="idebugprogramex2"></a>IDebugProgramEx2
このインターフェイスを使用すると、セッション デバッグ マネージャー (SDM) は、プログラムにアタッチし、プログラムに関連付けられているプログラム ノードを取得します。

## <a name="syntax"></a>構文

```
IDebugProgramEx2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 カスタム ポート サプライヤーは、このインターフェイスを[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)インターフェイスと同じオブジェクトに実装し、SDM をプログラムにアタッチすると同時に、ポート サプライヤーがプログラムにアタッチされているすべてのセッションを追跡できるようにします。 カスタム ポートサプライヤーは、このインターフェイスを実装できます (選択した場合)。

## <a name="notes-for-callers"></a>発信者向けのメモ
 SDM は、インターフェイスで`IDebugProgram2`[QueryInterface](/cpp/atl/queryinterface)を呼び出して、このインターフェイスを取得して、プログラムに接続されているセッションを追跡します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に`IDebugProgramEx2`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[Attach](../../../extensibility/debugger/reference/idebugprogramex2-attach.md)|プログラムをセッションにアタッチします。|
|[GetProgramNode](../../../extensibility/debugger/reference/idebugprogramex2-getprogramnode.md)|プログラムに関連付けられているプログラム ノードを取得します。|

## <a name="remarks"></a>Remarks
 このインターフェイスは、SDM とプログラムの間でプライベートです。

## <a name="requirements"></a>必要条件
 ヘッダー: ポートプリフ.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
