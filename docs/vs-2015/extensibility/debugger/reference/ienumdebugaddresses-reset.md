---
title: 'IEnumDebugAddresses:: Reset |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IEnumDebugAddresses::Reset
helpviewer_keywords:
- IEnumDebugAddresses::Reset method
ms.assetid: 3a9d7f20-5bc6-4e13-8e91-5af4092e092f
caps.latest.revision: 6
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 866c96f81edd5406f36790b932b057f6279f7e67
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68191945"
---
# <a name="ienumdebugaddressesreset"></a>IEnumDebugAddresses::Reset
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このメソッドは、列挙体を最初の要素にリセットします。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT Reset(void);  
```  
  
```csharp  
int Reset();  
```  
  
#### <a name="parameters"></a>パラメーター  
 None  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 このメソッドが呼び出された後、next を呼び出すと、列挙体の最初の要素が返さ[れます。](../../../extensibility/debugger/reference/ienumdebugaddresses-next.md)  
  
## <a name="see-also"></a>参照  
 [IEnumDebugAddresses](../../../extensibility/debugger/reference/ienumdebugaddresses.md)   
 [次へ](../../../extensibility/debugger/reference/ienumdebugaddresses-next.md)
