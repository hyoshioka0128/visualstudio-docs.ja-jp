---
title: 'IDispatchEx:: GetMemberProperties |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDispatchEx.GetMemberProperties
apilocation:
- scrobj.dll
helpviewer_keywords:
- GetMemberProperties method
ms.assetid: 20d43209-12e2-472a-9bf3-81eced137b71
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 488f8790ec25532fb611f18e8b24e7e7dba2e2f4
ms.sourcegitcommit: d281d2a04a5bc302650eebf369946d8f101e59dd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "88144550"
---
# <a name="idispatchexgetmemberproperties"></a>IDispatchEx::GetMemberProperties
メンバーのプロパティを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT GetMemberProperties(  
   DISPID id,  
   DWORD grfdexFetch,  
   DWORD *pgrfdex  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `id`  
 メンバーを識別します。 `GetDispID`は、またはを使用し `GetNextDispID` てディスパッチ識別子を取得します。  
  
 `grfdexFetch`  
 取得するプロパティを決定します。 この値は、次の値の下に表示される値の組み合わせにすることができ `pgrfdex` ます。  
  
|値|意味|  
|-----------|-------------|  
|grfdexPropCanAll|FdexPropCanGet、fdexPropCanPut、fdexPropCanPutRef、fdexPropCanCall、fdexPropCanConstruct、および Fdexpropcanget を結合します。|  
|grfdexPropCannotAll|FdexPropCannotGet、fdexPropCannotPut、fdexPropCannotPutRef、fdexPropCannotCall、fdexPropCannotConstruct、fdexPropCannotSourceEvents を結合します。|  
|grfdexPropExtraAll|FdexPropNoSideEffects と fdexPropDynamicType を結合します。|  
|grfdexPropAll|GrfdexPropCanAll、grfdexPropCannotAll、および grfdexPropExtraAll を結合します。|  
  
 `pgrfdex`  
 要求されたプロパティを受け取るのアドレス `DWORD` 。 次の値の組み合わせを指定できます。  
  
|値|意味|  
|-----------|-------------|  
|fdexPropCanGet|メンバーは DISPATCH_PROPERTYGET を使用して取得できます。|  
|fdexPropCannotGet|DISPATCH_PROPERTYGET を使用してメンバーを取得することはできません。|  
|fdexPropCanPut|メンバーは DISPATCH_PROPERTYPUT を使用して設定できます。|  
|fdexPropCannotPut|DISPATCH_PROPERTYPUT を使用してメンバーを設定することはできません。|  
|fdexPropCanPutRef|メンバーは DISPATCH_PROPERTYPUTREF を使用して設定できます。|  
|fdexPropCannotPutRef|DISPATCH_PROPERTYPUTREF を使用してメンバーを設定することはできません。|  
|fdexPropNoSideEffects|メンバーには副作用がありません。 たとえば、デバッガーは、デバッグされているスクリプトの状態を変更せずに、このメンバーを安全に取得/設定/呼び出しできます。|  
|fdexPropDynamicType|メンバーは動的であり、オブジェクトの有効期間中に変更できます。|  
|fdexPropCanCall|メンバーは、DISPATCH_METHOD を使用してメソッドとして呼び出すことができます。|  
|fdexPropCannotCall|DISPATCH_METHOD を使用して、メンバーをメソッドとして呼び出すことはできません。|  
|fdexPropCanConstruct|メンバーは DISPATCH_CONSTRUCT を使用してコンストラクターとして呼び出すことができます。|  
|fdexPropCannotConstruct|DISPATCH_CONSTRUCT を使用して、メンバーをコンストラクターとして呼び出すことはできません。|  
|fdexPropCanSourceEvents|メンバーは、イベントを発生させることができます。|  
|fdexPropCannotSourceEvents|メンバーはイベントを起動できません。|  
  
## <a name="return-value"></a>戻り値  
 次の値のいずれか。  
  
|値|意味|
|-|-|  
|`S_OK`|正常終了しました。|  
|`DISP_E_UNKNOWNNAME`|名前が不明です。|  
  
## <a name="example"></a>例  
  
```cpp
BSTR bstrName;  
   DISPID dispid;  
   IDispatchEx *pdex;   
   DWORD dwProps;  
  
   // Assign to pdex and bstrName  
   if (SUCCEEDED(pdex->GetDispID(bstrName, fdexNameCaseSensitive, &dispid)) &&  
      SUCCEEDED(pdex->GetMemberProperties(dispid, grfdexPropAll, &dwProps)) &&  
         (dwProps & fdexPropCanPut))  
   {  
      // Assign to member  
   }  
```  
  
## <a name="see-also"></a>関連項目  
 [IDispatchEx インターフェイス](../../winscript/reference/idispatchex-interface.md)   
 [IDispatchEx:: GetDispID](../../winscript/reference/idispatchex-getdispid.md)   
 [IDispatchEx::GetNextDispID](../../winscript/reference/idispatchex-getnextdispid.md)