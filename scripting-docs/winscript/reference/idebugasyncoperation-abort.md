---
title: 'IDebugAsyncOperation:: Abort |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugAsyncOperation.Abort
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugAsyncOperation::Abort
ms.assetid: 232541c6-81b8-4eb7-96a7-a8e5fe087b31
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: b9ca6c5e1498229c84dc28a13cda2cce77b58a4f
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72573302"
---
# <a name="idebugasyncoperationabort"></a>IDebugAsyncOperation::Abort
操作をキャンセルします。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT Abort();  
```  
  
#### <a name="parameters"></a>パラメーター  
 このメソッドはパラメーターを受け取りません。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは `HRESULT` を返します。 有効な値を次の表に示しますが、これ以外にもあります。  
  
|値|説明|  
|-----------|-----------------|  
|S_OK|メソッドが成功しました。|  
|E_NOTIMPL|操作を取り消すことはできません。|  
  
## <a name="remarks"></a>コメント  
 このメソッドは、通常、応答しない操作をキャンセルするために、デバッガースレッド内から呼び出されます。 このメソッドにより、`IDebugSyncOperation` オブジェクトの `InProgressAbort` メソッドが呼び出されます。  
  
## <a name="see-also"></a>参照  
 [IDebugAsyncOperation インターフェイス](../../winscript/reference/idebugasyncoperation-interface.md)   
 [IDebugAsyncOperation:: Start](../../winscript/reference/idebugasyncoperation-start.md)   
 [IDebugSyncOperation::InProgressAbort](../../winscript/reference/idebugsyncoperation-inprogressabort.md)