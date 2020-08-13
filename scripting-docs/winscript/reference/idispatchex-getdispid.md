---
title: 'IDispatchEx:: GetDispID |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDispatchEx.GetDispID
apilocation:
- scrobj.dll
helpviewer_keywords:
- GetDispID method
ms.assetid: a288d63d-b08a-4540-9d9d-0bcd182eff9a
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 81bb33a1e793f38e15dc51b37c4fa062eb54e7fa
ms.sourcegitcommit: d281d2a04a5bc302650eebf369946d8f101e59dd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "88144534"
---
# <a name="idispatchexgetdispid"></a>IDispatchEx::GetDispID
1つのメンバー名を対応する DISPID にマップします。これは、後続のへの呼び出しで使用でき `IDispatchEx::InvokeEx` ます。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT GetDispID(  
   BSTR bstrName,  
   DWORD grfdex,  
   DISPID *pid  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `bstrName`  
 マップされる名前が渡されました。  
  
 `grfdex`  
 メンバー識別子を取得するためのオプションを決定します。 次の値の組み合わせを指定できます。  
  
|値|意味|  
|-----------|-------------|  
|fdexNameCaseSensitive|大文字と小文字を区別する方法で名前の参照を実行するように要求します。 大文字と小文字を区別する検索をサポートしていないオブジェクトによって無視される場合があります。|  
|fdexNameEnsure|メンバーが存在しない場合に作成されることを要求します。 新しいメンバーは、値を使用して作成する必要があり `VT_EMPTY` ます。|  
|fdexNameImplicit|ベースオブジェクトが明示的に指定されていない場合に、呼び出し元が特定の名前のメンバーのオブジェクトを検索していることを示します。|  
|fdexNameCaseInsensitive|大文字と小文字を区別せずに名前参照を実行するように要求します。 大文字と小文字を区別しない検索をサポートしていないオブジェクトによって無視される場合があります。|  
  
 `pid`  
 DISPID の結果を受信するために、呼び出し元に割り当てられた場所へのポインター。 エラーが発生した場合、には `pid` DISPID_UNKNOWN が含まれます。  
  
## <a name="return-value"></a>戻り値  
 次の値のいずれか。  
  
|値|意味|
|-|-|  
|`S_OK`|正常終了しました。|  
|`E_OUTOFMEMORY`|メモリが不足しています。|  
|`DISP_E_UNKNOWNNAME`|名前が不明です。|  
  
## <a name="remarks"></a>解説  
 `GetDispID`は、指定され `GetIDsOfNames` たメンバーの DISPID を取得するために、の代わりに使用できます。  
  
 では、 `IDispatchEx` メンバーの追加と削除が許可されているので、オブジェクトの有効期間中は dispid のセットが一定のままになりません。  
  
 の使用 `riid` されていないパラメーターは `IDispatch::GetIDsOfNames` 削除されました。  
  
## <a name="example"></a>例  
  
```cpp
BSTR bstrName;  
   DISPID dispid;  
   IDispatchEx *pdex;   
  
   // Assign to pdex and bstrName  
   pdex->GetDispID(bstrName, fdexNameCaseSensitive, &dispid);  
   // Use dispid  
```  
  
## <a name="see-also"></a>関連項目  
 [IDispatchEx インターフェイス](../../winscript/reference/idispatchex-interface.md)