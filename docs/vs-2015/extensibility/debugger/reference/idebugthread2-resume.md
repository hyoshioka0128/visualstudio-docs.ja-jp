---
title: 'IDebugThread2:: Resume |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugThread2::Resume
helpviewer_keywords:
- IDebugThread2::Resume
ms.assetid: 36aad682-b0b9-40a2-b3fc-f0e61d41cdbc
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 5bdec7338864926187b3d5056ffd2f2c4e1d7824
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68152990"
---
# <a name="idebugthread2resume"></a>IDebugThread2::Resume
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

スレッドの実行を再開します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT Resume (   
   DWORD *pdwSuspendCount  
);  
```  
  
```csharp  
int Resume (   
   out uint pdwSuspendCount  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pdwSuspendCount`  
 入出力再開操作後の中断回数を返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 このメソッドを呼び出すたびに、0に達するまで中断回数が減少します。この時間が経過すると、実行は実際に再開されます。 この中断回数は、[ **スレッド** デバッグ] ウィンドウに表示されます。  
  
 このメソッドを呼び出すたびに、前に [Suspend](../../../extensibility/debugger/reference/idebugthread2-suspend.md) メソッドを呼び出す必要があります。 中断カウントは、これ `IDebugThread2::Suspend` までにメソッドが呼び出された回数を決定します。  
  
## <a name="see-also"></a>参照  
 [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)   
 [[中断]](../../../extensibility/debugger/reference/idebugthread2-suspend.md)
