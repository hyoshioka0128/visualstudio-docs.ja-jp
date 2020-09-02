---
title: 'IDebugPortPicker:: SetSite |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- IDebugPortPicker::SetSite
ms.assetid: 7319e187-adfe-4b3f-aec9-521356fb5a8a
caps.latest.revision: 7
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 6cd0b91491be365a4686265bd698717219df0afb
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68188407"
---
# <a name="idebugportpickersetsite"></a>IDebugPortPicker::SetSite
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

サービスプロバイダーを設定します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT SetSite(  
   IServiceProvider * pSP  
);  
```  
  
```csharp  
public int SetSite(  
   IServiceProvider pSP  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pSP`  
 からサービスプロバイダーのインターフェイスへの参照。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 このメソッドは、他のメソッドが呼び出される前に呼び出されます。  
  
## <a name="see-also"></a>参照  
 [IDebugPortPicker](../../../extensibility/debugger/reference/idebugportpicker.md)
