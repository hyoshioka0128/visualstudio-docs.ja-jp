---
title: SCRIPTTHREADID 定数 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- SCRIPTTHREADID
apilocation:
- scrobj.dll
helpviewer_keywords:
- SCRIPTTHREADID
ms.assetid: 1df9940c-ad0c-42d8-96b9-6a6abe2382e6
caps.latest.revision: 9
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: bf1b23b191bda29b00bf29f482332301897f9f37
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72575663"
---
# <a name="scriptthreadid-constants"></a>SCRIPTTHREADID 定数
スレッドの種類を指定するために使用します。  
  
## <a name="syntax"></a>構文  
  
```cpp
typedef DWORD SCRIPTTHREADID;  
```  
  
## <a name="constants"></a>定数  
  
|定数|値|意味|  
|--------------|-----------|-------------|  
|SCRIPTTHREADID_CURRENT|0xFFFFFFFD|現在実行中のスレッド。|  
|SCRIPTTHREADID_BASE|0xFFFFFFFE|基本スレッド。つまり、スクリプトエンジンがインスタンス化されたスレッド。|  
|SCRIPTTHREADID_ALL|~|すべてのスレッド。|  
  
## <a name="remarks"></a>コメント  
 `SCRIPTTHREADID` 型は `IActiveScript::GetCurrentScriptThreadID`、`IActiveScript::GetScriptThreadID`、`IActiveScript::GetScriptThreadState`、および `IActiveScript::InterruptScriptThread`によって使用されますが、定数は `IActiveScript::GetScriptThreadState` と `IActiveScript::InterruptScriptThread`でのみ使用できます。  
  
## <a name="see-also"></a>参照  
 [IActiveScript:: GetCurrentScriptThreadID](../../winscript/reference/iactivescript-getcurrentscriptthreadid.md)   
 [IActiveScript:: GetScriptThreadID](../../winscript/reference/iactivescript-getscriptthreadid.md)   
 [IActiveScript:: GetScriptThreadState](../../winscript/reference/iactivescript-getscriptthreadstate.md)   
 [IActiveScript::InterruptScriptThread](../../winscript/reference/iactivescript-interruptscriptthread.md)