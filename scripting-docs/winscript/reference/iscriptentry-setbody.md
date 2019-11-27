---
title: 'IScriptEntry:: SetBody |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IScriptEntry.SetBody
apilocation:
- scrobj.dll
helpviewer_keywords:
- IScriptEntry::SetBody
ms.assetid: 719062e4-98e4-4a7b-946d-6e5dbbcc5225
caps.latest.revision: 12
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 1af865c8366481204ee413377a083b09d8c97383
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72575377"
---
# <a name="iscriptentrysetbody"></a>IScriptEntry::SetBody
`IScriptEntry` スクリプトブロックの本文またはスクリプトレットの `IScriptScriptlet` に含まれるテキストを設定します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT SetBody(  
   LPCOLESTR          psz  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `psz`  
 から`IScriptEntry` スクリプトブロックの場合、`psz` は、スクリプトタグで囲まれたテキストです。  
  
 `IScriptEntry` 関数ブロックの場合、`psz` は関数本体です。  
  
 `IScriptScriptlet` オブジェクト (`IScriptEntry`から派生) の場合、`psz` はスクリプトレットのスクリプトテキストです。  
  
## <a name="return-value"></a>戻り値  
 `HRESULT`。 有効な値を次の表に示しますが、これ以外にもあります。  
  
|値|説明|  
|-----------|-----------------|  
|`S_OK`|メソッドが成功しました。|  
  
## <a name="remarks"></a>コメント  
  
## <a name="see-also"></a>参照  
 [Iscriptentry インターフェイス](../../winscript/reference/iscriptentry-interface.md)   
 [IScriptEntry::GetBody](../../winscript/reference/iscriptentry-getbody.md)