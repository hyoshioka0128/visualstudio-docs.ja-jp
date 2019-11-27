---
title: 'IDebugDocumentInfo:: GetName |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugDocumentInfo.GetName
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugDocumentInfo::GetName
ms.assetid: c25d73da-99b6-4c9f-82af-182b4853f81c
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: bc098da29367a322bd93b4f60ba0e090aee9ee91
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72570961"
---
# <a name="idebugdocumentinfogetname"></a>IDebugDocumentInfo::GetName
指定されたドキュメント名を返します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT GetName(  
   DOCUMENTNAMETYPE  dnt,  
   BSTR*             pbstrName  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `dnt`  
 から返されるドキュメント名の種類。  
  
 `pbstrName`  
 入出力名前を含む文字列。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは `HRESULT` を返します。 有効な値を次の表に示しますが、これ以外にもあります。  
  
|値|説明|  
|-----------|-----------------|  
|`S_OK`|メソッドが成功しました。|  
|`E_FAIL`|指定されたドキュメント名は不明です。|  
  
## <a name="remarks"></a>コメント  
 このメソッドは、指定されたドキュメント名を返します。  
  
## <a name="see-also"></a>参照  
 [IDebugDocumentInfo インターフェイス](../../winscript/reference/idebugdocumentinfo-interface.md)   
 [DOCUMENTNAMETYPE 列挙型](../../winscript/reference/documentnametype-enumeration.md)