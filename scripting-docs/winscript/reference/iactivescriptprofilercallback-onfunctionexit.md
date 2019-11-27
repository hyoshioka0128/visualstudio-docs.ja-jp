---
title: 'IActiveScriptProfilerCallback:: OnFunctionExit |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptProfilerCallback.OnFunctionExit
apilocation:
- scrobj.dll
ms.assetid: a5d21715-2b0b-423e-8644-f04a9e7cde3d
caps.latest.revision: 9
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 87801b7873e43498031264ff4719fb47eca99f40
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72571672"
---
# <a name="iactivescriptprofilercallbackonfunctionexit"></a>IActiveScriptProfilerCallback::OnFunctionExit
スクリプトエンジンがドキュメントオブジェクトモデル (DOM) への呼び出しではない関数呼び出しの実行を終了したことをプロファイラーオブジェクトに通知します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT OnFunctionExit(  
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
 DOM 呼び出しの場合、スクリプトエンジンは `IActiveScriptProfilerCallback::OnFunctionExit`ではなく[IActiveScriptProfilerCallback2:: OnFunctionExitByName](../../winscript/reference/iactivescriptprofilercallback2-onfunctionexitbyname.md)を呼び出します。 これは、DOM 内の一意のメソッドとプロパティの数が多いためです。  
  
## <a name="see-also"></a>参照  
 [IActiveScriptProfilerCallback::OnFunctionEnter](../../winscript/reference/iactivescriptprofilercallback-onfunctionenter.md)   
 [IActiveScriptProfilerCallback インターフェイス](../../winscript/reference/iactivescriptprofilercallback-interface.md)