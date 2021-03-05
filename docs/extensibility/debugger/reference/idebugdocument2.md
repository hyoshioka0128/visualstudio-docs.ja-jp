---
description: このインターフェイスは、ソースドキュメントを表します。
title: IDebugDocument2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocument2
helpviewer_keywords:
- IDebugDocument2 interface
ms.assetid: 1bc58426-dbf5-4471-9aad-9d66cd80eef0
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 96bf5821cb463b8a99f7376cb99b81ab8cae2206
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102167348"
---
# <a name="idebugdocument2"></a>IDebugDocument2
このインターフェイスは、ソースドキュメントを表します。

## <a name="syntax"></a>構文

```
IDebugDocument2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] は、通常、このインターフェイスを実装します。 デバッグエンジン (DE) は、ソースコードを指定する必要があり、ソースがディスク上に存在しない場合にも、このインターフェイスを実装できます。  このような場合、DE は [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md) および [IDebugActivateDocumentEvent2](../../../extensibility/debugger/reference/idebugactivatedocumentevent2.md) インターフェイスを実装するほか、 [IDebugDisassemblyStream2](../../../extensibility/debugger/reference/idebugdisassemblystream2.md) および [IDebugDocumentPosition2](../../../extensibility/debugger/reference/idebugdocumentposition2.md) インターフェイスにいくつかの追加のメソッドを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 `IDebugDocumentContext2`、、、およびインターフェイスのメソッドは、 `IDebugDisassemblyStream2` `IDebugDocumentPosition2` `IDebugActivateDocumentEvent2` このインターフェイスを返します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、のメソッドを示し `IDebugDocument2` ます。

|メソッド|説明|
|------------|-----------------|
|[GetName](../../../extensibility/debugger/reference/idebugdocument2-getname.md)|複数の形式のいずれかで文書の名前を取得します。|
|[GetDocumentClassID](../../../extensibility/debugger/reference/idebugdocument2-getdocumentclassid.md)|ドキュメントのクラス識別子を取得します。|

## <a name="remarks"></a>解説
 このインターフェイスは、DE がソースコードを提供する場合にのみ実装されます。 たとえば、HTML ページでスクリプトをデバッグする場合、ソースは動的にダウンロードまたは生成され、ディスクファイルとして存在しないため、DE によってソースコードが提供されます。 C++ などの従来の言語をデバッグする場合は、このインターフェイスを実装する必要はありません。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [IsPositionInDocument](../../../extensibility/debugger/reference/idebugdocumentposition2-ispositionindocument.md)
- [GetDocument](../../../extensibility/debugger/reference/idebugactivatedocumentevent2-getdocument.md)
- [GetDocument](../../../extensibility/debugger/reference/idebugdocumentcontext2-getdocument.md)
- [GetDocument](../../../extensibility/debugger/reference/idebugdocumentposition2-getdocument.md)
- [GetDocument](../../../extensibility/debugger/reference/idebugdisassemblystream2-getdocument.md)
