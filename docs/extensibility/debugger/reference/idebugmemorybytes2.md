---
description: このインターフェイスは、メモリのバイト数を表します。
title: IDebugMemoryBytes2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMemoryBytes2
helpviewer_keywords:
- IDebugMemoryBytes2 interface
ms.assetid: d7647575-0e06-4190-88f5-ca40b82209a4
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: b18b4575780966d9ad34fa6c5638a89274d52c3c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105058639"
---
# <a name="idebugmemorybytes2"></a>IDebugMemoryBytes2
このインターフェイスは、メモリのバイト数を表します。

## <a name="syntax"></a>Syntax

```
IDebugMemoryBytes2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 デバッグエンジン (DE) は、メモリ内のバイトを表すために、このインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
- [Getmemorybytes](../../../extensibility/debugger/reference/idebugprogram2-getmemorybytes.md) は、システムメモリへのアクセスを提供するために、このインターフェイスを返します。 [Getmemorybytes](../../../extensibility/debugger/reference/idebugproperty2-getmemorybytes.md) と [getmemorybytes](../../../extensibility/debugger/reference/idebugreference2-getmemorybytes.md) は、オブジェクトのバイトへのアクセスを提供するために、このインターフェイスを返します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、のメソッドを示し `IDebugMemoryBytes2` ます。

|メソッド|説明|
|------------|-----------------|
|[ReadAt](../../../extensibility/debugger/reference/idebugmemorybytes2-readat.md)|指定された位置から始まるバイトシーケンスを読み取ります。|
|[WriteAt](../../../extensibility/debugger/reference/idebugmemorybytes2-writeat.md)|`dwCount`で始まるバイトを書き込み `pStartContext` ます。|
|[GetSize](../../../extensibility/debugger/reference/idebugmemorybytes2-getsize.md)|このインターフェイスによって表されるメモリのサイズ (バイト単位) を取得します。|

## <a name="remarks"></a>注釈
 プロパティの場合、配列を表す [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) インターフェイスは、 `IDebugMemoryBytes2` その配列内の値にアクセスするためのインターフェイスを提供します。

 Visual Studio の **メモリビュー** は、 [getmemorybytes](../../../extensibility/debugger/reference/idebugprogram2-getmemorybytes.md) を呼び出し `IDebugMemoryBytes2` て、システムメモリにアクセスするためのインターフェイスを取得します。 アクセスするアドレスを取得するには、アドレスとして入力された式をメモリビューに解析し、 [EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) を使用して解析された式を評価して、インターフェイスを取得し `IDebugProperty2` ます。 [Getmemorycontext](../../../extensibility/debugger/reference/idebugproperty2-getmemorycontext.md)を呼び出すと、メモリアドレスを説明する[IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)が返されます。 このメモリコンテキストは、 [readat](../../../extensibility/debugger/reference/idebugmemorybytes2-readat.md) および [writeat](../../../extensibility/debugger/reference/idebugmemorybytes2-writeat.md)に渡されます。

## <a name="requirements"></a>要件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>こちらもご覧ください
- [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [GetMemoryBytes](../../../extensibility/debugger/reference/idebugprogram2-getmemorybytes.md)
- [GetMemoryBytes](../../../extensibility/debugger/reference/idebugproperty2-getmemorybytes.md)
- [GetMemoryBytes](../../../extensibility/debugger/reference/idebugreference2-getmemorybytes.md)
- [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)
