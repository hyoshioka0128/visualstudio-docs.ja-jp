---
title: 'IMachineDebugManagerEvents:: onRemoveApplication |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IMachineDebugManagerEvents.onRemoveApplication
apilocation:
- scrobj.dll
helpviewer_keywords:
- IMachineDebugManagerEvents::onRemoveApplication
ms.assetid: 3ba71bd8-fd69-4a41-99c6-c736c416f227
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: b50d91a75a8f251ad04b456b179fdd0ba0d1dc32
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72571480"
---
# <a name="imachinedebugmanagereventsonremoveapplication"></a>IMachineDebugManagerEvents::onRemoveApplication
実行中のアプリケーションの一覧からアプリケーションが削除されたときに、イベントを処理します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT onRemoveApplication(  
   IRemoteDebugApplication*  pda,  
   DWORD                     dwAppCookie  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pda`  
 から実行中のアプリケーションの一覧から削除されたアプリケーション。  
  
 `dwAppCookie`  
 からアプリケーションの一覧からアプリケーションを追加したときに指定されたクッキー。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは `HRESULT` を返します。 有効な値を次の表に示しますが、これ以外にもあります。  
  
|値|説明|  
|-----------|-----------------|  
|`S_OK`|メソッドが成功しました。|  
  
## <a name="remarks"></a>コメント  
 このメソッドは、アプリケーションが実行中のアプリケーションの一覧から削除されたことを示します。  
  
## <a name="see-also"></a>参照  
 [Imachinedebugmanagerevents インターフェイス](../../winscript/reference/imachinedebugmanagerevents-interface.md)   
 [IMachineDebugManagerEvents::onAddApplication](../../winscript/reference/imachinedebugmanagerevents-onaddapplication.md)