---
description: このインターフェイスは、デバッグ中のプログラムを実行しているコンピューターのアドレス空間内の位置を表します。
title: IDebugMemoryContext2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMemoryContext2
helpviewer_keywords:
- IDebugMemoryContext2 interface
ms.assetid: 3a544c8b-11dc-46bb-8549-261e4ac5bbc4
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 5a967c992fc55065c50dbbe173495e7c1199df59
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105058483"
---
# <a name="idebugmemorycontext2"></a>IDebugMemoryContext2
このインターフェイスは、デバッグ中のプログラムを実行しているコンピューターのアドレス空間内の位置を表します。

## <a name="syntax"></a>Syntax

```
IDebugMemoryContext2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 デバッグエンジン (DE) は、メモリ内のアドレスを表すために、このインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 [Getmemorycontext](../../../extensibility/debugger/reference/idebugproperty2-getmemorycontext.md)または[getmemorycontext](../../../extensibility/debugger/reference/idebugreference2-getmemorycontext.md)を呼び出すと、このインターフェイスが返されます。 また、 [加算](../../../extensibility/debugger/reference/idebugmemorycontext2-add.md) および [減算](../../../extensibility/debugger/reference/idebugmemorycontext2-subtract.md) の呼び出しは、適切な算術演算が適用された後に、このインターフェイスの新しいコピーを返します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、のメソッドを示し `IDebugMemoryContext2` ます。

|メソッド|説明|
|------------|-----------------|
|[GetName](../../../extensibility/debugger/reference/idebugmemorycontext2-getname.md)|このコンテキストのユーザーが指定可能な名前を取得します。|
|[GetInfo](../../../extensibility/debugger/reference/idebugmemorycontext2-getinfo.md)|このコンテキストを説明する情報を取得します。|
|[追加](../../../extensibility/debugger/reference/idebugmemorycontext2-add.md)|新しいコンテキストを作成するために、指定した値を現在のコンテキストのアドレスに追加します。|
|[Subtract](../../../extensibility/debugger/reference/idebugmemorycontext2-subtract.md)|新しいコンテキストを作成するために、現在のコンテキストのアドレスから指定された値を減算します。|
|[比較](../../../extensibility/debugger/reference/idebugmemorycontext2-compare.md)|Compare フラグによって示される方法で、2つのコンテキストを比較します。|

## <a name="remarks"></a>注釈
 Visual Studio の **メモリ** ウィンドウは、 [getmemorycontext](../../../extensibility/debugger/reference/idebugproperty2-getmemorycontext.md) を呼び出して、 `IDebugMemoryContext2` メモリアドレスに使用される評価済みの式を含むインターフェイスを取得します。 次に、このコンテキストを [readat](../../../extensibility/debugger/reference/idebugmemorybytes2-readat.md) と [writeat](../../../extensibility/debugger/reference/idebugmemorybytes2-writeat.md) に渡して、読み取りまたは書き込みを行うアドレスを指定します。

## <a name="requirements"></a>要件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>こちらもご覧ください
- [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [GetMemoryContext](../../../extensibility/debugger/reference/idebugproperty2-getmemorycontext.md)
- [GetMemoryContext](../../../extensibility/debugger/reference/idebugreference2-getmemorycontext.md)
- [ReadAt](../../../extensibility/debugger/reference/idebugmemorybytes2-readat.md)
- [WriteAt](../../../extensibility/debugger/reference/idebugmemorybytes2-writeat.md)
