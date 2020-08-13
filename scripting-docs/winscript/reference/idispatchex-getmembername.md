---
title: 'IDispatchEx:: GetMemberName |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDispatchEx.GetMemberName
apilocation:
- scrobj.dll
helpviewer_keywords:
- GetMemberName method
ms.assetid: 5e59b63c-b781-4b90-88fd-40603a379a2d
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 8dbfb82e986ed6d1738bcc0cffeec35e5ba4515c
ms.sourcegitcommit: d281d2a04a5bc302650eebf369946d8f101e59dd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "88144611"
---
# <a name="idispatchexgetmembername"></a>IDispatchEx::GetMemberName
メンバーの名前を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT GetMemberName(  
   DISPID id,  
   BSTR *pbstrName  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `id`  
 メンバーを識別します。 `GetDispID`は、またはを使用し `GetNextDispID` てディスパッチ識別子を取得します。  
  
 `pbstrName`  
 `BSTR`メンバーの名前を受け取るのアドレス。 この値は、呼び出し元のアプリケーションによって解放されます。  
  
## <a name="return-value"></a>戻り値  
 次の値のいずれか。  
  
|値|意味|
|-|-|  
|`S_OK`|正常終了しました。|  
|`DISP_E_UNKNOWNNAME`|名前が不明です。|  
  
## <a name="example"></a>例  
  
```cpp
HRESULT hr;  
   BSTR bstrName;  
   DISPID dispid;  
   IDispatchEx *pdex;  
  
   // Assign to pdex  
   hr = pdex->GetNextDispID(fdexEnumAll, DISPID_STARTENUM, &dispid);  
   while (hr == NOERROR)  
   {  
      hr = pdex->GetMemberName(dispid, &bstrName);  
      if (!wcscmp(bstrName, OLESTR("Bar")))  
      {  
         SysFreeString(bstrName);  
         return TRUE;  
      }  
   SysFreeString(bstrName);  
   hr = pdex->GetNextDispID(fdexEnumAll, dispid, &dispid);  
   }  
```  
  
## <a name="see-also"></a>関連項目  
 [IDispatchEx インターフェイス](../../winscript/reference/idispatchex-interface.md)   
 [IDispatchEx:: GetDispID](../../winscript/reference/idispatchex-getdispid.md)   
 [IDispatchEx::GetNextDispID](../../winscript/reference/idispatchex-getnextdispid.md)