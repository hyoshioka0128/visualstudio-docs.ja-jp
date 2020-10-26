---
title: 'IDebugInterceptExceptionCompleteEvent2:: GetInterceptCookie |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugInterceptExceptionCompleteEvent2::GetInterceptCookie
helpviewer_keywords:
- IDebugInterceptExceptionCompleteEvent2::GetInterceptCookie
ms.assetid: 07b20866-e598-4783-9ecc-6aa8625c8804
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: e186419a102bdf48a437002ab03120587d6e0822
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68180657"
---
# <a name="idebuginterceptexceptioncompleteevent2getinterceptcookie"></a>IDebugInterceptExceptionCompleteEvent2::GetInterceptCookie
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

インターセプトされた例外の処理が完了したときに呼び出されます。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT GetInterceptCookie(  
   UINT64* pqwCookie  
);  
```  
  
```csharp  
int GetInterceptCookie(  
   out ulong pqwCookie  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pqwCookie`  
 入出力インターセプトされた例外に関連付けられている一意の値。  
  
## <a name="return-value"></a>戻り値  
 成功した場合は、を返します。それ以外の場合は `S_OK` エラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 [InterceptCurrentException](../../../extensibility/debugger/reference/idebugstackframe3-interceptcurrentexception.md)メソッドによってインターセプトされた例外の処理が完了すると、 [IDebugInterceptExceptionCompleteEvent2](../../../extensibility/debugger/reference/idebuginterceptexceptioncompleteevent2.md)イベントが送信されます。 ハンドラーは、メソッドを使用して、 `GetInterceptCookie` 例外に関連付けられている一意の値 (メソッドに渡されたものと同じ値) を取得でき `InterceptCurrentException` ます。  
  
## <a name="see-also"></a>参照  
 [InterceptCurrentException](../../../extensibility/debugger/reference/idebugstackframe3-interceptcurrentexception.md)   
 [IDebugInterceptExceptionCompleteEvent2](../../../extensibility/debugger/reference/idebuginterceptexceptioncompleteevent2.md)
