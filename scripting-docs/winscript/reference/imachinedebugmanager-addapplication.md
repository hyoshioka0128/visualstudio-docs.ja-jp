---
title: 'IMachineDebugManager:: AddApplication |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IMachineDebugManager.AddApplication
apilocation:
- scrobj.dll
helpviewer_keywords:
- IMachineDebugManager::AddApplication
ms.assetid: 7cd591b6-718c-4e77-acb7-a6dd147ddf57
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 54ff617ac96c0eb3498b796d4f7fe49f95e1cc96
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72573965"
---
# <a name="imachinedebugmanageraddapplication"></a>IMachineDebugManager::AddApplication
実行中のアプリケーションの一覧にアプリケーションを追加します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT AddApplication(  
   IRemoteDebugApplication*  pda,  
   DWORD*                    pdwAppCookie  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pda`  
 からアプリケーションを実行中のアプリケーションの一覧に表示します。  
  
 `pdwAppCookie`  
 入出力コンピューターデバッグマネージャーからアプリケーションを削除するために使用されるクッキー。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは `HRESULT` を返します。 有効な値を次の表に示しますが、これ以外にもあります。  
  
|値|説明|  
|-----------|-----------------|  
|`S_OK`|メソッドが成功しました。|  
  
## <a name="remarks"></a>コメント  
 このメソッドは、`IProcessDebugManager::AddApplication` が呼び出されるたびにプロセスデバッグマネージャーによって呼び出されます。  
  
## <a name="see-also"></a>参照  
 [Imachinedebugmanager インターフェイス](../../winscript/reference/imachinedebugmanager-interface.md)   
 [Imachinedebugmanager:: RemoveApplication](../../winscript/reference/imachinedebugmanager-removeapplication.md)   
 [IProcessDebugManager::AddApplication](../../winscript/reference/iprocessdebugmanager-addapplication.md)