---
title: 'IActiveScriptProfilerCallback2:: OnFunctionEnterByName |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IActiveScriptProfilerCallback2::OnFunctionEnterByName
ms.assetid: 24b1593a-97fc-4d70-9b85-ec86fb59f987
caps.latest.revision: 6
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: c0407441c77250b2cc27e9fee09c5039bb8e44ab
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72571642"
---
# <a name="iactivescriptprofilercallback2onfunctionenterbyname"></a>IActiveScriptProfilerCallback2::OnFunctionEnterByName
スクリプトエンジンがドキュメントオブジェクトモデル (DOM) 関数呼び出しを実行しようとしていることをプロファイラーオブジェクトに通知します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT OnFunctionEnterByName(  
    [in] [string] const WCHAR *pwszFunctionName,  
    [in] PROFILER_SCRIPT_TYPE scriptType);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pwszFunctionName`  
 からスクリプトエンジンが実行する関数の名前。  
  
 `scriptType`  
 から関数の型。 有効な値の説明については、「 [PROFILER_SCRIPT_TYPE 列挙型](../../winscript/reference/profiler-script-type-enumeration.md)」を参照してください。  
  
## <a name="return-value"></a>戻り値  
 このメソッドの戻り値は、スクリプトエンジンによって無視されます。  
  
## <a name="remarks"></a>コメント  
 DOM 呼び出しの場合、スクリプトエンジンは[IActiveScriptProfilerCallback:: OnFunctionEnter](../../winscript/reference/iactivescriptprofilercallback-onfunctionenter.md)を呼び出す代わりに、このメソッドを呼び出します。 これは、DOM 内の一意のメソッドとプロパティの数が多いためです。  
  
## <a name="see-also"></a>参照  
 [IActiveScriptProfilerCallback2:: OnFunctionExitByName](../../winscript/reference/iactivescriptprofilercallback2-onfunctionexitbyname.md)   
 [IActiveScriptProfilerCallback2 インターフェイス](../../winscript/reference/iactivescriptprofilercallback2-interface.md)