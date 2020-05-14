---
title: をクリックします。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocumentContext2
helpviewer_keywords:
- IDebugDocumentContext2
ms.assetid: 2a446c71-8100-4c09-a1cc-fd446bd74030
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2d31a78412a1a6b20518b6f38ba76b7964cbdbe3
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80731735"
---
# <a name="idebugdocumentcontext2"></a>IDebugDocumentContext2
このインターフェイスは、ソース ファイル ドキュメント内の位置を表します。

## <a name="syntax"></a>構文

```
IDebugDocumentContext2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 デバッグ エンジン (DE) は、ソース コード レベルのデバッグのサポートの一部としてこのインターフェイスを実装します。 このインターフェイスは、ソース コード内の位置に加えて、コンテキストを比較し、ソース コード ドキュメント内を移動するためのメソッドを提供します。

## <a name="notes-for-callers"></a>発信者向けのメモ
 いくつかのインターフェイスのメソッド (ほとんどの場合[、GetDocumentContext](../../../extensibility/debugger/reference/idebugstackframe2-getdocumentcontext.md)インターフェイスと[GetDocumentContext](../../../extensibility/debugger/reference/idebugcodecontext2-getdocumentcontext.md)インターフェイス) は、このインターフェイスを返します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に`IDebugDocumentContext2`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[GetDocument](../../../extensibility/debugger/reference/idebugdocumentcontext2-getdocument.md)|このドキュメント コンテキストを含むドキュメントを取得します。|
|[GetName](../../../extensibility/debugger/reference/idebugdocumentcontext2-getname.md)|このドキュメント コンテキストを含むドキュメントの表示名を取得します。|
|[EnumCodeContexts](../../../extensibility/debugger/reference/idebugdocumentcontext2-enumcodecontexts.md)|このドキュメント コンテキストに関連付けられているすべてのコード コンテキストの一覧を取得します。|
|[GetLanguageInfo](../../../extensibility/debugger/reference/idebugdocumentcontext2-getlanguageinfo.md)|このドキュメント コンテキストに関連付けられている言語を取得します。|
|[GetStatementRange](../../../extensibility/debugger/reference/idebugdocumentcontext2-getstatementrange.md)|このドキュメント コンテキストのファイル ステートメント範囲を取得します。|
|[GetSourceRange](../../../extensibility/debugger/reference/idebugdocumentcontext2-getsourcerange.md)|このドキュメント コンテキストのファイル ソース範囲を取得します。|
|[比較](../../../extensibility/debugger/reference/idebugdocumentcontext2-compare.md)|このドキュメント コンテキストを、指定されたドキュメント コンテキストの配列と比較します。|
|[Seek](../../../extensibility/debugger/reference/idebugdocumentcontext2-seek.md)|指定された数のステートメントまたは行でドキュメント コンテキストを移動します。|

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [GetDocumentContext](../../../extensibility/debugger/reference/idebugcanstopevent2-getdocumentcontext.md)
- [GetDocumentContext](../../../extensibility/debugger/reference/idebugactivatedocumentevent2-getdocumentcontext.md)
- [GetDocumentContext](../../../extensibility/debugger/reference/idebugstackframe2-getdocumentcontext.md)
- [GetDocumentContext](../../../extensibility/debugger/reference/idebugcodecontext2-getdocumentcontext.md)
