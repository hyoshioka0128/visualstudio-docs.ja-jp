---
description: このインターフェイスを使用すると、セッションデバッグマネージャー (SDM) をプログラムにアタッチし、プログラムに関連付けられたプログラムノードを取得できます。
title: IDebugProgramEx2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramEx2
helpviewer_keywords:
- IDebugProgramEx2 interface
ms.assetid: 663359ed-635a-4539-addb-0cc52f19d1bd
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e39a469d04ac14f3ed36366d035bf4ca01a9d2ef
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105087328"
---
# <a name="idebugprogramex2"></a>IDebugProgramEx2
このインターフェイスを使用すると、セッションデバッグマネージャー (SDM) をプログラムにアタッチし、プログラムに関連付けられたプログラムノードを取得できます。

## <a name="syntax"></a>Syntax

```
IDebugProgramEx2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 カスタムポートサプライヤーは、 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) インターフェイスと同じオブジェクトにこのインターフェイスを実装して、SDM がプログラムにアタッチされるようにします。同時に、ポートサプライヤーがプログラムにアタッチされているすべてのセッションを追跡できるようにします。 カスタムポート供給業者は、選択した場合、このインターフェイスを実装できます。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 SDM は、インターフェイスの [QueryInterface](/cpp/atl/queryinterface) を呼び出して、 `IDebugProgram2` プログラムにアタッチされたセッションを追跡するために、このインターフェイスを取得します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、のメソッドを示し `IDebugProgramEx2` ます。

|メソッド|説明|
|------------|-----------------|
|[[アタッチ]](../../../extensibility/debugger/reference/idebugprogramex2-attach.md)|セッションにプログラムをアタッチします。|
|[GetProgramNode](../../../extensibility/debugger/reference/idebugprogramex2-getprogramnode.md)|プログラムに関連付けられているプログラムノードを取得します。|

## <a name="remarks"></a>注釈
 このインターフェイスは、SDM とプログラムの間でプライベートです。

## <a name="requirements"></a>要件
 ヘッダー: Portpriv. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>こちらもご覧ください
- [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
