---
title: 'IActiveScriptProfilerControl2:: CompleteProfilerStart |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IActiveScriptProfilerControl2::CompleteProfilerStart
ms.assetid: e14d94a2-39d3-40a1-84d9-6300fbe2b339
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: f0230ecb480792b5b24b7375f5b95926735d0a61
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72571560"
---
# <a name="iactivescriptprofilercontrol2completeprofilerstart"></a>IActiveScriptProfilerControl2::CompleteProfilerStart
適用可能なすべてのスクリプトエンジンでプロファイリングを開始したことをプロファイラーに通知します。 このメソッドを使用すると、プロファイリングの開始時に [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] が実行されている場合に、完全な呼び出し履歴を取得できます。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT CompleteProfilerStart();  
```  
  
#### <a name="parameters"></a>パラメーター  
 メソッドは、パラメーターを受け取りません。  
  
## <a name="return-value"></a>戻り値  
 HRESULT を返します。 次の値を指定できます。  
  
|戻り値|意味|  
|------------------|-------------|  
|`S_OK`|メソッドが成功しました。|  
|`E_FAIL`|プロファイルを開始できません。|  
|`S_FALSE`|スクリプトが実行されていないときにプロファイルが開始されました。|  
|`ACTIVPROF_E_PROFILER_ABSENT`|プロファイルが有効になっていません。 コールバックが設定されていません。|  
|`E_OUTOFMEMORY`|メモリ不足の状態により、呼び出し履歴を取得できません。|  
  
## <a name="remarks"></a>コメント  
 `IActiveScriptProfilerControl2::CompleteProfilerStart` を呼び出すと、コールスタックに既に存在する関数のイベントが確実に送信されます。 このメソッドは、現在のタブにある任意のスクリプトエンジンでプロファイリングを開始した後に呼び出す必要があります。メソッドは、任意のスクリプトエンジンに対して呼び出すことができます。  
  
## <a name="see-also"></a>参照  
 [IActiveScriptProfilerControl2::PrepareProfilerStop](../../winscript/reference/iactivescriptprofilercontrol2-prepareprofilerstop.md)   
 [IActiveScriptProfilerControl2 インターフェイス](../../winscript/reference/iactivescriptprofilercontrol2-interface.md)