---
title: 'IDebugAddress:: GetAddress |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugAddress::GetAddress
helpviewer_keywords:
- IDebugAddress:GetAddress method
ms.assetid: 2590387b-5d36-4116-9a75-737957b8898e
caps.latest.revision: 7
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: f4d3263ca020f491e0c1cf20ee49792cacfbc362
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68186685"
---
# <a name="idebugaddressgetaddress"></a>IDebugAddress::GetAddress
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

オブジェクトとそのスコープ内またはコンテナー内の位置を記述する構造体を返します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetAddress (  
   DEBUG_ADDRESS * pAddress  
);  
```  
  
```csharp  
int GetAddress(  
   DEBUG_ADDRESS[] pAddress  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pAddress`  
 [入力、出力]このメソッドによって格納される [DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md) 構造体。  
  
## <a name="return-value"></a>戻り値  
 成功した場合は S_OK を返します。それ以外の場合は、エラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 [DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md)構造体がこのメソッドに渡され、その後、適切な情報が入力されます。 この情報の解釈方法は、返される情報の種類とシンボルハンドラー自体によって異なります。 詳細については、「 [DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md) 」を参照してください。  
  
## <a name="see-also"></a>参照  
 [DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md)
