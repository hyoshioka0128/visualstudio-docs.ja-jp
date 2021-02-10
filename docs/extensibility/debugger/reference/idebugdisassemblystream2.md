---
title: IDebugDisassemblyStream2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDisassemblyStream2
helpviewer_keywords:
- IDebugDisassemblyStream2 interface
ms.assetid: b03cab0c-3f0b-4cc6-88dc-acb3b48c567a
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d561c8eaa9f7b4fc08f71c241fd052fd366ca80d
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99944647"
---
# <a name="idebugdisassemblystream2"></a>IDebugDisassemblyStream2
このインターフェイスは、命令のストリームを表します。

## <a name="syntax"></a>構文

```
IDebugDisassemblyStream2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 デバッグエンジンは、プログラムのコードの逆アセンブリをサポートするために、このインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 [Getdisassemblystream](../../../extensibility/debugger/reference/idebugprogram2-getdisassemblystream.md)メソッドを呼び出すと、このインターフェイスが返されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、のメソッドを示し `IDebugDisassemblyStream2` ます。

|Method|説明|
|------------|-----------------|
|[読み取り](../../../extensibility/debugger/reference/idebugdisassemblystream2-read.md)|逆アセンブリストリームの現在位置から指示を読み取ります。|
|[Seek](../../../extensibility/debugger/reference/idebugdisassemblystream2-seek.md)|指定された位置を基準として、逆アセンブルストリーム内の読み取りポインターを指定された数だけ移動します。|
|[GetCodeLocationId](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcodelocationid.md)|特定のコードコンテキストのコード位置識別子を返します。|
|[GetCodeContext](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcodecontext.md)|指定されたコードの場所の識別子に対応するコードコンテキストオブジェクトを返します。|
|[GetCurrentLocation](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcurrentlocation.md)|現在のコードの場所を表すコード位置識別子を返します。|
|[GetDocument](../../../extensibility/debugger/reference/idebugdisassemblystream2-getdocument.md)|この逆アセンブリストリームに関連付けられているソースドキュメントを取得します。|
|[GetScope](../../../extensibility/debugger/reference/idebugdisassemblystream2-getscope.md)|この逆アセンブリストリームのスコープを取得します。|
|[GetSize](../../../extensibility/debugger/reference/idebugdisassemblystream2-getsize.md)|この逆アセンブリストリームのサイズを取得します。|

## <a name="remarks"></a>解説
 逆アセンブリストリームは、アドレス空間全体を表すために作成することも、スペース内の関数またはモジュールだけを表すように作成することもできます。 各命令は、 [Read](../../../extensibility/debugger/reference/idebugdisassemblystream2-read.md)メソッドの呼び出しによって返される[disassemblydata](../../../extensibility/debugger/reference/disassemblydata.md)構造体によって表されます。

## <a name="requirements"></a>要件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [GetDisassemblyStream](../../../extensibility/debugger/reference/idebugprogram2-getdisassemblystream.md)
- [DisassemblyData](../../../extensibility/debugger/reference/disassemblydata.md)
