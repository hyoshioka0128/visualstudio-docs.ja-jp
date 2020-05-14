---
title: IDebug ディスアセンブリストリーム2 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDisassemblyStream2
helpviewer_keywords:
- IDebugDisassemblyStream2 interface
ms.assetid: b03cab0c-3f0b-4cc6-88dc-acb3b48c567a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 98ba08e4ec32aceaf6c265714848939cc6ad9c66
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80732048"
---
# <a name="idebugdisassemblystream2"></a>IDebugDisassemblyStream2
このインターフェイスは、命令のストリームを表します。

## <a name="syntax"></a>構文

```
IDebugDisassemblyStream2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 デバッグ エンジンは、プログラムのコードの逆アセンブリをサポートするために、このインターフェイスを実装します。

## <a name="notes-for-callers"></a>発信者向けのメモ
 [メソッド](../../../extensibility/debugger/reference/idebugprogram2-getdisassemblystream.md)の呼び出しは、このインターフェイスを返します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に`IDebugDisassemblyStream2`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[Read](../../../extensibility/debugger/reference/idebugdisassemblystream2-read.md)|逆アセンブリ ストリームの現在位置から開始する命令を読み取ります。|
|[Seek](../../../extensibility/debugger/reference/idebugdisassemblystream2-seek.md)|指定した位置に対する指定した数の命令を逆アセンブリ ストリーム内の読み取りポインターに移動します。|
|[GetCodeLocationId](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcodelocationid.md)|特定のコード コンテキストのコードの場所識別子を返します。|
|[GetCodeContext](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcodecontext.md)|指定したコードの場所識別子に対応するコード コンテキスト オブジェクトを返します。|
|[GetCurrentLocation](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcurrentlocation.md)|現在のコードの場所を表すコードの場所の識別子を返します。|
|[GetDocument](../../../extensibility/debugger/reference/idebugdisassemblystream2-getdocument.md)|この逆アセンブリ ストリームに関連付けられているソース ドキュメントを取得します。|
|[GetScope](../../../extensibility/debugger/reference/idebugdisassemblystream2-getscope.md)|この逆アセンブリ ストリームのスコープを取得します。|
|[GetSize](../../../extensibility/debugger/reference/idebugdisassemblystream2-getsize.md)|この逆アセンブリ ストリームのサイズを取得します。|

## <a name="remarks"></a>Remarks
 逆アセンブリ ストリームは、アドレス空間全体を表すか、空間内の関数またはモジュールのみを表すために作成できます。 各命令は[、Read](../../../extensibility/debugger/reference/idebugdisassemblystream2-read.md)メソッドの呼び出しによって返される[DisassemblyData](../../../extensibility/debugger/reference/disassemblydata.md)構造体によって表されます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [GetDisassemblyStream](../../../extensibility/debugger/reference/idebugprogram2-getdisassemblystream.md)
- [DisassemblyData](../../../extensibility/debugger/reference/disassemblydata.md)
