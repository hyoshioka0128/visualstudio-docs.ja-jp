---
title: 'IActiveScriptProfilerCallback2:: OnFunctionExitByName |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IActiveScriptProfilerCallback2::OnFunctionExitByName
ms.assetid: a6ddead4-e66d-4789-b778-84e5c343f908
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: a70bc72dd1070759ad8b78e43926f06a2c56ec15
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72571625"
---
# <a name="iactivescriptprofilercallback2onfunctionexitbyname"></a>IActiveScriptProfilerCallback2::OnFunctionExitByName
スクリプトエンジンがドキュメントオブジェクトモデル (DOM) 関数呼び出しの実行を終了したことをプロファイラーオブジェクトに通知します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT OnFunctionExitByName(  
    [in] [string] const WCHAR *pwszFunctionName,  
    [in] PROFILER_SCRIPT_TYPE scriptType);  
  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pwszFunctionName`  
 からスクリプトエンジンが実行を終了した関数の名前。  
  
 `scriptType`  
 から関数の型。 有効な値の説明については、「 [PROFILER_SCRIPT_TYPE 列挙型](../../winscript/reference/profiler-script-type-enumeration.md)」を参照してください。  
  
## <a name="return-value"></a>戻り値  
 このメソッドの戻り値は、スクリプトエンジンによって無視されます。  
  
## <a name="remarks"></a>コメント  
 DOM 呼び出しの場合、スクリプトエンジンは[IActiveScriptProfilerCallback:: OnFunctionExit](../../winscript/reference/iactivescriptprofilercallback-onfunctionexit.md)を呼び出すのではなく、このメソッドを呼び出します。 これは、DOM 内の一意のメソッドとプロパティの数が多いためです。  
  
## <a name="see-also"></a>参照  
 [IActiveScriptProfilerCallback2::OnFunctionEnterByName](../../winscript/reference/iactivescriptprofilercallback2-onfunctionenterbyname.md)   
 [IActiveScriptProfilerCallback2 インターフェイス](../../winscript/reference/iactivescriptprofilercallback2-interface.md)