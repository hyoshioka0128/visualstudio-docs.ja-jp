---
title: 'IDebugDocumentHelper:: AddUnicodeText |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugDocumentHelper.AddUnicodeText
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugDocumentHelper::AddUnicodeText
ms.assetid: f4ef648e-c55d-4ef0-8df3-e808b798d3b8
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 5820c380c92f2c3cd95763b440d5f9755db3e717
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72577055"
---
# <a name="idebugdocumenthelperaddunicodetext"></a>IDebugDocumentHelper::AddUnicodeText
このドキュメントの末尾に Unicode 文字列を追加します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT AddUnicodeText(  
   LPCOLESTR  pszText  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pszText`  
 からテキストを含む null で終わる文字列へのポインター。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは `HRESULT` を返します。 有効な値を次の表に示しますが、これ以外にもあります。  
  
|値|説明|  
|-----------|-----------------|  
|`S_OK`|メソッドが成功しました。|  
|`E_FAIL`|メソッドが文字を追加できませんでした。|  
  
## <a name="remarks"></a>コメント  
 このメソッドは `IDebugDocumentTextEvents` 通知を生成します。  
  
> [!NOTE]
> `AddDeferredText` が呼び出された後にこのメソッドが呼び出されると、`E_FAIL` が返されます。  
  
## <a name="see-also"></a>参照  
 [IDebugDocumentHelper インターフェイス](../../winscript/reference/idebugdocumenthelper-interface.md)   
 [IDebugDocumentHelper:: AddDeferredText](../../winscript/reference/idebugdocumenthelper-adddeferredtext.md)   
 [IDebugDocumentTextEvents インターフェイス](../../winscript/reference/idebugdocumenttextevents-interface.md)