---
title: ExtendedDebugPropertyInfo 構造体 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ExtendedDebugPropertyInfo
apilocation:
- scrobj.dll
helpviewer_keywords:
- ExtendedDebugPropertyInfo structure
ms.assetid: f2cf6477-454b-4d13-95da-ae4c90daa175
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 09f3c5a219fca9ec9b881e2ae8363aae4d48e03f
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72575836"
---
# <a name="extendeddebugpropertyinfo-structure"></a>ExtendedDebugPropertyInfo 構造体
拡張プロパティを特徴付けるように、追加のメンバーで `DebugPropertyInfo` 構造体を拡張します。  
  
## <a name="syntax"></a>構文  
  
```cpp
typedef struct ExtendedDebugPropertyInfo{  
   DBGPROP_INFO_FLAGS  dwValidFields;  
   LPOLESTR  bstrName;  
   LPOLESTR  bstrType;  
   LPOLESTR  bstrValue;  
   LPOLESTR  bstrFullName;  
   DBGPROP_ATTRIB_FLAGS  dwAttrib;  
   IDebugProperty*  pDebugProp;  
   DWORD  nDISPID;  
   DWORD  nType;  
   VARIANT  varValue;  
   ILockBytes*  plbValue;  
   IDebugExtendedProperty*  pDebugExtProp;  
};  
```  
  
## <a name="members"></a>メンバー  
 `dwValidFields`  
 初期化されるフィールドを指定するために使用される列挙データ型。  
  
 `bstrName`  
 コンテキスト内のプロパティ名。  
  
 `bstrType`  
 書式設定された文字列としてのプロパティの型。  
  
 `bstrValue`  
 書式設定された文字列としてのプロパティ値。  
  
 `bstrFullName`  
 プロパティの完全名。  
  
 `dwAttrib`  
 デバッグプロパティの属性のフラグを指定する列挙体。  
  
 `pDebugProp`  
 この `ExtendedDebugPropertyInfo`に対応する `IDebugProperty` オブジェクト。  
  
 `nDISPID`  
 ディスパッチ id。  
  
 `nType`  
 拡張プロパティの型。  
  
 `varValue`  
 拡張プロパティ値がバリアントに適合する場合は、その値。  
  
 `plbValue`  
 プロパティ値の実際のデータバイト。  
  
 `pDebugExtProp`  
 この `ExtendedDebugPropertyInfo`に対応する `IDebugExtendedProperty` オブジェクト。  
  
## <a name="see-also"></a>参照  
 [DebugPropertyInfo 構造体](../../winscript/reference/debugpropertyinfo-structure.md)   
 [IDebugProperty インターフェイス](../../winscript/reference/idebugproperty-interface.md)   
 [IDebugExtendedProperty インターフェイス](../../winscript/reference/idebugextendedproperty-interface.md)   
 [DBGPROP_ATTRIB_FLAGS](../../winscript/reference/dbgprop-attrib-flags.md)   
 [DBGPROP_INFO_FLAGS](../../winscript/reference/dbgprop-info-flags.md)