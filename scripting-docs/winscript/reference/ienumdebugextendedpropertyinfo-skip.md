---
title: 'IEnumDebugExtendedPropertyInfo:: Skip |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IEnumDebugExtendedPropertyInfo.Skip
apilocation:
- scrobj.dll
helpviewer_keywords:
- IEnumDebugExtendedPropertyInfo::Skip
ms.assetid: a0b4a9fc-e122-482b-9384-b83c460b61fe
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 8e5c187f3484154a2758b67300c98d4cb9fc9023
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72574238"
---
# <a name="ienumdebugextendedpropertyinfoskip"></a>IEnumDebugExtendedPropertyInfo::Skip
列挙シーケンス内の指定された数の `ExtendedDebugPropertyInfo` 構造体をスキップします。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT Skip(  
   ULONG celt  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `celt`  
 からスキップする列挙シーケンス内の `ExtendedDebugPropertyInfo` 構造体の数。  
  
## <a name="return-value"></a>戻り値  
 は、有効な `HRESULT`(通常は `S_OK`) を返します。 は `S_FALSE` を返し、`celt` が列挙子に残されている要素の数より大きい場合は、現在の要素ポインターを列挙体の末尾に設定します。  
  
## <a name="see-also"></a>参照  
 [IEnumDebugExtendedPropertyInfo インターフェイス](../../winscript/reference/ienumdebugextendedpropertyinfo-interface.md)   
 [ExtendedDebugPropertyInfo 構造体](../../winscript/reference/extendeddebugpropertyinfo-structure.md)