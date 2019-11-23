---
title: 'ISimpleConnectionPoint:: Advise |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ISimpleConnectionPoint.Advise
apilocation:
- pdm.dll
helpviewer_keywords:
- ISimpleConnectionPoint::Advise
ms.assetid: 59ded60d-b938-4110-aca3-e69ba234ca9a
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: d7d08d4774dffbfd840c674b15abe82bedb37e5f
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72571827"
---
# <a name="isimpleconnectionpointadvise"></a>ISimpleConnectionPoint::Advise
単純な接続ポイントオブジェクトとクライアントのシンクとの間の接続を確立します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT Advise(  
   IDispatch*  pdisp,  
   DWORD*      pdwCookie  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pdisp`  
 からクライアントのアドバイズシンクの `IDispatch` インターフェイスへのポインター。 クライアントのシンクは、単純な接続ポイントからの発信呼び出しを受信します。  
  
 `pdwCookie`  
 入出力この接続を一意に識別する、返されたトークンへのポインター。 呼び出し元は、後でこのトークンを使用して、`ISimpleConnectionPoint::Unadvise` メソッドに渡すことによって接続を削除します。 接続が正常に確立されなかった場合、この値は0になります。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは `HRESULT` を返します。 有効な値を次の表に示しますが、これ以外にもあります。  
  
|値|説明|  
|-----------|-----------------|  
|`S_OK`|メソッドが成功しました。|  
  
## <a name="remarks"></a>コメント  
 このメソッドは、単純な接続ポイントオブジェクトとクライアントのシンクとの間の接続を確立します。  
  
## <a name="see-also"></a>参照  
 [ISimpleConnectionPoint インターフェイス](../../winscript/reference/isimpleconnectionpoint-interface.md)   
 [ISimpleConnectionPoint::Unadvise](../../winscript/reference/isimpleconnectionpoint-unadvise.md)