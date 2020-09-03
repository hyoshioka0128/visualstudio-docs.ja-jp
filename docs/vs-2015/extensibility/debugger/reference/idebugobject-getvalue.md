---
title: 'IDebugObject:: GetValue |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugObject::GetValue
helpviewer_keywords:
- IDebugObject::GetValue method
ms.assetid: eec6051e-8ecb-49fa-bdd4-dd786f211692
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: de6e6888cfce338ebcee90e722f07e900ce25d0b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68180530"
---
# <a name="idebugobjectgetvalue"></a>IDebugObject::GetValue
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

オブジェクトの値を連続する一連のバイトとして取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT GetValue(   
   BYTE* pValue,  
   UINT  nSize  
);  
```  
  
```csharp  
int GetValue(  
   ref byte[] pValue,   
   uint nSize  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pValue`  
 [入力、出力]オブジェクトの値を表す連続する一連のバイトを格納する配列。  
  
 `nSize`  
 からフェッチする最大バイト数。  
  
## <a name="return-value"></a>戻り値  
 成功した場合は S_OK を返します。それ以外の場合は、エラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 [GetSize](../../../extensibility/debugger/reference/idebugobject-getsize.md)メソッドを呼び出すことによってフェッチできる値の合計バイト数を取得します。  
  
## <a name="see-also"></a>参照  
 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
