---
title: 'IDebugHelper:: CreatePropertyBrowser |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugHelper.CreatePropertyBrowser
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugHelper::CreatePropertyBrowser
ms.assetid: 2fa819cf-c7f7-4bd7-b018-ea33b804ba8f
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 99aa03470b49d02ee9f0ac1548bd1f8e27d0ab34
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72562500"
---
# <a name="idebughelpercreatepropertybrowser"></a>IDebugHelper::CreatePropertyBrowser
バリアントをラップするプロパティブラウザーを返します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT CreatePropertyBrowser(  
   VARIANT*                  pvar,  
   LPCOLESTR                 bstrName,  
   IDebugApplicationThread*  pdat,  
   IDebugProperty**          ppdob  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pvar`  
 から参照するルートバリアント。  
  
 `bstrName`  
 からルートに付ける名前。  
  
 `pdat`  
 からプロパティを要求するスレッド。 このパラメーターが NULL の場合、マーシャリングは実行されません。  
  
 `ppdob`  
 入出力プロパティブラウザー。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは `HRESULT` を返します。 有効な値を次の表に示しますが、これ以外にもあります。  
  
|値|説明|  
|-----------|-----------------|  
|`S_OK`|メソッドが成功しました。|  
  
## <a name="remarks"></a>コメント  
 このメソッドは、バリアントをラップするプロパティブラウザーを返します。  
  
## <a name="see-also"></a>参照  
 [IDebugHelper:: CreatePropertyBrowserEx](../../winscript/reference/idebughelper-createpropertybrowserex.md)   
 [IDebugHelper インターフェイス](../../winscript/reference/idebughelper-interface.md)   
 [IDebugProperty インターフェイス](../../winscript/reference/idebugproperty-interface.md)