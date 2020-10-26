---
title: IDebugProcessEx2::D etach |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugProcessEx2::Detach
helpviewer_keywords:
- IDebugProcessEx2::Detach method
ms.assetid: 66d54c2c-9302-47c8-9975-f30ed988ab29
caps.latest.revision: 16
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: b79f1f80f9b6849c37fc9b6c4c8669f1397f0227
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62538149"
---
# <a name="idebugprocessex2detach"></a>IDebugProcessEx2::Detach
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このメソッドは、セッションがプロセスのデバッグを終了したことをプロセスに通知します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT Detach(   
   IDebugSession2* pSession  
);  
```  
  
```csharp  
int Detach(  
   IDebugSession2 pSession  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pSession`  
 からこのプロセスをデタッチするセッションを一意に識別する値。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 渡されるインターフェイス `pSession` は、クッキーとしてのみ扱われます。これは、最初にこのプロセスにアタッチされたセッションデバッグマネージャーを一意に識別する値です。指定されたインターフェイスのメソッドは機能しません。  
  
## <a name="see-also"></a>参照  
 [IDebugProcessEx2](../../../extensibility/debugger/reference/idebugprocessex2.md)
