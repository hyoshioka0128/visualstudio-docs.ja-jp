---
title: 'IEnumDebugAddresses:: Clone |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IEnumDebugAddresses::Clone
helpviewer_keywords:
- IEnumDebugAddresses::Clone method
ms.assetid: 71189a00-34eb-4c71-b96e-8bd6e70c6966
caps.latest.revision: 6
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 732b01b813a9d09861d87a75a3078407bb75bcab
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68191970"
---
# <a name="ienumdebugaddressesclone"></a>IEnumDebugAddresses::Clone
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このメソッドは、現在の列挙体のコピーを別のオブジェクトとして返します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT Clone(  
   IEnumDebugAddresses** ppEnum  
);  
```  
  
```csharp  
int Clone(  
   out IEnumDebugAddresses ppEnum  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `ppEnum`  
 入出力この列挙体のコピーを別のオブジェクトとして返します。  
  
## <a name="property-valuereturn-value"></a>プロパティ値/戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 列挙体のコピーは、このメソッドが呼び出されたときの元の状態と同じ状態になります。 ただし、コピーと元の状態は別々であり、個別に変更できます。  
  
## <a name="see-also"></a>参照  
 [IEnumDebugAddresses](../../../extensibility/debugger/reference/ienumdebugaddresses.md)
