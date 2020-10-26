---
title: 'IDebugDocumentContext2:: GetSourceRange |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugDocumentContext2::GetSourceRange
helpviewer_keywords:
- IDebugDocumentContext2::GetSourceRange
ms.assetid: 5903c75e-5390-4d13-9314-1ee276255313
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: bcec6af2b8e7b1acfdc9c3cf38cb18654be78c53
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68145000"
---
# <a name="idebugdocumentcontext2getsourcerange"></a>IDebugDocumentContext2::GetSourceRange
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このドキュメントコンテキストのソースコードの範囲を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT GetSourceRange(   
   TEXT_POSITION* pBegPosition,  
   TEXT_POSITION* pEndPosition  
);  
```  
  
```csharp  
int GetSourceRange(   
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
 ソース範囲は、ソースコードの範囲全体であり、現在のステートメントから、コードを提供した前のステートメントの直後に戻ります。 ソース範囲は、通常、コメントなどのソースステートメントと、[逆アセンブル] ウィンドウのコードを組み合わせるために使用されます。  
  
 このドキュメントコンテキスト内に含まれるコードステートメントの範囲だけを取得するには、 [GetStatementRange](../../../extensibility/debugger/reference/idebugdocumentcontext2-getstatementrange.md) メソッドを呼び出します。  
  
## <a name="see-also"></a>参照  
 [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)   
 [GetStatementRange](../../../extensibility/debugger/reference/idebugdocumentcontext2-getstatementrange.md)   
 [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)
