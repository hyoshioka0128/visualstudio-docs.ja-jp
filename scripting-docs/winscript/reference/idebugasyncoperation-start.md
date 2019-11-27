---
title: 'IDebugAsyncOperation:: Start |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugAsyncOperation.Start
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugAsyncOperation::Start
ms.assetid: a7272364-28e0-48ae-8405-b8bce8a6b9fd
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 485eb34ebe200e7f7898d9338effed37cbf2aa10
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72573250"
---
# <a name="idebugasyncoperationstart"></a>IDebugAsyncOperation::Start
非同期操作を開始します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT Start(  
   IDebugAsyncOperationCallBack*  padocb  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `padocb`  
 この操作からステータスイベントを受け取るコールバックインターフェイス。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは `HRESULT` を返します。 有効な値を次の表に示しますが、これ以外にもあります。  
  
|値|説明|  
|-----------|-----------------|  
|`S_OK`|メソッドが成功しました。|  
|`E_UNEXPECTED`|操作は既に保留中です。|  
  
## <a name="remarks"></a>コメント  
 このメソッドは、`IDebugSyncOperation::GetTargetThread`から取得したスレッドで `IDebugSyncOperation::Execute` を非同期的に呼び出します。 このメソッドは、デバッガースレッド内からのみ呼び出す必要があります。それ以外の場合は、操作が完了するまで戻りません。  
  
## <a name="see-also"></a>参照  
 [IDebugAsyncOperation::Abort](../../winscript/reference/idebugasyncoperation-abort.md)   
 [IDebugAsyncOperation インターフェイス](../../winscript/reference/idebugasyncoperation-interface.md)   
 [IDebugSyncOperation::Execute](../../winscript/reference/idebugsyncoperation-execute.md)   
 [IDebugSyncOperation::GetTargetThread](../../winscript/reference/idebugsyncoperation-gettargetthread.md)