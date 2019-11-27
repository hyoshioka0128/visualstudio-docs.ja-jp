---
title: 'IDebugApplication:: 焼討デバッガイベント |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugApplication.FireDebuggerEvent
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugApplication::FireDebuggerEvent
ms.assetid: fd1f602e-fc15-4158-a6e7-497ff5b4a509
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 00d895ed484e37f0ba38636a409876156ed97287
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72575008"
---
# <a name="idebugapplicationfiredebuggerevent"></a>IDebugApplication::FireDebuggerEvent
デバッガーの `IApplicationDebugger` インターフェイスに汎用イベントを発生させます。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT FireDebuggerEvent(  
   REFGUID    riid,  
   IUnknown*  punk  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `riid`  
 からオブジェクトの GUID。  
  
 `punk`  
 からデバッガーに渡すイベントオブジェクト。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは `HRESULT` を返します。 有効な値を次の表に示しますが、これ以外にもあります。  
  
|値|説明|  
|-----------|-----------------|  
|`S_OK`|メソッドが成功しました。|  
|`E_NOTIMPL`|メソッドは現在実装されていません。|  
  
## <a name="remarks"></a>コメント  
 GUID と `IUnknown` のセマンティクスは、アプリケーション/デバッガーが完全に定義されています。  
  
 このメソッドは、デバッガーモデルのカスタム拡張を可能にします。現在は実装されていません。  
  
 このメソッドによって `IApplicationDebugger::onDebuggerEvent` が呼び出されます。  
  
## <a name="see-also"></a>参照  
 [IDebugApplication インターフェイス](../../winscript/reference/idebugapplication-interface.md)   
 [IApplicationDebugger::onDebuggerEvent](../../winscript/reference/iapplicationdebugger-ondebuggerevent.md)