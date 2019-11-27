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
ms.openlocfilehash: 38ead33fb51caff1103ca9abe6bc01f3e0aa6aa3
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72576637"
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
 メンバー識別子。 `GetDispID` または `GetNextDispID` を使用してディスパッチ識別子を取得します。  
  
## <a name="return-value"></a>戻り値  
 次のいずれかの値を返します。  
  
|||  
|-|-|  
|`S_OK`|成功。|  
|`S_FALSE`|メンバーは存在しますが、削除できません。|  
  
## <a name="remarks"></a>コメント  
 メンバーが削除された場合、DISPID は `GetNextDispID`に対して有効なままである必要があります。  
  
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
  
## <a name="see-also"></a>参照  
 [IDispatchEx インターフェイス](../../winscript/reference/idispatchex-interface.md)   
 [IDispatchEx::GetDispID](../../winscript/reference/idispatchex-getdispid.md)   
 [IDispatchEx::GetNextDispID](../../winscript/reference/idispatchex-getnextdispid.md)