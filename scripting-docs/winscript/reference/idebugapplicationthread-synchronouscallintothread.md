---
title: 'IDebugApplicationThread:: SynchronousCallIntoThread |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugApplicationThread.SynchronousCallIntoThread
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugApplicationThread::SynchronousCallIntoThread
ms.assetid: 8a91157f-dade-418a-ad02-5607ce12c95c
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: d545782f8103d10b38f3eb0d2f149c4ef3b9dc95
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72574498"
---
# <a name="idebugapplicationthreadsynchronouscallintothread"></a>IDebugApplicationThread::SynchronousCallIntoThread
アプリケーションスレッドでコードを実行するための機構を呼び出し元に提供します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT SynchronousCallIntoThread(  
   IDebugThreadCall*  pstcb,  
   DWORD_PTR          dwParam1,  
   DWORD_PTR          dwParam2,  
   DWORD_PTR          dwParam3  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pstcb`  
 から呼び出すオブジェクト。  
  
 `dwParam1`  
 から`IDebugThreadCall::ThreadCallHandler` メソッドに渡す最初のパラメーター。  
  
 `dwParam2`  
 から`IDebugThreadCall::ThreadCallHandler` メソッドに渡す2番目のパラメーター。  
  
 `dwParam3`  
 から`IDebugThreadCall::ThreadCallHandler` メソッドに渡す3番目のパラメーター。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは `HRESULT` を返します。 有効な値を次の表に示しますが、これ以外にもあります。  
  
|値|説明|  
|-----------|-----------------|  
|`S_OK`|メソッドが成功しました。|  
  
## <a name="remarks"></a>コメント  
 このメソッドは、呼び出し元がデバッガースレッドでコードを実行するための機構を提供します。 言語エンジンとホストは、通常、このメソッドを使用して、シングルスレッド実装の上にフリースレッドオブジェクトを実装します。  
  
## <a name="see-also"></a>参照  
 [IDebugApplicationThread インターフェイス](../../winscript/reference/idebugapplicationthread-interface.md)   
 [IDebugThreadCall インターフェイス](../../winscript/reference/idebugthreadcall-interface.md)