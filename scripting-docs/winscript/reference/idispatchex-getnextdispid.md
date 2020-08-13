---
title: 'IDispatchEx:: GetNextDispID |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDispatchEx.GetNextDispID
apilocation:
- scrobj.dll
helpviewer_keywords:
- GetNextDispID method
ms.assetid: 8263d441-85ee-47f4-bdba-fbf2ad07e85f
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 8811e828a6701769badf45ca7c37f9c53529150f
ms.sourcegitcommit: d281d2a04a5bc302650eebf369946d8f101e59dd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "88144430"
---
# <a name="idispatchexgetnextdispid"></a>IDispatchEx::GetNextDispID

オブジェクトのメンバーを列挙します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetNextDispID(
   DWORD grfdex,
   DISPID id,
   DISPID *pid
);
```

## <a name="parameters"></a>パラメーター

`grfdex`\
列挙する項目のセットを決定します。 次の値の組み合わせを指定できます。

|値|意味|
|-----------|-------------|
|fdexEnumDefault|オブジェクトが既定の要素を列挙することを要求します。 オブジェクトは、要素の任意のセットを列挙できます。|
|fdexEnumAll|オブジェクトがすべての要素を列挙することを要求します。 オブジェクトは、要素の任意のセットを列挙できます。|

`id`\
現在のメンバーを識別します。 GetNextDispID は、この後の列挙体の項目を取得します。 では、GetDispID または GetNextDispID への以前の呼び出しを使用して、この識別子を取得します。 DISPID_STARTENUM 値を使用して、最初の項目の最初の識別子を取得します。

`pid`\
列挙体の次の項目の識別子を受け取る DISPID 変数のアドレス。

メンバーがまたはによって削除された場合、はに `DeleteMemberByName` `DeleteMemberByDispID` 対して `DISPID` 有効なままである必要があり `GetNextDispID` ます。

## <a name="return-value"></a>戻り値

次の値のいずれか。

|値|意味|
|-|-|
|`S_OK`|正常終了しました。|
|`S_FALSE`|列挙が行われます。|

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

- [IDispatchEx インターフェイス](../../winscript/reference/idispatchex-interface.md)
- [IDispatchEx::GetDispID](../../winscript/reference/idispatchex-getdispid.md)
- [IDispatchEx::DeleteMemberByName](../../winscript/reference/idispatchex-deletememberbyname.md)
- [IDispatchEx::DeleteMemberByDispID](../../winscript/reference/idispatchex-deletememberbydispid.md)