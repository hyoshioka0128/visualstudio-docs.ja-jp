---
title: 'IDebugObject2:: IsUserData |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugObject2::IsUserData
helpviewer_keywords:
- IDebugObject2::IsUserData method
ms.assetid: 6ffa0d0e-f742-496d-acc7-db74c248bc45
caps.latest.revision: 8
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: fd595ce041ae1968e085e3b63b49d308cfd14452
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68194578"
---
# <a name="idebugobject2isuserdata"></a>IDebugObject2::IsUserData
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

オブジェクトがユーザーデータを表すかどうかを判断します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT IsUserData(  
   BOOL* pfUser  
);  
```  
  
```csharp  
int IsUserData(  
   out int pfUser  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pfUser`  
 入出力`TRUE`オブジェクトがユーザーデータを表している場合は0以外 () を返し、 `FALSE` そうでない場合はゼロ () を返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合は S_OK を返します。それ以外の場合は、エラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 ユーザーデータとは、"ジャスト Mycode" として指定されたモジュールの一部である任意のオブジェクトです (ユーザーが構成可能なオプションで、モジュールをユーザーコードとしてマークし、スタックトレースに表示します)。  
  
## <a name="see-also"></a>参照  
 [IDebugObject2](../../../extensibility/debugger/reference/idebugobject2.md)
