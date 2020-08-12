---
title: IDispatchEx::D eleteMemberByDispID |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDispatchEx.DeleteMemberByDispID
apilocation:
- scrobj.dll
helpviewer_keywords:
- DeleteMemberByDispID method
ms.assetid: f61231e5-ba93-4ac3-bde8-d363548356b3
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 0c3dbb040e39fd15b77e42b2eaa9fb2cdda0b1b2
ms.sourcegitcommit: d281d2a04a5bc302650eebf369946d8f101e59dd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "88144637"
---
# <a name="idispatchexdeletememberbydispid"></a>IDispatchEx::DeleteMemberByDispID
メンバーを DISPID で削除します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT DeleteMemberByDispID(  
    DISPID id  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `id`  
 メンバー識別子。 `GetDispID`は、またはを使用し `GetNextDispID` てディスパッチ識別子を取得します。  
  
## <a name="return-value"></a>戻り値  
 次の値のいずれか。  
  
|値|意味|
|-|-|  
|`S_OK`|正常終了しました。|  
|`S_FALSE`|メンバーは存在しますが、削除できません。|  
  
## <a name="remarks"></a>解説  
 メンバーが削除された場合、DISPID はに対して有効なままである必要があり `GetNextDispID` ます。  
  
 指定された名前のメンバーが削除され、後で同じ名前のメンバーが再作成される場合、DISPID は同じである必要があります。 (大文字と小文字のみが異なるメンバー名が "同じ" であるかどうかは、オブジェクトに依存します)。  
  
## <a name="example"></a>例  
  
```cpp
BSTR bstrName;  
DISPID dispid;  
IDispatchEx *pdex;   
  
// Assign to pdex and bstrName  
if (SUCCEEDED(pdex->GetDispID(bstrName, fdexNameCaseSensitive, &dispid)))  
    pdex->DeleteMemberByDispID(dispid);  
```  
  
## <a name="see-also"></a>関連項目  
 [IDispatchEx インターフェイス](../../winscript/reference/idispatchex-interface.md)   
 [IDispatchEx:: GetDispID](../../winscript/reference/idispatchex-getdispid.md)   
 [IDispatchEx::GetNextDispID](../../winscript/reference/idispatchex-getnextdispid.md)