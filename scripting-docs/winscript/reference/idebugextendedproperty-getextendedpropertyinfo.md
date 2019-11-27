---
title: 'IDebugExtendedProperty:: GetExtendedPropertyInfo |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugExtendedProperty.GetExtendedPropertyInfo
apilocation:
- scrobj.dll
helpviewer_keywords:
- IDebugExtendedProperty::GetExtendedPropertyInfo
ms.assetid: 56edf538-5082-4653-82b6-e6640d6f61ba
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 77167c46e02bcf2bf5d3ce5836ad5de103176e93
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72576384"
---
# <a name="idebugextendedpropertygetextendedpropertyinfo"></a>IDebugExtendedProperty::GetExtendedPropertyInfo
拡張プロパティの拡張情報をフェッチします。これは、より単純な `IDebugProperty`よりも詳細な情報です。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT GetExtendedPropertyInfo(  
   EX_DBGPROP_INFO_FLAGS  dwFieldSpec,  
   UINT  nRadix,  
   ExtendedDebugPropertyInfo*  pExtendedPropertyInfo  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `dwFieldSpec`  
 から`ExtendedDebugPropertyInfo` 構造体に入力するフィールドを決定する EX_DBGPROP_INFO_FLAGS 定数を指定します。  
  
 `nRadix`  
 から数値情報の解釈に使用される基数。  
  
 `pExtendedPropertyInfo`  
 入出力プロパティを記述する `ExtendedDebugPropertyInfo` 構造体を返します。  
  
## <a name="return-value"></a>戻り値  
 は、有効な `HRESULT`(通常は `S_OK`) を返します。  
  
## <a name="see-also"></a>参照  
 [IDebugExtendedProperty インターフェイス](../../winscript/reference/idebugextendedproperty-interface.md)   
 [EX_DBGPROP_INFO_FLAGS](../../winscript/reference/ex-dbgprop-info-flags.md)   
 [ExtendedDebugPropertyInfo 構造体](../../winscript/reference/extendeddebugpropertyinfo-structure.md)