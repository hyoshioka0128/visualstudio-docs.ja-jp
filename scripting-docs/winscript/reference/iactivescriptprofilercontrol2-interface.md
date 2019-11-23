---
title: IActiveScriptProfilerControl2 Interface |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IActiveScriptProfilerControl2 interface
ms.assetid: 89455276-5c23-420b-a7e0-804a32635291
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 7059868ae65c5093b24f342bd303ec70172171c0
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72571534"
---
# <a name="iactivescriptprofilercontrol2-interface"></a>IActiveScriptProfilerControl2 インターフェイス
スクリプトの実行時にプロファイリングを開始または停止する機能を追加するメソッドを提供します。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[IActiveScriptProfilerControl2::CompleteProfilerStart](../../winscript/reference/iactivescriptprofilercontrol2-completeprofilerstart.md)|適用可能なすべてのスクリプトエンジンでプロファイリングを開始したことをプロファイラーに通知します。 これにより、プロファイリングの開始時に [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] が実行されている場合に、完全な呼び出し履歴を取得できます。|  
|[IActiveScriptProfilerControl2::PrepareProfilerStop](../../winscript/reference/iactivescriptprofilercontrol2-prepareprofilerstop.md)|適用可能なすべてのスクリプトエンジンでプロファイリングを停止することをプロファイラーに通知します。 これにより、プロファイリングを停止したときに [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] が実行されている場合に、完全な呼び出し履歴を取得できます。|  
  
## <a name="see-also"></a>参照  
 [IActiveScriptProfilerControl インターフェイス](../../winscript/reference/iactivescriptprofilercontrol-interface.md)   
 [アクティブ スクリプト プロファイラーのインターフェイス](../../winscript/reference/active-script-profiler-interfaces.md)