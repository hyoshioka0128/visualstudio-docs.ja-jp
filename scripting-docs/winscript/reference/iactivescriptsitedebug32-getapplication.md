---
title: 'IActiveScriptSiteDebug32:: GetApplication |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 533d770d-06a4-4693-873e-255c9c6f0df0
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
ms.openlocfilehash: 93c4a8fe6e5c2aac8b07f896810dcd03060b46d0
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72572201"
---
# <a name="iactivescriptsitedebug32getapplication"></a>IActiveScriptSiteDebug32:: GetApplication
このスクリプトサイトに関連付けられているデバッグアプリケーションオブジェクトを返します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT GetApplication(  
   IDebugApplication**  ppda  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `ppda`  
 入出力スクリプトサイトに関連付けられているデバッグアプリケーションオブジェクトへのポインター。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは `HRESULT` を返します。 有効な値を次の表に示しますが、これ以外にもあります。  
  
|値|説明|  
|-----------|-----------------|  
|`S_OK`|メソッドが成功しました。|  
|`E_NOTIMPL`|ホストはデバッグを直接サポートしていません。|  
  
## <a name="remarks"></a>コメント  
 `GetApplication` メソッドは、スマートホストが各スクリプトが属するアプリケーションオブジェクトを定義する方法を提供します。 スクリプトエンジンは、このメソッドを呼び出して、含まれているアプリケーションを取得し、失敗した場合に `IProcessDebugManager::GetDefaultApplication` できるようにする必要があります。  
  
## <a name="see-also"></a>参照  
 [IActiveScriptSiteDebug32 インターフェイス](../../winscript/reference/iactivescriptsitedebug32-interface.md)   
 [IProcessDebugManager::GetDefaultApplication](../../winscript/reference/iprocessdebugmanager-getdefaultapplication.md)