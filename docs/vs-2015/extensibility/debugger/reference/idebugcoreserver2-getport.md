---
title: 'IDebugCoreServer2:: GetPort |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugCoreServer2::GetPort
helpviewer_keywords:
- IDebugCoreServer2::GetPort
ms.assetid: 3f5ea4a8-6085-4600-980a-9e48f8b5be56
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: e00f055d8e6a0fe1bea82061431410eb1e3b236f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68192922"
---
# <a name="idebugcoreserver2getport"></a>IDebugCoreServer2::GetPort
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

特定のポートを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT GetPort(   
   REFGUID       guidPort,  
   IDebugPort2** ppPort  
);  
```  
  
```csharp  
int GetPort(   
   ref Guid        guidPort,  
   out IDebugPort2 ppPort  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `guidPort`  
 から取得するポートの GUID。  
  
 `ppPort`  
 入出力目的のポートを表す [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md) オブジェクトを返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。 `E_PORTSUPPLIER_NO_PORT`指定された識別子を持つポートがない場合は、を返します。  
  
## <a name="see-also"></a>参照  
 [IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md)   
 [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)
