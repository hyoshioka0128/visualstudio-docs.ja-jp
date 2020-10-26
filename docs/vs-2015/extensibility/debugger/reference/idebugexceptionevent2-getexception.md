---
title: 'IDebugExceptionEvent2:: GetException |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugExceptionEvent2::GetException
helpviewer_keywords:
- IDebugExceptionEvent2::GetException
ms.assetid: 7c98f41d-322b-4e72-a514-cbd4823eb70d
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a0e19dc924101fcceb93948272fc1e83353e2815
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68163796"
---
# <a name="idebugexceptionevent2getexception"></a>IDebugExceptionEvent2::GetException
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このイベントを発生させた例外の詳細な説明を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT GetException(   
   EXCEPTION_INFO* pExceptionInfo  
);  
```  
  
```csharp  
int GetException(   
   EXCEPTION_INFO[] pExceptionInfo  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pExceptionInfo`  
 [入力、出力]例外の説明と共に入力される [EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md) 構造体。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 [C++ のみ]呼び出し元は、構造内の[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)オブジェクトを解放するだけでなく、 [EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md)構造体内の任意の文字列を解放する役割も担います。  
  
## <a name="see-also"></a>参照  
 [IDebugExceptionEvent2](../../../extensibility/debugger/reference/idebugexceptionevent2.md)   
 [EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md)   
 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)   
 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
