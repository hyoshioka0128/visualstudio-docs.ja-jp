---
title: 'IDebugApplicationNodeEvents:: onRemoveChild |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugApplicationNodeEvents.onRemoveChild
apilocation:
- scrobj.dll
helpviewer_keywords:
- IDebugApplicationNodeEvents::onRemoveChild
ms.assetid: 2e025d29-b8c0-4793-a2d3-c20d548d6386
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: f0ff7b28f14c26029d64197ba919cc97c90a856c
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72574664"
---
# <a name="idebugapplicationnodeeventsonremovechild"></a>IDebugApplicationNodeEvents::onRemoveChild
デバッグアプリケーションノードオブジェクトから子ノードが削除されると、イベントを処理します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT onRemoveChild(  
   IDebugApplicationNode*  prddpChild  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `prddpChild`  
 から削除された子アプリケーションノード。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは `HRESULT` を返します。 有効な値を次の表に示しますが、これ以外にもあります。  
  
|値|説明|  
|-----------|-----------------|  
|`S_OK`|メソッドが成功しました。|  
  
## <a name="remarks"></a>コメント  
 このメソッドは、子ノードがデバッグアプリケーションノードオブジェクトから削除されると、イベントを処理します。  
  
 `IDebugApplicationNode` インターフェイスの実装者は、このイベントを発生させます。  
  
## <a name="see-also"></a>参照  
 [IDebugApplicationNodeEvents インターフェイス](../../winscript/reference/idebugapplicationnodeevents-interface.md)   
 [IDebugApplicationNodeEvents:: onAddChild](../../winscript/reference/idebugapplicationnodeevents-onaddchild.md)   
 [IDebugApplicationNode インターフェイス](../../winscript/reference/idebugapplicationnode-interface.md)