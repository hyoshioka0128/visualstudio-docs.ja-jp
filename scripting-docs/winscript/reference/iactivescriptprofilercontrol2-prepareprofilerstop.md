---
title: IActiveScriptProfilerControl2::P repareProfilerStop |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IActiveScriptProfilerControl2::PrepareProfilerStop
ms.assetid: e43a63bc-c44f-44a8-9db4-29062b9e6a16
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 24d4d73e0263882ad028ea66d3fac5e24f3af9ba
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72571443"
---
# <a name="iactivescriptprofilercontrol2prepareprofilerstop"></a>IActiveScriptProfilerControl2::PrepareProfilerStop
適用可能なすべてのスクリプトエンジンでプロファイリングを停止することをプロファイラーに通知します。 このメソッドを使用すると、プロファイリングの停止時に [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] が実行されている場合に、完全な呼び出し履歴を取得できます。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT PrepareProfilerStop();  
```  
  
#### <a name="parameters"></a>パラメーター  
 メソッドは、パラメーターを受け取りません。  
  
## <a name="return-value"></a>戻り値  
 HRESULT を返します。 次の値を指定できます。  
  
|戻り値|意味|  
|------------------|-------------|  
|`S_OK`|メソッドが成功しました。|  
|`E_FAIL`|プロファイルを開始できませんでした。|  
|`S_FALSE`|スクリプトが実行されていないときに、プロファイリングが停止されました。|  
|`ACTIVPROF_E_PROFILER_ABSENT`|プロファイルが有効になっていません。|  
  
## <a name="remarks"></a>コメント  
 `IActiveScriptProfilerControl2::PrepareProfilerStop` を呼び出すと、コールスタック内の関数のイベントが確実に送信されます。 現在のタブにあるスクリプトエンジンでプロファイリングを停止する前に、このメソッドを呼び出す必要があります。メソッドは、任意のスクリプトエンジンに対して呼び出すことができます。  
  
## <a name="see-also"></a>参照  
 [IActiveScriptProfilerControl2::CompleteProfilerStart](../../winscript/reference/iactivescriptprofilercontrol2-completeprofilerstart.md)   
 [IActiveScriptProfilerControl2 インターフェイス](../../winscript/reference/iactivescriptprofilercontrol2-interface.md)