---
title: をクリックしてドキュメントを作成する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocument2
helpviewer_keywords:
- IDebugDocument2 interface
ms.assetid: 1bc58426-dbf5-4471-9aad-9d66cd80eef0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 4c959c018dd4da0ff088c4fb52c0420de83b4eac
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80731994"
---
# <a name="idebugdocument2"></a>IDebugDocument2
このインターフェイスは、ソース ドキュメントを表します。

## <a name="syntax"></a>構文

```
IDebugDocument2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]通常は、このインターフェイスを実装します。 デバッグ エンジン (DE) は、ソース コードを提供する必要があり、ソースがディスク上に存在しない場合にも、このインターフェイスを実装できます。  このような場合、DE は[IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)インターフェイスと[IDebugActivateDocumentEvent2](../../../extensibility/debugger/reference/idebugactivatedocumentevent2.md)インターフェイス、および[IDebugDisassemblyStream2](../../../extensibility/debugger/reference/idebugdisassemblystream2.md)および[IDebugDocumentPosition2](../../../extensibility/debugger/reference/idebugdocumentposition2.md)インターフェイスのいくつかの追加メソッドも実装します。

## <a name="notes-for-callers"></a>発信者向けのメモ
 `IDebugDocumentContext2`、、および`IDebugDisassemblyStream2``IDebugDocumentPosition2`インターフェイスのメソッドは`IDebugActivateDocumentEvent2`、このインターフェイスを返します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に`IDebugDocument2`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[GetName](../../../extensibility/debugger/reference/idebugdocument2-getname.md)|複数のフォームのいずれかでドキュメントの名前を取得します。|
|[GetDocumentClassID](../../../extensibility/debugger/reference/idebugdocument2-getdocumentclassid.md)|ドキュメントのクラス識別子を取得します。|

## <a name="remarks"></a>Remarks
 このインターフェイスは、DE がソース コードを提供する場合にのみ実装されます。 たとえば、HTML ページでスクリプトをデバッグする場合、ソースがダウンロードまたは動的に生成され、ディスク ファイルとして存在しないため、DE はソース コードを提供します。 C++ などの従来の言語をデバッグする場合、このインターフェイスを実装する必要はありません。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [IsPositionInDocument](../../../extensibility/debugger/reference/idebugdocumentposition2-ispositionindocument.md)
- [GetDocument](../../../extensibility/debugger/reference/idebugactivatedocumentevent2-getdocument.md)
- [GetDocument](../../../extensibility/debugger/reference/idebugdocumentcontext2-getdocument.md)
- [GetDocument](../../../extensibility/debugger/reference/idebugdocumentposition2-getdocument.md)
- [GetDocument](../../../extensibility/debugger/reference/idebugdisassemblystream2-getdocument.md)
