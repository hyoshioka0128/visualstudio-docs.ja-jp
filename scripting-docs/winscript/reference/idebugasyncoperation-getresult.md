---
title: 'IDebugAsyncOperation:: GetResult |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugAsyncOperation.GetResult
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugAsyncOperation::GetResult
ms.assetid: 56d43365-6b12-4213-a97c-953c40d7b7f6
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 55c51649a5bc3094dd306166e013a892ce67e236
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72573283"
---
# <a name="idebugasyncoperationgetresult"></a>IDebugAsyncOperation::GetResult
同期デバッグ操作からの戻り値と戻り値オブジェクトパラメーターを提供します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT GetResult(  
   HRESULT*    phrResult,  
   IUnknown**  ppunkResult  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `phrResult`  
 入出力操作が完了すると、`phrResult` が `IDebugSyncOperation::Execute`の戻り値になります。  
  
 `ppunkResult`  
 入出力操作が完了した場合、`ppunkResult` は操作によって返されるオブジェクトパラメーターです。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは `HRESULT` を返します。 有効な値を次の表に示しますが、これ以外にもあります。  
  
|値|説明|  
|-----------|-----------------|  
|`S_OK`|メソッドが成功しました。|  
|`E_PENDING`|操作は完了していません。|  
  
## <a name="remarks"></a>コメント  
 操作が完了している場合、このメソッドは `IDebugSyncOperation::Execute`から `HRESULT` とオブジェクトのパラメーターを返します。  
  
## <a name="see-also"></a>参照  
 [IDebugAsyncOperation インターフェイス](../../winscript/reference/idebugasyncoperation-interface.md)   
 [IDebugSyncOperation::Execute](../../winscript/reference/idebugsyncoperation-execute.md)