---
title: 'IDebugThread2:: Suspend |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugThread2::Suspend
helpviewer_keywords:
- IDebugThread2::Suspend
ms.assetid: 1e20be85-aa12-48de-bb83-0bf0976e99ae
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: c334a660b9c85345c636c7cc4b9aaea1a9b12076
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68152956"
---
# <a name="idebugthread2suspend"></a>IDebugThread2::Suspend
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

スレッドを中断します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT Suspend (   
   DWORD *pdwSuspendCount  
);  
```  
  
```csharp  
HRESULT Suspend (   
   out uint pdwSuspendCount  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pdwSuspendCount`  
 入出力中断操作後の中断回数を返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 このメソッドを呼び出すたびに、中断回数が0を超えて増加します。 この中断回数は、[ **スレッド** デバッグ] ウィンドウに表示されます。  
  
 このメソッドを呼び出すたびに、後で [Resume](../../../extensibility/debugger/reference/idebugthread2-resume.md) メソッドを呼び出す必要があります。  
  
## <a name="see-also"></a>参照  
 [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)   
 [[再開]](../../../extensibility/debugger/reference/idebugthread2-resume.md)
