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
ms.openlocfilehash: 8016eef7b6e0da9b9fc88695db845cba7f608ff3
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72574095"
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
 メンバーを識別します。 `GetDispID` または `GetNextDispID` を使用してディスパッチ識別子を取得します。  
  
 `grfdexFetch`  
 取得するプロパティを決定します。 これには、`pgrfdex` の下に一覧表示された値の組み合わせ、または次の値の組み合わせを使用できます。  
  
|値|意味|  
|-----------|-------------|  
|grfdexPropCanAll|FdexPropCanGet、fdexPropCanPut、fdexPropCanPutRef、fdexPropCanCall、fdexPropCanConstruct、および Fdexpropcanget を結合します。|  
|grfdexPropCannotAll|FdexPropCannotGet、fdexPropCannotPut、fdexPropCannotPutRef、fdexPropCannotCall、fdexPropCannotConstruct、fdexPropCannotSourceEvents を結合します。|  
|grfdexPropExtraAll|FdexPropNoSideEffects と fdexPropDynamicType を結合します。|  
|grfdexPropAll|GrfdexPropCanAll、grfdexPropCannotAll、および grfdexPropExtraAll を結合します。|  
  
 `pgrfdex`  
 要求されたプロパティを受け取る `DWORD` のアドレス。 次の値の組み合わせを指定できます。  
  
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
 次のいずれかの値を返します。  
  
|||  
|-|-|  
|`S_OK`|成功。|  
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
  
## <a name="see-also"></a>参照  
 [IDispatchEx インターフェイス](../../winscript/reference/idispatchex-interface.md)   
 [IDispatchEx::GetDispID](../../winscript/reference/idispatchex-getdispid.md)   
 [IDispatchEx::GetNextDispID](../../winscript/reference/idispatchex-getnextdispid.md)