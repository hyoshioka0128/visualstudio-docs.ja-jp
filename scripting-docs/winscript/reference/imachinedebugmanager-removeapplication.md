---
title: 'IMachineDebugManager:: RemoveApplication |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IMachineDebugManager.RemoveApplication
apilocation:
- scrobj.dll
helpviewer_keywords:
- IMachineDebugManager::RemoveApplication
ms.assetid: 873509ce-e638-484a-b2a2-489a8ce7dbfe
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 87951e55a7cfcfef1a366f79c380948c7651ed12
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72573937"
---
# <a name="imachinedebugmanagerremoveapplication"></a>IMachineDebugManager::RemoveApplication
実行中のアプリケーションの一覧からアプリケーションを削除します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT RemoveApplication(  
   DWORD  dwAppCookie  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `dwAppCookie`  
 からアプリケーションがアプリケーションの一覧に追加されたときに指定されたクッキー。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは `HRESULT` を返します。 有効な値を次の表に示しますが、これ以外にもあります。  
  
|値|説明|  
|-----------|-----------------|  
|`S_OK`|メソッドが成功しました。|  
  
## <a name="remarks"></a>コメント  
 このメソッドは、`IProcessDebugManager::RemoveApplication` が呼び出されるたびにプロセスデバッグマネージャーによって呼び出されます。  
  
## <a name="see-also"></a>参照  
 [Imachinedebugmanager:: AddApplication](../../winscript/reference/imachinedebugmanager-addapplication.md)   
 [Imachinedebugmanager インターフェイス](../../winscript/reference/imachinedebugmanager-interface.md)   
 [IProcessDebugManager::RemoveApplication](../../winscript/reference/iprocessdebugmanager-removeapplication.md)