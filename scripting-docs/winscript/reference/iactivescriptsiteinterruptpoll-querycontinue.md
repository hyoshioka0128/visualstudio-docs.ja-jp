---
title: 'IActiveScriptSiteInterruptPoll:: QueryContinue |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptSiteInterruptPoll.QueryContinue
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptSiteInterruptPoll::QueryContinue
ms.assetid: 41ac3807-f8b4-4a0e-bcc6-556bc89f3904
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 7ce2ad61b54dce510035dd8e97d0dfb2accbf7a7
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72572238"
---
# <a name="iactivescriptsiteinterruptpollquerycontinue"></a>IActiveScriptSiteInterruptPoll::QueryContinue
スクリプトを終了する必要があることをホストが指定できるようにします。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT QueryContinue();  
```  
  
#### <a name="parameters"></a>パラメーター  
 このメソッドはパラメーターを受け取りません。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは `HRESULT` を返します。 有効な値を次の表に示しますが、これ以外にもあります。  
  
|値|説明|  
|-----------|-----------------|  
|`S_OK`|呼び出しは成功し、ホストはスクリプトの実行を続行できるようにします。|  
|`S_FALSE`|呼び出しは成功し、ホストはスクリプトを終了するように要求します。|  
  
## <a name="remarks"></a>コメント  
 `QueryContinue` メソッドの戻り値が `S_OK`でない限り、ホストされているスクリプトは終了します。 `S_FALSE` の戻り値は、ホストがスクリプトを終了するように明示的に要求することを示します。  
  
 マルチスレッドホストでは、`IActiveScript::InterruptScriptThread` メソッドを使用してスクリプトを終了できます。  
  
## <a name="see-also"></a>参照  
 [IActiveScriptSiteInterruptPoll インターフェイス](../../winscript/reference/iactivescriptsiteinterruptpoll-interface.md)   
 [IActiveScript::InterruptScriptThread](../../winscript/reference/iactivescript-interruptscriptthread.md)