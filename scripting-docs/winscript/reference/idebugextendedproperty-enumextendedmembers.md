---
title: 'IDebugExtendedProperty:: EnumExtendedMembers |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugExtendedProperty.EnumExtendedMembers
apilocation:
- scrobj.dll
helpviewer_keywords:
- IDebugExtendedProperty::EnumExtendedMembers
ms.assetid: 27cdb091-da4e-44d2-a631-31ae00468b98
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: f6fd225be9504254965eab77b912f50fb5c777e3
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72576391"
---
# <a name="idebugextendedpropertyenumextendedmembers"></a>IDebugExtendedProperty::EnumExtendedMembers
拡張プロパティのメンバーを列挙します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT EnumExtendedMembers(  
   EX_DBGPROP_INFO_FLAGS  dwFieldSpec,  
   UINT  nRadix,  
   IEnumDebugExtendedPropertyInfo**  ppeepi  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `dwFieldSpec`  
 から入力する、列挙された拡張デバッグプロパティ構造内のフィールドを決定する EX_DBGPROP_INFO_FLAGS 定数を指定します。  
  
 `nRadix`  
 から数値情報の解釈に使用される基数。  
  
 `ppeepi`  
 入出力メンバープロパティを列挙する `IEnumDebugExtendedPropertyInfo` インターフェイスを返します。  
  
## <a name="return-value"></a>戻り値  
 は、有効な `HRESULT`(通常は `S_OK`) を返します。  
  
## <a name="see-also"></a>参照  
 [IDebugExtendedProperty インターフェイス](../../winscript/reference/idebugextendedproperty-interface.md)   
 [EX_DBGPROP_INFO_FLAGS](../../winscript/reference/ex-dbgprop-info-flags.md)   
 [ExtendedDebugPropertyInfo 構造体](../../winscript/reference/extendeddebugpropertyinfo-structure.md)