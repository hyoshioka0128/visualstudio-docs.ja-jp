---
title: 'IDebugDocumentText:: GetDocumentAttributes |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugDocumentText.GetDocumentAttributes
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugDocumentText::GetDocumentAttributes
ms.assetid: 8c544ca1-8db4-4bca-973e-09315d9a0ee5
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: f3a97c42037e5f7439692e3c3185b4194e63dc2a
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72572157"
---
# <a name="idebugdocumenttextgetdocumentattributes"></a>IDebugDocumentText::GetDocumentAttributes
ドキュメントの属性を返します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT GetDocumentAttributes(  
   TEXT_DOC_ATTR*  ptextdocattr  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `ptextdocattr`  
 入出力ドキュメントのテキスト属性。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは `HRESULT` を返します。 有効な値を次の表に示しますが、これ以外にもあります。  
  
|値|説明|  
|-----------|-----------------|  
|`S_OK`|メソッドが成功しました。|  
  
## <a name="remarks"></a>コメント  
 このメソッドは、ドキュメントの属性を返します。  
  
## <a name="see-also"></a>参照  
 [IDebugDocumentText インターフェイス](../../winscript/reference/idebugdocumenttext-interface.md)   
 [TEXT_DOC_ATTR 定数](../../winscript/reference/text-doc-attr-constants.md)