---
title: 'IDebugApplication:: HandleBreakPoint ポイント |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugApplication.HandleBreakPoint
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugApplication::HandleBreakPoint
ms.assetid: 97219bdf-a39a-4e69-81ac-4ca2afe77ce5
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 30937817424e88f80cfa6afa8c874adfd2b2687b
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72574958"
---
# <a name="idebugapplicationhandlebreakpoint"></a>IDebugApplication::HandleBreakPoint
現在のスレッドをブロックし、ブレークポイントの通知をデバッガー IDE に送信します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT HandleBreakPoint(  
   BREAKREASON         br,  
   BREAKRESUMEACTION*  pbra  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `br`  
 から中断の理由。  
  
 `pbra`  
 入出力デバッガーがアプリケーションを再開したときに実行するアクション。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは `HRESULT` を返します。 有効な値を次の表に示しますが、これ以外にもあります。  
  
|値|説明|  
|-----------|-----------------|  
|`S_OK`|メソッドが成功しました。|  
  
## <a name="remarks"></a>コメント  
 言語エンジンは、ブレークポイントにヒットしたスレッドのコンテキストでこのメソッドを呼び出します。 このメソッドは、現在のスレッドをブロックし、デバッガー IDE にブレークポイント通知を送信します。 デバッガーがアプリケーションを再開したときに、`pbra` パラメーターで、実行するアクションを指定します。  
  
> [!NOTE]
> スタックフレームの列挙やブレークポイント時の式の評価などのタスクを実行するために、スレッドから言語エンジンを呼び出すことができます。  
  
 このメソッドによって `IApplicationDebugger::onHandleBreakPoint` が呼び出されます。  
  
## <a name="see-also"></a>参照  
 [IDebugApplication インターフェイス](../../winscript/reference/idebugapplication-interface.md)   
 [Iapplicationdebugger:: onHandleBreakPoint ポイント](../../winscript/reference/iapplicationdebugger-onhandlebreakpoint.md)   
 [Breakreason 列挙型](../../winscript/reference/breakreason-enumeration.md)   
 [BREAKRESUMEACTION 列挙型](../../winscript/reference/breakresumeaction-enumeration.md)