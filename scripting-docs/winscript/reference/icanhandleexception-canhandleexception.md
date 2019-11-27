---
title: 'ICanHandleException:: CanHandleException |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ICanHandleException.CanHandleException
apilocation:
- scrobj.dll
helpviewer_keywords:
- ICanHandleException::CanHandleException
ms.assetid: 0fc703bf-9518-487e-af20-00e073b640f1
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: c536d35dcb9f0faca8b033ecd39aec520a2e260a
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72575718"
---
# <a name="icanhandleexceptioncanhandleexception"></a>ICanHandleException::CanHandleException
スクリプトエンジンの呼び出し元が、指定された例外を処理できるかどうかを判断します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT CanHandleException(  
   EXCEPINFO*  pExcepInfo,  
   VARIANT*    pvar  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pExcepInfo`  
 から例外ハンドラーが見つからない場合に報告される情報を格納している `EXCEPINFO` 構造体へのポインター。  
  
 `pvar`  
 から`throw` ステートメントによってスローされる値など、例外に関連付けられた値。 このパラメーターは `NULL` の場合もあります。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは `HRESULT` を返します。 有効な値を次の表に示しますが、これ以外にもあります。  
  
|値|説明|  
|-----------|-----------------|  
|`S_OK`|呼び出し元は例外を処理できます。|  
|`E_FAIL`|呼び出し元が例外を処理できません。|  
  
## <a name="remarks"></a>コメント  
 `IDispatchEx::InvokeEx`または同様のメソッドへの呼び出しによって例外が発生した場合、スクリプトエンジンは、`ICanHandleException` インターフェイスをサポートするスクリプトの呼び出し元チェーン内の呼び出し元を確認し、例外を処理できることを示します。 呼び出し元が例外を処理できない場合、スクリプトエンジンは停止します。  
  
## <a name="see-also"></a>参照  
 [Icanhandleexception インターフェイス](../../winscript/reference/icanhandleexception-interface.md)   
 [IDispatchEx::InvokeEx](../../winscript/reference/idispatchex-invokeex.md)