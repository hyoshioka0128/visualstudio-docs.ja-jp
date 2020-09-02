---
title: 'IDebugDocumentContext2:: GetStatementRange |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugDocumentContext2::GetStatementRange
helpviewer_keywords:
- IDebugDocumentContext2::GetStatementRange
ms.assetid: bc94851a-0ec4-47ea-99c7-0a585e54e726
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 68411ac4ded03c83ad0ad1e414107e6591f4e975
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68145057"
---
# <a name="idebugdocumentcontext2getstatementrange"></a>IDebugDocumentContext2::GetStatementRange
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

ドキュメントコンテキストのファイルステートメントの範囲を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT GetStatementRange(   
   TEXT_POSITION* pBegPosition,  
   TEXT_POSITION* pEndPosition  
);  
```  
  
```csharp  
int GetStatementRange(   
   TEXT_POSITION[] pBegPosition,  
   TEXT_POSITION[] pEndPosition  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pBegPosition`  
 [入力、出力]開始位置を格納する [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md) 構造体。 この情報が不要な場合は、この引数を null 値に設定します。  
  
 `pEndPosition`  
 [入力、出力]終了位置を格納する [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md) 構造体。 この情報が不要な場合は、この引数を null 値に設定します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 ステートメント範囲は、このドキュメントコンテキストが参照するコードを提供する行の範囲です。  
  
 このドキュメントコンテキスト内のソースコードの範囲 (コメントを含む) を取得するには、 [GetSourceRange](../../../extensibility/debugger/reference/idebugdocumentcontext2-getsourcerange.md) メソッドを呼び出します。  
  
## <a name="example"></a>例  
 次の例は、IDebugDocumentContext2 インターフェイスを公開する単純なオブジェクトに対してこのメソッドを実装する方法を示して `CDebugContext` います。 [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md) この例では、開始位置が null 値でない場合にのみ終了位置を入力します。  
  
```cpp#  
HRESULT CDebugContext::GetStatementRange(TEXT_POSITION* pBegPosition,  
                                         TEXT_POSITION* pEndPosition)    
{    
   HRESULT hr;    
  
   // Check for a valid beginning position argument pointer.    
   if (pBegPosition)    
   {    
      // Copy the member TEXT_POSITION into the local pBegPosition.    
      memcpy(pBegPosition, &m_pos, sizeof (TEXT_POSITION));    
  
      // Check for a valid ending position argument pointer.   
     if (pEndPosition)    
      {    
         // Copy the member TEXT_POSITION into the local pEndPosition.    
         memcpy(pEndPosition, &m_pos, sizeof (TEXT_POSITION));    
      }    
      hr = S_OK;    
   }    
   else    
   {    
      hr = E_INVALIDARG;    
   }    
  
   return hr;    
}    
```  
  
## <a name="see-also"></a>参照  
 [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)   
 [GetSourceRange](../../../extensibility/debugger/reference/idebugdocumentcontext2-getsourcerange.md)   
 [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)
