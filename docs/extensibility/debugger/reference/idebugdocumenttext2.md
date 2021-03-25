---
description: このインターフェイスは、テキストドキュメントを表します。
title: IDebugDocumentText2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocumentText2
helpviewer_keywords:
- IDebugDocumentText2 interface
ms.assetid: e85f50a3-211c-4220-a9f4-789950ba2782
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 557ae68e63280348ab315c3240e05dbfc38a8d4d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105066283"
---
# <a name="idebugdocumenttext2"></a>IDebugDocumentText2
このインターフェイスは、テキストドキュメントを表します。

## <a name="syntax"></a>Syntax

```
IDebugDocumentText2 : IDebugDocument2
```

## <a name="notes-for-implementers"></a>実装側の注意
 デバッグエンジン (DE) は、指定するソースコードがテキスト形式である場合に、このインターフェイスを実装します。 これは最も一般的なケースであるため、DE が [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md) インターフェイスを実装する場合は、インターフェイスも実装する必要があり `IDebugDocumentText2` ます。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 `QueryInterface`インターフェイスからこのインターフェイスを取得するには、メソッドを使用し `IDebugDocument2` ます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 このインターフェイスには、インターフェイスのメソッドに加えて、 `IDebugDocument2` 次のメソッドが実装されています。

|メソッド|説明|
|------------|-----------------|
|[GetSize](../../../extensibility/debugger/reference/idebugdocumenttext2-getsize.md)|ドキュメント内のこの位置にあるテキストのサイズを取得します。|
|[GetText](../../../extensibility/debugger/reference/idebugdocumenttext2-gettext.md)|ドキュメント内の指定した位置からテキストを取得します。|

## <a name="remarks"></a>注釈
 このインターフェイスを実装するオブジェクトは、 <xref:System.Runtime.InteropServices.ComTypes.IConnectionPointContainer> <xref:System.Runtime.InteropServices.ComTypes.IConnectionPoint> [IDebugDocumentTextEvents2](../../../extensibility/debugger/reference/idebugdocumenttextevents2.md) オブジェクトのインターフェイスを提供するインターフェイスも実装する必要があります。

## <a name="requirements"></a>要件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>こちらもご覧ください
- [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)
- [IDebugDocumentTextEvents2](../../../extensibility/debugger/reference/idebugdocumenttextevents2.md)
