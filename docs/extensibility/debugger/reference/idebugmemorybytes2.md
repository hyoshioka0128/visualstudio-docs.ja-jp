---
title: IDebugMemoryBytes2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMemoryBytes2
helpviewer_keywords:
- IDebugMemoryBytes2 interface
ms.assetid: d7647575-0e06-4190-88f5-ca40b82209a4
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 56cb234e2295c5c9c08c2a2e9271e1c173524875
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80727506"
---
# <a name="idebugmemorybytes2"></a>IDebugMemoryBytes2
このインターフェイスは、メモリのバイト数を表します。

## <a name="syntax"></a>構文

```
IDebugMemoryBytes2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 デバッグエンジン (DE) は、メモリ内のバイトを表すために、このインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
- [Getmemorybytes](../../../extensibility/debugger/reference/idebugprogram2-getmemorybytes.md) は、システムメモリへのアクセスを提供するために、このインターフェイスを返します。 [Getmemorybytes](../../../extensibility/debugger/reference/idebugproperty2-getmemorybytes.md) と [getmemorybytes](../../../extensibility/debugger/reference/idebugreference2-getmemorybytes.md) は、オブジェクトのバイトへのアクセスを提供するために、このインターフェイスを返します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、のメソッドを示し `IDebugMemoryBytes2` ます。

|Method|説明|
|------------|-----------------|
|[ReadAt](../../../extensibility/debugger/reference/idebugmemorybytes2-readat.md)|指定された位置から始まるバイトシーケンスを読み取ります。|
|[WriteAt](../../../extensibility/debugger/reference/idebugmemorybytes2-writeat.md)|`dwCount`で始まるバイトを書き込み `pStartContext` ます。|
|[GetSize](../../../extensibility/debugger/reference/idebugmemorybytes2-getsize.md)|このインターフェイスによって表されるメモリのサイズ (バイト単位) を取得します。|

## <a name="remarks"></a>解説
 プロパティの場合、配列を表す [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) インターフェイスは、 `IDebugMemoryBytes2` その配列内の値にアクセスするためのインターフェイスを提供します。

 Visual Studio の **メモリビュー** は、 [getmemorybytes](../../../extensibility/debugger/reference/idebugprogram2-getmemorybytes.md) を呼び出し `IDebugMemoryBytes2` て、システムメモリにアクセスするためのインターフェイスを取得します。 アクセスするアドレスを取得するには、アドレスとして入力された式をメモリビューに解析し、 [EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) を使用して解析された式を評価して、インターフェイスを取得し `IDebugProperty2` ます。 [Getmemorycontext](../../../extensibility/debugger/reference/idebugproperty2-getmemorycontext.md)を呼び出すと、メモリアドレスを説明する[IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)が返されます。 このメモリコンテキストは、 [readat](../../../extensibility/debugger/reference/idebugmemorybytes2-readat.md) および [writeat](../../../extensibility/debugger/reference/idebugmemorybytes2-writeat.md)に渡されます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [GetMemoryBytes](../../../extensibility/debugger/reference/idebugprogram2-getmemorybytes.md)
- [GetMemoryBytes](../../../extensibility/debugger/reference/idebugproperty2-getmemorybytes.md)
- [GetMemoryBytes](../../../extensibility/debugger/reference/idebugreference2-getmemorybytes.md)
- [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)
