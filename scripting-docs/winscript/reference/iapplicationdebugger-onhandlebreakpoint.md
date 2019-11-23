---
title: 'IApplicationDebugger:: onHandleBreakPoint ポイント |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IApplicationDebugger.onHandleBreakPoint
apilocation:
- scrobj.dll
helpviewer_keywords:
- IApplicationDebugger::onHandleBreakPoint
ms.assetid: 31adcecd-d6c1-4222-ab2c-32ec2fefb322
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 3796ea1f50f0c4bcf945dbc10592c048db22757b
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72577843"
---
# <a name="iapplicationdebuggeronhandlebreakpoint"></a>IApplicationDebugger::onHandleBreakPoint
ブレークポイントイベントを処理します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT onHandleBreakPoint(  
   IRemoteDebugApplicationThread*  prpt,  
   BREAKREASON                     br,  
   IActiveScriptErrorDebug*        pError  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `prpt`  
 からブレークポイントが発生したスレッド。  
  
 `br`  
 からブレークポイントの理由。  
  
 `pError`  
 から`br` の値が BREAKREASON_ERROR 場合に提供されるランタイムエラー情報。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは `HRESULT` を返します。 有効な値を次の表に示しますが、これ以外にもあります。  
  
|値|説明|  
|-----------|-----------------|  
|`S_OK`|メソッドが成功しました。|  
  
## <a name="remarks"></a>コメント  
 このメソッドは、ブレークポイントにヒットし `IDebugApplication::HandleBreakPoint` が呼び出されると呼び出されます。  
  
 デバッガー IDE が `IRemoteDebugApplication::ResumeFromBreakPoint`を呼び出すまで、アプリケーションは中断されたままになります。  
  
## <a name="see-also"></a>参照  
 [Iapplicationdebugger インターフェイス](../../winscript/reference/iapplicationdebugger-interface.md)   
 [IDebugApplication:: HandleBreakPoint ポイント](../../winscript/reference/idebugapplication-handlebreakpoint.md)   
 [Iremotedebugapplication:: ResumeFromBreakPoint](../../winscript/reference/iremotedebugapplication-resumefrombreakpoint.md)   
 [BREAKREASON 列挙型](../../winscript/reference/breakreason-enumeration.md)