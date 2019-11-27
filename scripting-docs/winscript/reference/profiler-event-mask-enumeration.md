---
title: PROFILER_EVENT_MASK 列挙型 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- PROFILER_EVENT_MASK
apilocation:
- scrobj.dll
ms.assetid: c2168408-f4f6-4600-971d-f15b4edf4ca2
caps.latest.revision: 17
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: c1e1e7f3b604832014cb23245b105756d1126c5b
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72572284"
---
# <a name="profiler_event_mask-enumeration"></a>PROFILER_EVENT_MASK 列挙型
プロファイルが必要なイベントの種類を示します。  
  
## <a name="syntax"></a>構文  
  
```cpp
typedef enum {  
    PROFILER_EVENT_MASK_TRACE_SCRIPT_FUNCTION_CALL = 0x00000001,  
    PROFILER_EVENT_MASK_TRACE_NATIVE_FUNCTION_CALL = 0x00000002,  
    PROFILER_EVENT_MASK_TRACE_DOM_FUNCTION_CALL    = 0x00000004,  
    PROFILER_EVENT_MASK_TRACE_ALL =  
    PROFILER_EVENT_MASK_TRACE_SCRIPT_FUNCTION_CALL |  
    PROFILER_EVENT_MASK_TRACE_NATIVE_FUNCTION_CALL,  
    PROFILER_EVENT_MASK_TRACE_ALL_WITH_DOM = PROFILER_EVENT_MASK_TRACE_ALL |  
    PROFILER_EVENT_MASK_TRACE_DOM_FUNCTION_CALL  
} PROFILER_EVENT_MASK;  
```  
  
## <a name="members"></a>メンバー  
  
|メンバー|説明|  
|------------|-----------------|  
|PROFILER_EVENT_MASK_TRACE_SCRIPT_FUNCTION_CALL|ユーザーが記述したスクリプトおよび動的コードで定義されている関数をプロファイルします。|  
|PROFILER_EVENT_MASK_TRACE_NATIVE_FUNCTION_CALL|スクリプトエンジンによって定義されるネイティブ関数をプロファイルします。|  
|PROFILER_EVENT_MASK_TRACE_ALL|ドキュメントオブジェクトモデル (DOM) への呼び出しを除く、すべてのユーザー定義およびスクリプトエンジン関数をプロファイルします。|  
|PROFILER_EVENT_MASK_TRACE_DOM_FUNCTION_CALL|DOM を呼び出すプロファイル関数。|  
|PROFILER_EVENT_MASK_TRACE_ALL_WITH_DOM|DOM への呼び出しを含むすべての関数をプロファイリングします。|  
  
## <a name="see-also"></a>参照  
 [アクティブスクリプトプロファイラーの定数、列挙型、および構造体](../../winscript/reference/active-script-profiler-constants-enumerations-and-structures.md)   
 [IActiveScriptProfilerControl:: SetProfilerEventMask](../../winscript/reference/iactivescriptprofilercontrol-setprofilereventmask.md)   
 [IActiveScriptProfilerControl::StartProfiling](../../winscript/reference/iactivescriptprofilercontrol-startprofiling.md)