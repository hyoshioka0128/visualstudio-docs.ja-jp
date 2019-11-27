---
title: PROFILER_SCRIPT_TYPE 列挙型 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- PROFILER_SCRIPT_TYPE
apilocation:
- scrobj.dll
ms.assetid: 3ab6633a-6241-44f0-b837-14336f70c71e
caps.latest.revision: 11
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: e08583f9bb914adfbd144715646991c6070f3f32
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72574572"
---
# <a name="profiler_script_type-enumeration"></a>PROFILER_SCRIPT_TYPE 列挙型
スクリプトの種類を指定します。  
  
## <a name="syntax"></a>構文  
  
```cpp
typedef enum {  
    PROFILER_SCRIPT_TYPE_USER,  
    PROFILER_SCRIPT_TYPE_DYNAMIC,  
    PROFILER_SCRIPT_TYPE_NATIVE,  
    PROFILER_SCRIPT_TYPE_DOM  
} PROFILER_SCRIPT_TYPE;  
```  
  
## <a name="members"></a>メンバー  
  
|メンバー|説明|  
|------------|-----------------|  
|PROFILER_SCRIPT_TYPE_USER|ユーザーが記述したスクリプトコードを指定します。|  
|PROFILER_SCRIPT_TYPE_DYNAMIC|実行中に動的に生成されるスクリプトコードを指定します。|  
|PROFILER_SCRIPT_TYPE_NATIVE|スクリプトエンジンによって定義されるネイティブ関数およびオブジェクトのスクリプトの種類を指定します。|  
|PROFILER_SCRIPT_TYPE_DOM|Internet Explorer のドキュメントオブジェクトモデル (DOM) への呼び出しを指定します。たとえば、`document.getElementById` メソッドを呼び出します。|  
  
## <a name="see-also"></a>参照  
 [アクティブスクリプトプロファイラーの定数、列挙型、および構造体](../../winscript/reference/active-script-profiler-constants-enumerations-and-structures.md)   
 [IActiveScriptProfilerCallback:: ScriptCompiled](../../winscript/reference/iactivescriptprofilercallback-scriptcompiled.md)   
 [IActiveScriptProfilerCallback2::OnFunctionEnterByName](../../winscript/reference/iactivescriptprofilercallback2-onfunctionenterbyname.md)   
 [IActiveScriptProfilerCallback2::OnFunctionExitByName](../../winscript/reference/iactivescriptprofilercallback2-onfunctionexitbyname.md)