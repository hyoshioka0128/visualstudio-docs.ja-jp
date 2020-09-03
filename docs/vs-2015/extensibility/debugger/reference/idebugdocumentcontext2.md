---
title: IDebugDocumentContext2 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugDocumentContext2
helpviewer_keywords:
- IDebugDocumentContext2
ms.assetid: 2a446c71-8100-4c09-a1cc-fd446bd74030
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: b6d040597f48d4514a58027df3335c080d6305a4
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68144948"
---
# <a name="idebugdocumentcontext2"></a>IDebugDocumentContext2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このインターフェイスは、ソースファイルドキュメント内の位置を表します。  
  
## <a name="syntax"></a>Syntax  
  
```  
IDebugDocumentContext2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>実装側の注意  
 デバッグエンジン (DE) は、ソースコードレベルのデバッグのサポートの一部として、このインターフェイスを実装します。 このインターフェイスは、ソースコード内の位置に加えて、コンテキストを比較し、ソースコードドキュメント内を移動するためのメソッドを提供します。  
  
## <a name="notes-for-callers"></a>呼び出し元に関する注意事項  
 いくつかのインターフェイスのメソッド (通常は [getdocumentcontext](../../../extensibility/debugger/reference/idebugstackframe2-getdocumentcontext.md) および [getdocumentcontext](../../../extensibility/debugger/reference/idebugcodecontext2-getdocumentcontext.md) インターフェイス) は、このインターフェイスを返します。  
  
## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド  
 次の表に、のメソッドを示し `IDebugDocumentContext2` ます。  
  
|メソッド|説明|  
|------------|-----------------|  
|[GetDocument](../../../extensibility/debugger/reference/idebugdocumentcontext2-getdocument.md)|このドキュメントコンテキストを含むドキュメントを取得します。|  
|[GetName](../../../extensibility/debugger/reference/idebugdocumentcontext2-getname.md)|このドキュメントコンテキストを含むドキュメントの表示可能な名前を取得します。|  
|[EnumCodeContexts](../../../extensibility/debugger/reference/idebugdocumentcontext2-enumcodecontexts.md)|このドキュメントコンテキストに関連付けられているすべてのコードコンテキストのリストを取得します。|  
|[GetLanguageInfo](../../../extensibility/debugger/reference/idebugdocumentcontext2-getlanguageinfo.md)|このドキュメントコンテキストに関連付けられている言語を取得します。|  
|[GetStatementRange](../../../extensibility/debugger/reference/idebugdocumentcontext2-getstatementrange.md)|このドキュメントコンテキストのファイルステートメントの範囲を取得します。|  
|[GetSourceRange](../../../extensibility/debugger/reference/idebugdocumentcontext2-getsourcerange.md)|このドキュメントコンテキストのファイルソースの範囲を取得します。|  
|[比較](../../../extensibility/debugger/reference/idebugdocumentcontext2-compare.md)|このドキュメントコンテキストと、指定されたドキュメントコンテキストの配列を比較します。|  
|[Seek](../../../extensibility/debugger/reference/idebugdocumentcontext2-seek.md)|指定された数のステートメントまたは行によってドキュメントコンテキストを移動します。|  
  
## <a name="requirements"></a>要件  
 ヘッダー: msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [GetDocumentContext](../../../extensibility/debugger/reference/idebugcanstopevent2-getdocumentcontext.md)   
 [GetDocumentContext](../../../extensibility/debugger/reference/idebugactivatedocumentevent2-getdocumentcontext.md)   
 [GetDocumentContext](../../../extensibility/debugger/reference/idebugstackframe2-getdocumentcontext.md)   
 [GetDocumentContext](../../../extensibility/debugger/reference/idebugcodecontext2-getdocumentcontext.md)
