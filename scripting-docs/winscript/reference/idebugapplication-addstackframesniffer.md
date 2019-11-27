---
title: 'IDebugApplication:: AddStackFrameSniffer |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugApplication.AddStackFrameSniffer
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugApplication::AddStackFrameSniffer
ms.assetid: a7a9684a-14c5-415a-ae63-a17397d58d07
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: a461c24b6f62f1e0ece88915e097faf0c59f15e7
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72575031"
---
# <a name="idebugapplicationaddstackframesniffer"></a>IDebugApplication::AddStackFrameSniffer
このアプリケーションにスタックフレーム列挙子プロバイダーを追加します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT AddStackFrameSniffer(  
   IDebugStackFrameSniffer*  pdsfs,  
   DWORD*                    pdwCookie  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pdsfs`  
 からこのアプリケーションに追加するスタックフレーム列挙子プロバイダー。  
  
 `pdwCookie`  
 入出力このスタックフレーム列挙子プロバイダーをアプリケーションから削除するために使用されるクッキー。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは `HRESULT` を返します。 有効な値を次の表に示しますが、これ以外にもあります。  
  
|値|説明|  
|-----------|-----------------|  
|`S_OK`|メソッドが成功しました。|  
  
## <a name="remarks"></a>コメント  
 通常、言語エンジンはこのメソッドを呼び出して、スタックフレームをデバッガーに公開しますが、他のエンティティがスタックフレームを公開する可能性があります。  
  
## <a name="see-also"></a>参照  
 [IDebugApplication インターフェイス](../../winscript/reference/idebugapplication-interface.md)   
 [IDebugApplication::RemoveStackFrameSniffer](../../winscript/reference/idebugapplication-removestackframesniffer.md)   
 [IDebugStackFrameSniffer インターフェイス](../../winscript/reference/idebugstackframesniffer-interface.md)