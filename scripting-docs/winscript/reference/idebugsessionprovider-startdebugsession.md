---
title: 'IDebugSessionProvider:: StartDebugSession |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugSessionProvider.StartDebugSession
apilocation:
- scrobj.dll
helpviewer_keywords:
- IDebugSessionProvider::StartDebugSession
ms.assetid: 47697dfb-d4e1-492c-a14f-753e28195a76
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 0fc4bdade94401d5fc7b5756eb61fddd166fe49b
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72574909"
---
# <a name="idebugsessionproviderstartdebugsession"></a>IDebugSessionProvider::StartDebugSession
指定されたアプリケーションとのデバッグセッションを開始します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT StartDebugSession(  
   IRemoteDebugApplication*  pda  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pda`  
 からデバッグアプリケーションを指定します。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは `HRESULT` を返します。 有効な値を次の表に示しますが、これ以外にもあります。  
  
|値|説明|  
|-----------|-----------------|  
|`S_OK`|メソッドが成功しました。|  
  
## <a name="remarks"></a>コメント  
 このメソッドは、指定されたアプリケーションとのデバッグセッションを開始します。 デバッガーは、この呼び出しから戻る前に `IRemoteDebugApplication::ConnectDebugger` を呼び出す必要があります。  
  
## <a name="see-also"></a>参照  
 [IDebugSessionProvider インターフェイス](../../winscript/reference/idebugsessionprovider-interface.md)   
 [IRemoteDebugApplication::ConnectDebugger](../../winscript/reference/iremotedebugapplication-connectdebugger.md)