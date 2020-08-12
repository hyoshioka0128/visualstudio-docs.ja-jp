---
title: IDispatchEx::D eleteMemberByName |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDispatchEx.DeleteMemberByName
apilocation:
- scrobj.dll
helpviewer_keywords:
- DeleteMemberByName method
ms.assetid: a01b4e6a-d989-4b29-bb3f-04554f8c39f7
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: cf62972b192d73bd130d15066d79ea70fe24beb8
ms.sourcegitcommit: d281d2a04a5bc302650eebf369946d8f101e59dd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "88144598"
---
# <a name="idispatchexdeletememberbyname"></a>IDispatchEx::DeleteMemberByName
メンバーを名前で削除します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT DeleteMemberByName(  
   BSTR bstrName,  
   DWORD grfdex  
  
```  
  
#### <a name="parameters"></a>パラメーター  
 `bstrName`  
 削除するメンバーの名前。  
  
 `grfdex`  
 メンバー名で大文字と小文字を区別するかどうかを指定します。 次のいずれかの値を指定できます。  
  
|値|意味|  
|-----------|-------------|  
|fdexNameCaseSensitive|大文字と小文字を区別する方法で名前の参照を実行するように要求します。 大文字と小文字を区別する検索をサポートしていないオブジェクトによって無視される可能性があります。|  
|fdexNameCaseInsensitive|大文字と小文字を区別せずに名前参照を実行するように要求します。 大文字と小文字を区別しない検索をサポートしていないオブジェクトによって無視される可能性があります。|  
  
## <a name="return-value"></a>戻り値  
 次の値のいずれか。  
  
|値|意味|
|-|-|  
|`S_OK`|正常終了しました。|  
|`S_FALSE`|メンバーは存在しますが、削除できません。|  
  
## <a name="remarks"></a>解説  
 メンバーが削除された場合、DISPID はに対して有効なままである必要があり `GetNextDispID` ます。  
  
 指定された名前のメンバーが削除され、後で同じ名前のメンバーが再作成される場合、DISPID は同じである必要があります。 (大文字と小文字のみが異なるメンバーが "同じ" であるかどうかは、オブジェクトに依存します)。  
  
## <a name="example"></a>例  
  
```cpp
BSTR bstrName;  
IDispatchEx *pdex;  
  
// Assign to pdex and bstrName  
pdex->DeleteMemberByName(bstrName, fdexNameCaseSensitive);  
```  
  
## <a name="see-also"></a>関連項目  
 [IDispatchEx インターフェイス](../../winscript/reference/idispatchex-interface.md)