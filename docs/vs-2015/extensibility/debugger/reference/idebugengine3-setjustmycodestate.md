---
title: 'IDebugEngine3:: Setジャスト Mycodestate |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugEngine3::SetJustMyCodeState
helpviewer_keywords:
- IDebugEngine3::SetJustMyCodeState
ms.assetid: 8ec17fbf-df93-424a-b2ed-fd1e5ee51256
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: ebaf697bfdfff435c12eee1002ff93f4eba7ed65
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68195864"
---
# <a name="idebugengine3setjustmycodestate"></a>IDebugEngine3::SetJustMyCodeState
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このメソッドは、ジャスト Mycode 状態情報についてデバッグエンジンに通知します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT SetJustMyCodeState(  
   BOOL           fUpdate,  
   DWORD          dwModules,  
   JMC_CODE_SPEC* rgJMCSpec  
);  
```  
  
```csharp  
int SetJustMyCodeState(  
   int             fUpdate,   
   uint            dwModules,   
   JMC_CODE_SPEC[] rgJMCSpec  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `fUpdate`  
 から現在の `TRUE` 情報を更新する場合は0以外 ()。すべての情報をリセットする場合は 0 ( `FALSE` )。  
  
 `dwModules`  
 からの情報構造の数 `rgJMCSpec.`  
  
 `rgJMCSpec`  
 から使用する [JMC_CODE_SPEC](../../../extensibility/debugger/reference/jmc-code-spec.md) 構造体の配列。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 ジャスト Mycode は、システムコードでソースコードを使用できる場合でも、ユーザーに属しているコードのみをデバッグし、システムコードなどのすべての中間コードを無視するという概念です。  
  
## <a name="see-also"></a>参照  
 [IDebugEngine3](../../../extensibility/debugger/reference/idebugengine3.md)   
 [JMC_CODE_SPEC](../../../extensibility/debugger/reference/jmc-code-spec.md)
