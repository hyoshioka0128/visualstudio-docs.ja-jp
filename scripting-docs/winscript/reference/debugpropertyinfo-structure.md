---
title: DebugPropertyInfo 構造体 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- DebugPropertyInfo
apilocation:
- scrobj.dll
helpviewer_keywords:
- DebugPropertyInfo structure
ms.assetid: 3246efbc-c212-4024-8f07-6414c2f85e75
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 793c83b467460f0744abffe3f161f7510f56257a
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72575067"
---
# <a name="debugpropertyinfo-structure"></a>DebugPropertyInfo 構造体
名前、型、および値を持つ階層的な性質を持つオブジェクトを記述します。 ローカル変数、パラメーター、ウォッチ変数と式、およびレジスタのデバッグプロパティを記述するために使用されます。  
  
## <a name="syntax"></a>構文  
  
```cpp
typedef struct DebugPropertyInfo{  
   DBGPROP_INFO_FLAGS  dwValidFields;  
   BSTR  bstrName;  
   BSTR  bstrType;  
   BSTR  bstrValue;  
   BSTR  bstrFullName;  
   DBGPROP_ATTRIB_FLAGS  dwAttrib;  
   IDebugProperty*  pDebugProp;  
};  
```  
  
## <a name="members"></a>メンバー  
 dwValidFields  
 初期化されるフィールドを指定するために使用される列挙データ型。  
  
 bstrName  
 コンテキスト内のプロパティ名。  
  
 bstrType  
 プロパティの型を書式設定された文字列として指定します。  
  
 bstrValue  
 書式設定された文字列としてのプロパティ値。  
  
 bstrFullName  
 プロパティの完全名。  
  
 dwAttrib  
 デバッグプロパティの属性のフラグを指定する列挙体。  
  
 pDebugProp  
 この `DebugPropertyInfo` 構造体の情報によって記述された `IDebugProperty`。  
  
## <a name="see-also"></a>参照  
 [IDebugProperty インターフェイス](../../winscript/reference/idebugproperty-interface.md)   
 [DBGPROP_ATTRIB_FLAGS](../../winscript/reference/dbgprop-attrib-flags.md)   
 [DBGPROP_INFO_FLAGS](../../winscript/reference/dbgprop-info-flags.md)