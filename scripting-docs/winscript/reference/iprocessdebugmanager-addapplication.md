---
title: 'IProcessDebugManager:: AddApplication |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IProcessDebugManager.AddApplication
apilocation:
- pdm.dll
helpviewer_keywords:
- IProcessDebugManager::AddApplication
ms.assetid: 73828299-11eb-4c58-ad70-f80f2d0eede8
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 47ad8132b9b51efa5f5c2f260e48441e5da64c42
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72576813"
---
# <a name="iprocessdebugmanageraddapplication"></a>IProcessDebugManager::AddApplication
コンピューターデバッグマネージャーの実行中のアプリケーションの一覧にアプリケーションを追加します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT AddApplication(  
   IDebugApplication*  pda,  
   DWORD*              pdwAppCookie  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pda`  
 から実行中のアプリケーションの一覧に追加するデバッグアプリケーション。  
  
 `pdwAppCookie`  
 入出力コンピューターデバッグマネージャーからアプリケーションを削除するために使用されるクッキー。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは `HRESULT` を返します。 有効な値を次の表に示しますが、これ以外にもあります。  
  
|値|説明|  
|-----------|-----------------|  
|`S_OK`|メソッドが成功しました。|  
  
## <a name="remarks"></a>コメント  
 このメソッドは、コンピューターデバッグマネージャーで、実行中のアプリケーションの一覧にアプリケーションを追加します。  
  
## <a name="see-also"></a>参照  
 [Iprocessdebugmanager インターフェイス](../../winscript/reference/iprocessdebugmanager-interface.md)   
 [IProcessDebugManager::RemoveApplication](../../winscript/reference/iprocessdebugmanager-removeapplication.md)