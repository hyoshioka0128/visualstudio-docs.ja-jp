---
title: 'IDebugDisassemblyStream2:: GetCodeLocationId |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugDisassemblyStream2::GetCodeLocationId
helpviewer_keywords:
- IDebugDisassemblyStream2::GetCodeLocationId
ms.assetid: 567adfb8-2f54-499a-a027-e4ecb82277ef
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: ebb2280f814985e2352413921a00268d96761b7d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68196230"
---
# <a name="idebugdisassemblystream2getcodelocationid"></a>IDebugDisassemblyStream2::GetCodeLocationId
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

特定のコードコンテキストのコード位置識別子を返します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT GetCodeLocationId(   
   IDebugCodeContext2* pCodeContext,  
   UINT64*             puCodeLocationId  
);  
```  
  
```csharp  
int GetCodeLocationId(   
   IDebugCodeContext2 pCodeContext,  
   out ulong          puCodeLocationId  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pCodeContext`  
 から識別子に変換される [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md) オブジェクト。  
  
 `puCodeLocationId`  
 入出力コードの場所の識別子を返します。 「解説」を参照してください。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。 `E_CODE_CONTEXT_OUT_OF_SCOPE`コードコンテキストが有効であってもスコープ外にある場合は、を返します。  
  
## <a name="remarks"></a>注釈  
 コードの場所の識別子は、逆アセンブリをサポートするデバッグエンジン (DE) に固有です。 この場所識別子は、コード内の位置を追跡するために、DE によって内部的に使用されます。通常は、何らかの種類のアドレスまたはオフセットです。 唯一の要件は、ある場所のコードコンテキストが別の場所のコードコンテキストよりも小さい場合、最初のコードコンテキストの対応するコードの場所の識別子も、2番目のコードコンテキストのコードの場所の識別子よりも小さくなければならないということです。  
  
 コードの場所の識別子のコードコンテキストを取得するには、 [GetCodeContext](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcodecontext.md) メソッドを呼び出します。  
  
## <a name="see-also"></a>参照  
 [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)   
 [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)   
 [GetCodeContext](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcodecontext.md)
