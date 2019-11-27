---
title: 'IDebugExpression:: Abort |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugExpression.Abort
apilocation:
- jscript.dll
helpviewer_keywords:
- IDebugExpression::Abort
ms.assetid: dbdb63c1-6c4a-4cef-bb40-1843495ae167
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 508939b23be53acbff269744ae4035853f977ada
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72575935"
---
# <a name="idebugexpressionabort"></a>IDebugExpression::Abort
式を停止します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT Abort();  
```  
  
#### <a name="parameters"></a>パラメーター  
 このメソッドはパラメーターを受け取りません。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは `HRESULT` を返します。 有効な値を次の表に示しますが、これ以外にもあります。  
  
|値|説明|  
|-----------|-----------------|  
|`S_OK`|メソッドが成功しました。|  
  
## <a name="remarks"></a>コメント  
 このメソッドは、最も早い機会で式の評価を停止します。  
  
## <a name="see-also"></a>参照  
 [IDebugExpression インターフェイス](../../winscript/reference/idebugexpression-interface.md)   
 [IDebugExpression::Start](../../winscript/reference/idebugexpression-start.md)