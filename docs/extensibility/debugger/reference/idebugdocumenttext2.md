---
title: をクリックします。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocumentText2
helpviewer_keywords:
- IDebugDocumentText2 interface
ms.assetid: e85f50a3-211c-4220-a9f4-789950ba2782
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5b5def7f6cc4ac5ced91ca0a273ce750003dca20
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80731568"
---
# <a name="idebugdocumenttext2"></a>IDebugDocumentText2
このインターフェイスは、テキスト ドキュメントを表します。

## <a name="syntax"></a>構文

```
IDebugDocumentText2 : IDebugDocument2
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 デバッグ エンジン (DE) は、指定する必要があるソース コードがテキスト形式である場合に、このインターフェイスを実装します。 これは最も一般的なケースであるため、DE が[IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)インターフェイスを実装する場合は、`IDebugDocumentText2`インターフェイスも実装する必要があります。

## <a name="notes-for-callers"></a>発信者向けのメモ
 このメソッド`QueryInterface`を使用して、インターフェイスからこの`IDebugDocument2`インターフェイスを取得します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 `IDebugDocument2`インターフェイスのメソッドに加えて、このインターフェイスは、次のメソッドを実装します。

|Method|説明|
|------------|-----------------|
|[GetSize](../../../extensibility/debugger/reference/idebugdocumenttext2-getsize.md)|文書内のこの位置にあるテキストのサイズを取得します。|
|[GetText](../../../extensibility/debugger/reference/idebugdocumenttext2-gettext.md)|文書内の指定した位置からテキストを取得します。|

## <a name="remarks"></a>Remarks
 このインターフェイスを実装するオブジェクトは<xref:System.Runtime.InteropServices.ComTypes.IConnectionPointContainer>[、IDebugDocumentTextEvents2](../../../extensibility/debugger/reference/idebugdocumenttextevents2.md)オブジェクト<xref:System.Runtime.InteropServices.ComTypes.IConnectionPoint>のインターフェイスを提供するインターフェイスも実装する必要があります。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)
- [IDebugDocumentTextEvents2](../../../extensibility/debugger/reference/idebugdocumenttextevents2.md)
