---
title: をクリックします。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCodeContext2
helpviewer_keywords:
- IDebugCodeContext2 interface
ms.assetid: 3670439e-2171-405d-9d77-dedb0f1cba93
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 778602cc29049d855c418fd8fa416feb1ad8e9fe
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80734217"
---
# <a name="idebugcodecontext2"></a>IDebugCodeContext2
このインターフェイスは、コード命令の開始位置を表します。 今日のほとんどの実行時アーキテクチャでは、コード コンテキストはプログラムの実行ストリームのアドレスと考えることができます。

## <a name="syntax"></a>構文

```
IDebugCodeContext2 : IDebugMemoryContext2
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 デバッグ エンジンは、コード命令の位置をドキュメントの位置に関連付けるために、このインターフェイスを実装します。

## <a name="notes-for-callers"></a>発信者向けのメモ
 多くのインターフェイスのメソッドは、このインターフェイスを返[GetCodeContext](../../../extensibility/debugger/reference/idebugstackframe2-getcodecontext.md)します。 また、ブレークポイントの解像度情報だけでなく[、IDebugDisassemblyStream2](../../../extensibility/debugger/reference/idebugdisassemblystream2.md)インターフェイスで広く使用されています。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 このインターフェイスは[、IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)インターフェイスのメソッドに加えて、次のメソッドを実装します。

|Method|説明|
|------------|-----------------|
|[GetDocumentContext](../../../extensibility/debugger/reference/idebugcodecontext2-getdocumentcontext.md)|アクティブなコード コンテキストに対応するドキュメント コンテキストを取得します。|
|[GetLanguageInfo](../../../extensibility/debugger/reference/idebugcodecontext2-getlanguageinfo.md)|このコード コンテキストの言語情報を取得します。|

## <a name="remarks"></a>Remarks
 インターフェイスと[IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)インターフェイスの主な違いは、`IDebugCodeContext2`常に命令に整列されるということです。 `IDebugCodeContext2` つまり、a`IDebugCodeContext2`は常に命令の先頭を指し示しますが`IDebugMemoryContext2`、実行時アーキテクチャではメモリの任意のバイトを指している可能性があります。 `IDebugCodeContext2`は、基本ストレージ・サイズ (通常はバイト) ではなく、命令によって増分されます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [GetDisassemblyStream](../../../extensibility/debugger/reference/idebugprogram2-getdisassemblystream.md)
- [CanSetNextStatement](../../../extensibility/debugger/reference/idebugthread2-cansetnextstatement.md)
- [SetNextStatement](../../../extensibility/debugger/reference/idebugthread2-setnextstatement.md)
- [GetCodeContext](../../../extensibility/debugger/reference/idebugcanstopevent2-getcodecontext.md)
- [GetCodeContext](../../../extensibility/debugger/reference/idebugstackframe2-getcodecontext.md)
- [次へ](../../../extensibility/debugger/reference/ienumdebugcodecontexts2-next.md)
- [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)
