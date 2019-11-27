---
title: 'IDebugProperty:: EnumMembers |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugProperty.EnumMembers
apilocation:
- scrobj.dll
helpviewer_keywords:
- IDebugProperty::EnumMembers
ms.assetid: 8ce398a5-6452-4804-ae8f-5c54cd11c661
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 5f8c5f2cbb107d55e9ffe602cb7d3492701de10c
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72562423"
---
# <a name="idebugpropertyenummembers"></a>IDebugProperty::EnumMembers
プロパティのメンバーを列挙します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT EnumMembers (  
   DBGPROP_INFO_FLAGSdwFieldSpec,  
   UINTnRadix,  
   REFIIDrefiid,  
   IEnumDebugPropertyInfo**ppEnum  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `dwFieldSpec`  
 から列挙されたデバッグプロパティ構造内のどのフィールドに入力するかを決定する `DBGPROP_INFO_FLAGS` 定数を指定します。  
  
 `nRadix`  
 から数値情報の解釈に使用される基数。  
  
 `refiid`  
 からこの IID は、列挙子をフィルター処理するために渡されます。 IID は、`IDebugPropertyEnumType_All`から継承する `IDebugPropertyEnumType` インターフェイスの1つです。  
  
 `ppEnum`  
 入出力メンバープロパティを列挙する `IEnumDebugPropertyInfo` インターフェイスを返します。  
  
## <a name="return-value"></a>戻り値  
 は、有効な `HRESULT`(通常は `S_OK`) を返します。  
  
## <a name="see-also"></a>参照  
 [IDebugProperty インターフェイス](../../winscript/reference/idebugproperty-interface.md)   
 [DBGPROP_INFO_FLAGS](../../winscript/reference/dbgprop-info-flags.md)   
 [IDebugPropertyEnumType_All インターフェイス](../../winscript/reference/idebugpropertyenumtype-all-interface.md)   
 [IEnumDebugPropertyInfo インターフェイス](../../winscript/reference/ienumdebugpropertyinfo-interface.md)