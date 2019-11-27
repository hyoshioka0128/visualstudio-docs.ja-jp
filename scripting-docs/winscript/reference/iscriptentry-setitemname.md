---
title: 'IScriptEntry:: SetItemName |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IScriptEntry.SetItemName
apilocation:
- scrobj.dll
helpviewer_keywords:
- IScriptEntry::SetItemName
ms.assetid: 9551a7ec-38f8-466a-9722-09367763f380
caps.latest.revision: 11
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 7ba226704f5b064c86b52c1b349650d509b2b549
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72575366"
---
# <a name="iscriptentrysetitemname"></a>IScriptEntry::SetItemName
`IScriptEntry` オブジェクトを識別する項目の名前を設定します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT SetItemName(  
   LPCOLESTR          psz  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `psz`  
 から項目名を格納しているバッファーのアドレス。 項目名は、エントリを識別するためにホストによって使用されます。  
  
## <a name="return-value"></a>戻り値  
 `HRESULT`。 有効な値を次の表に示しますが、これ以外にもあります。  
  
|値|説明|  
|-----------|-----------------|  
|`S_OK`|メソッドが成功しました。|  
|`E_FAIL`|メソッドは成功しませんでした。|  
  
## <a name="remarks"></a>コメント  
 `IScriptEntry` オブジェクトの場合、このメソッドは `S_OK`を返します。  
  
 `IScriptScriptlet` オブジェクト (`IScriptEntry`から派生) の場合、このメソッドは `E_FAIL`を返します。 `IScriptScriptlet` オブジェクトの場合、項目名は[IActiveScriptAuthor:: AddScriptlet](../../winscript/reference/iactivescriptauthor-addscriptlet.md)によって設定され、変更することはできません。  
  
## <a name="see-also"></a>参照  
 [Iscriptentry インターフェイス](../../winscript/reference/iscriptentry-interface.md)   
 [IScriptEntry::GetItemName](../../winscript/reference/iscriptentry-getitemname.md)