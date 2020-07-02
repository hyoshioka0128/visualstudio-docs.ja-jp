---
title: 'IActiveScriptSiteDebug32:: GetApplication |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 533d770d-06a4-4693-873e-255c9c6f0df0
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
ms.openlocfilehash: 0b82ab6cd37f789e98ca08c635011a7e04f5b871
ms.sourcegitcommit: 9a9c61ca115c22d33bb902153eb0853789c7be4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85835629"
---
# <a name="iactivescriptsitedebug32getapplication"></a>IActiveScriptSiteDebug32::GetApplication
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
  
|[値]|説明|  
|-----------|-----------------|  
|`S_OK`|メソッドが成功しました。|  
|`E_NOTIMPL`|ホストはデバッグを直接サポートしていません。|  
  
## <a name="remarks"></a>Remarks  
 メソッドは、 `GetApplication` スマートホストが各スクリプトが属するアプリケーションオブジェクトを定義する方法を提供します。 スクリプトエンジンは、含まれているアプリケーションを取得するために、このメソッドの呼び出しを試みる必要があり `IProcessDebugManager::GetDefaultApplication` ます。これが失敗した場合は、にアクセスします。  
  
## <a name="see-also"></a>関連項目  
 [IActiveScriptSiteDebug32 インターフェイス](../../winscript/reference/iactivescriptsitedebug32-interface.md)   
 [IProcessDebugManager::GetDefaultApplication](../../winscript/reference/iprocessdebugmanager-getdefaultapplication.md)