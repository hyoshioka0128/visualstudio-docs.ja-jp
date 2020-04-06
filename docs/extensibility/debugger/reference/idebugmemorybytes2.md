---
title: メモリバイト2をデバッグする |マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80727506"
---
# <a name="idebugmemorybytes2"></a>IDebugMemoryBytes2
このインターフェイスは、メモリのバイトを表します。

## <a name="syntax"></a>構文

```
IDebugMemoryBytes2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 デバッグ エンジン (DE) は、メモリ内のバイトを表すこのインターフェイスを実装します。

## <a name="notes-for-callers"></a>発信者向けのメモ
- [システム メモリ](../../../extensibility/debugger/reference/idebugprogram2-getmemorybytes.md)へのアクセスを提供するために、このインターフェイスを返します。 [オブジェクトのバイトへの](../../../extensibility/debugger/reference/idebugproperty2-getmemorybytes.md)アクセスを提供するために、このインターフェイス[を返します](../../../extensibility/debugger/reference/idebugreference2-getmemorybytes.md)。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に`IDebugMemoryBytes2`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[ReadAt](../../../extensibility/debugger/reference/idebugmemorybytes2-readat.md)|指定された位置から開始して、バイトシーケンスを読み取ります。|
|[WriteAt](../../../extensibility/debugger/reference/idebugmemorybytes2-writeat.md)|バイト`dwCount`を書き込`pStartContext`みます。|
|[GetSize](../../../extensibility/debugger/reference/idebugmemorybytes2-getsize.md)|このインターフェイスによって表されるメモリのサイズ (バイト単位) を取得します。|

## <a name="remarks"></a>Remarks
 プロパティの場合、配列を表す[IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)インターフェイス`IDebugMemoryBytes2`は、その配列内の値にアクセスするためのインターフェイスを提供します。

 システム メモリにアクセスするためのインターフェイスを取得するために[、メモリ](../../../extensibility/debugger/reference/idebugprogram2-getmemorybytes.md)`IDebugMemoryBytes2`**ビュー**を呼び出します。 アクセスするアドレスは、メモリ ビューにアドレスとして入力された式を解析し、次に[EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)を使用して解析された式を評価して`IDebugProperty2`インターフェイスを取得することによって取得されます。 呼び出しは[、](../../../extensibility/debugger/reference/idebugproperty2-getmemorycontext.md)メモリ アドレスを記述する[IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)を返します。 このメモリ コンテキストは[ReadAt](../../../extensibility/debugger/reference/idebugmemorybytes2-readat.md)と[WriteAt](../../../extensibility/debugger/reference/idebugmemorybytes2-writeat.md)に渡されます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [GetMemoryBytes](../../../extensibility/debugger/reference/idebugprogram2-getmemorybytes.md)
- [GetMemoryBytes](../../../extensibility/debugger/reference/idebugproperty2-getmemorybytes.md)
- [GetMemoryBytes](../../../extensibility/debugger/reference/idebugreference2-getmemorybytes.md)
- [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)
