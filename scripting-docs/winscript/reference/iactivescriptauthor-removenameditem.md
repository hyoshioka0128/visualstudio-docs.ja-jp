---
title: 'IActiveScriptAuthor:: RemoveNamedItem |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptAuthor.RemoveNamedItem
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptAuthor::RemoveNamedItem
ms.assetid: 1173ef46-39a5-4bc1-8e0c-89259a16be16
caps.latest.revision: 14
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: cade532d2ca276237981855cafe12804307d0bb6
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72572848"
---
# <a name="iactivescriptauthorremovenameditem"></a>IActiveScriptAuthor::RemoveNamedItem
スクリプト作成エンジンの名前空間から `NamedItem` オブジェクトを削除します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT RemoveNamedItem(  
   LPCOLESTR          pszName  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pszName`  
 から削除する `NamedItem` オブジェクトを識別するバッファーのアドレス。  
  
## <a name="return-value"></a>戻り値  
 `HRESULT`。 有効な値を次の表に示しますが、これ以外にもあります。  
  
|値|説明|  
|-----------|-----------------|  
|`S_OK`|メソッドが成功しました。|  
|`S_FALSE`|`NamedItem` オブジェクトは、スクリプト作成エンジンの名前空間に存在しません。|  
  
## <a name="remarks"></a>コメント  
 [IActiveScript:: AddNamedItem](../../winscript/reference/iactivescript-addnameditem.md)は、スクリプト作成エンジンの名前空間に `NamedItem` オブジェクトを挿入するために使用されます。  
  
## <a name="see-also"></a>参照  
 [IActiveScriptAuthor インターフェイス](../../winscript/reference/iactivescriptauthor-interface.md)   
 [IActiveScriptAuthor::AddNamedItem](../../winscript/reference/iactivescriptauthor-addnameditem.md)