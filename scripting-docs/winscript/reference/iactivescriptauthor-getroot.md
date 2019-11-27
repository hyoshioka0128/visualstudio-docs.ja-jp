---
title: 'IActiveScriptAuthor:: GetRoot |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptAuthor.GetRoot
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptAuthor::GetRoot
ms.assetid: 8e55a0c0-dd35-43d5-bf6f-e2f59c1e88d1
caps.latest.revision: 11
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: ca2aab154d56cd98c3c2acede61f86f725ce9c1b
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72576188"
---
# <a name="iactivescriptauthorgetroot"></a>IActiveScriptAuthor::GetRoot
作成者のスクリプトツリーの `IScriptNode` ルートを返します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT GetRoot(  
   IScriptNode        **ppsp  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `ppsp`  
 入出力ルートノードの `IScriptNode` インターフェイスへのポインターを受け取る変数のアドレス。  
  
## <a name="return-value"></a>戻り値  
 `HRESULT`。 有効な値を次の表に示しますが、これ以外にもあります。  
  
|値|説明|  
|-----------|-----------------|  
|`S_OK`|メソッドが成功しました。|  
  
## <a name="remarks"></a>コメント  
  
## <a name="see-also"></a>参照  
 [IActiveScriptAuthor インターフェイス](../../winscript/reference/iactivescriptauthor-interface.md)   
 [IScriptNode インターフェイス](../../winscript/reference/iscriptnode-interface.md)