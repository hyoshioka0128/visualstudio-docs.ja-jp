---
title: IDebugCodeContext2 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugCodeContext2
helpviewer_keywords:
- IDebugCodeContext2 interface
ms.assetid: 3670439e-2171-405d-9d77-dedb0f1cba93
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2e06fd709b2d076b6fa8de7f104e907eb1b35a42
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68190946"
---
# <a name="idebugcodecontext2"></a>IDebugCodeContext2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このインターフェイスは、コード命令の開始位置を表します。 現在、ほとんどのランタイムアーキテクチャでは、コードコンテキストはプログラムの実行ストリームのアドレスと考えることができます。  
  
## <a name="syntax"></a>Syntax  
  
```  
IDebugCodeContext2 : IDebugMemoryContext2  
```  
  
## <a name="notes-for-implementers"></a>実装側の注意  
 デバッグエンジンは、コード命令の位置をドキュメントの位置と関連付けるために、このインターフェイスを実装します。  
  
## <a name="notes-for-callers"></a>呼び出し元に関する注意事項  
 多くのインターフェイスのメソッドは、このインターフェイス (通常は [GetCodeContext](../../../extensibility/debugger/reference/idebugstackframe2-getcodecontext.md)) を返します。 また、 [IDebugDisassemblyStream2](../../../extensibility/debugger/reference/idebugdisassemblystream2.md) インターフェイスおよびブレークポイントの解決情報でも広く使用されています。  
  
## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド  
 このインターフェイスは、 [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md) インターフェイスのメソッドに加えて、次のメソッドを実装します。  
  
|メソッド|説明|  
|------------|-----------------|  
|[GetDocumentContext](../../../extensibility/debugger/reference/idebugcodecontext2-getdocumentcontext.md)|アクティブなコードコンテキストに対応するドキュメントコンテキストを取得します。|  
|[GetLanguageInfo](../../../extensibility/debugger/reference/idebugcodecontext2-getlanguageinfo.md)|このコードコンテキストの言語情報を取得します。|  
  
## <a name="remarks"></a>注釈  
 `IDebugCodeContext2`インターフェイスと[IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)インターフェイスの主な違いは、が `IDebugCodeContext2` 常に命令でアラインされることです。 これは、が `IDebugCodeContext2` 常に命令の先頭を指しているのに対し、は `IDebugMemoryContext2` ランタイムアーキテクチャのメモリの任意のバイトを指す場合があることを意味します。 `IDebugCodeContext2` は、基本ストレージサイズ (通常はバイト) ではなく、命令によってインクリメントされます。  
  
## <a name="requirements"></a>要件  
 ヘッダー: msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [GetDisassemblyStream](../../../extensibility/debugger/reference/idebugprogram2-getdisassemblystream.md)   
 [CanSetNextStatement](../../../extensibility/debugger/reference/idebugthread2-cansetnextstatement.md)   
 [SetNextStatement](../../../extensibility/debugger/reference/idebugthread2-setnextstatement.md)   
 [GetCodeContext](../../../extensibility/debugger/reference/idebugcanstopevent2-getcodecontext.md)   
 [GetCodeContext](../../../extensibility/debugger/reference/idebugstackframe2-getcodecontext.md)   
 [次に](../../../extensibility/debugger/reference/ienumdebugcodecontexts2-next.md)   
 [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)
