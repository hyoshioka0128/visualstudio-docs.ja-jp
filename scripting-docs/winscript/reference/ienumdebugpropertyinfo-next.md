---
title: 'IEnumDebugPropertyInfo:: Next |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IEnumDebugPropertyInfo.Next
apilocation:
- scrobj.dll
helpviewer_keywords:
- IEnumDebugPropertyInfo::Next
ms.assetid: 052837ac-1599-49cc-9a5a-ba90f992eeff
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: b99631c217ca56dce91512403dfb6623cd1e7641
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72574198"
---
# <a name="ienumdebugpropertyinfonext"></a>IEnumDebugPropertyInfo::Next
列挙シーケンス内の指定された数の `DebugPropertyInfo` 構造体を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT Next (  
   ULONGcelt,  
   DebugPropertyInfo*rgelt,  
   ULONG* pceltFetched  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `celt`  
 から取得する `DebugPropertyInfo`構造体の数。  
  
 `rgelt`  
 入出力取得した `DebugPropertyInfo` 構造体の配列。  
  
 `pceltFetched`  
 入出力実際に取得された `DebugPropertyInfo` 構造体の数を返します。  
  
## <a name="return-value"></a>戻り値  
 は、有効な `HRESULT`(通常は `S_OK`) を返します。  
  
## <a name="see-also"></a>参照  
 [IEnumDebugPropertyInfo インターフェイス](../../winscript/reference/ienumdebugpropertyinfo-interface.md)   
 [DebugPropertyInfo 構造体](../../winscript/reference/debugpropertyinfo-structure.md)