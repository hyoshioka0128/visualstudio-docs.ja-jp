---
title: 'IActiveScriptProfilerCallback:: OnFunctionEnter |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptProfilerCallback.OnFunctionEnter
apilocation:
- scrobj.dll
ms.assetid: 12dab2b4-df4e-444d-99cb-25e1c278e6e8
caps.latest.revision: 9
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 6157638353712d6f376fa1eb46a68980b493a5c3
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72571689"
---
# <a name="iactivescriptprofilercallbackonfunctionenter"></a>IActiveScriptProfilerCallback::OnFunctionEnter
スクリプトエンジンがドキュメントオブジェクトモデル (DOM) への呼び出しではない関数呼び出しを実行しようとしていることをプロファイラーオブジェクトに通知します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT OnFunctionEnter(  
    [in] PROFILER_TOKEN scriptId,   
    [in] PROFILER_TOKEN functionId);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `scriptId`  
 から関数が含まれているスクリプトの一意の ID。 この ID は、スクリプトエンジンによって割り当てられます。  
  
 `functionId`  
 から関数の一意の ID。 この ID は、スクリプトエンジンによって割り当てられます。  
  
## <a name="return-value"></a>戻り値  
 このメソッドの戻り値は、スクリプトエンジンによって無視されます。  
  
## <a name="remarks"></a>コメント  
 DOM 呼び出しの場合、スクリプトエンジンは `IActiveScriptProfilerCallback::OnFunctionEnter`ではなく[IActiveScriptProfilerCallback2:: OnFunctionEnterByName](../../winscript/reference/iactivescriptprofilercallback2-onfunctionenterbyname.md)を呼び出します。 これは、DOM 内の一意のメソッドとプロパティの数が多いためです。  
  
## <a name="see-also"></a>参照  
 [IActiveScriptProfilerCallback:: OnFunctionExit](../../winscript/reference/iactivescriptprofilercallback-onfunctionexit.md)   
 [IActiveScriptProfilerCallback インターフェイス](../../winscript/reference/iactivescriptprofilercallback-interface.md)