---
title: 'IDebugApplication:: Removeglobal式 Contextprovider |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugApplication.RemoveGlobalExpressionContextProvider
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugApplication::RemoveGlobalExpressionContextProvider
ms.assetid: ace638a3-ed34-4d20-8404-45c684aaaf1a
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: b4b948cea02d696b6c176e925adf9c95913be2cd
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72571141"
---
# <a name="idebugapplicationremoveglobalexpressioncontextprovider"></a>IDebugApplication::RemoveGlobalExpressionContextProvider
グローバル式コンテキストプロバイダーをこのアプリケーションから削除します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT RemoveGlobalExpressionContextProvider(  
   DWORD_PTR  dwCookie  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `dwCookie`  
 からグローバルコンテキストプロバイダーが追加されたときに `AddGlobalExpressionContextProvider` メソッドによって返されるクッキー。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは `HRESULT` を返します。 有効な値を次の表に示しますが、これ以外にもあります。  
  
|値|説明|  
|-----------|-----------------|  
|`S_OK`|メソッドが成功しました。|  
  
## <a name="remarks"></a>コメント  
 `RemoveGlobalExpressionContextProvider` メソッドは、このアプリケーションからグローバル式コンテキストプロバイダーを削除します。  
  
## <a name="see-also"></a>参照  
 [IDebugApplication::AddGlobalExpressionContextProvider](../../winscript/reference/idebugapplication-addglobalexpressioncontextprovider.md)   
 [IDebugApplication インターフェイス](../../winscript/reference/idebugapplication-interface.md)