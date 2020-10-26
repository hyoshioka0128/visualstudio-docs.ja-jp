---
title: 'IDebugProgramNodeAttach2:: OnAttach |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugProgramNodeAttach2::OnAttach
helpviewer_keywords:
- IDebugProgramNodeAttach2::OnAttach
ms.assetid: 5fe52761-a508-4ab5-abdb-334fb6590334
caps.latest.revision: 4
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 845ec66215c5d999aaf3b5c9658bc0fb8e7295a7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68148537"
---
# <a name="idebugprogramnodeattach2onattach"></a>IDebugProgramNodeAttach2::OnAttach
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

関連付けられているプログラムにアタッチするか、アタッチプロセスを [attach](../../../extensibility/debugger/reference/idebugengine2-attach.md) メソッドに従います。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT OnAttach(  
   [in] REFGUID guidProgramId  
);  
```  
  
```csharp  
int OnAttach(  
   ref Guid guidProgramId  
};  
```  
  
#### <a name="parameters"></a>パラメーター  
 `guidProgramId`  
 [入力] `GUID` 関連付けられたプログラムに割り当てる場合は。  
  
## <a name="return-value"></a>戻り値  
 正常に終了した場合は、`S_OK` を返します。 `S_FALSE` [Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md)メソッドを呼び出さない場合は、を返します。 それ以外の場合はエラー コードを返します。  
  
## <a name="remarks"></a>注釈  
 [Attach メソッドが](../../../extensibility/debugger/reference/idebugengine2-attach.md)呼び出される前に、アタッチ処理中にこのメソッドが呼び出されます。 メソッドは、 `OnAttach` アタッチプロセス自体を実行できます (この場合、このメソッドはを返し `S_FALSE` ます)。また、メソッドにアタッチプロセスを遅延させ `IDebugEngine2::Attach` `OnAttach` ます (メソッドはを返し `S_OK` ます)。 どちらの場合も、 `OnAttach` メソッドは、 `GUID` デバッグされているプログラムのを指定されたに設定でき `GUID` ます。  
  
## <a name="see-also"></a>参照  
 [IDebugProgramNodeAttach2](../../../extensibility/debugger/reference/idebugprogramnodeattach2.md)   
 [[アタッチ]](../../../extensibility/debugger/reference/idebugengine2-attach.md)
