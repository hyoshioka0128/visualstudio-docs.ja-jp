---
title: 'IActiveScriptDebug:: EnumCodeContextsOfPosition |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptDebug.EnumCodeContextsOfPosition
apilocation:
- jscript.dll
helpviewer_keywords:
- IActiveScriptDebug::EnumCodeContextsOfPosition
ms.assetid: 19f44420-bcc8-4c10-8c38-378d96044117
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: aedfe5d40d8f4086e30f3a62c070b8ccd5ef2388
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72572786"
---
# <a name="iactivescriptdebugenumcodecontextsofposition"></a>IActiveScriptDebug::EnumCodeContextsOfPosition
`IDebugDocumentContext::EnumCodeContexts` メソッドを委任するためにスマートホストによって使用されます。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT EnumCodeContextsOfPosition(  
   DWORD_PTR                 dwSourceContext,  
   ULONG                     uCharacterOffset,  
   ULONG                     uNumChars,  
   IEnumDebugCodeContexts**  ppescc  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `dwSourceContext`  
 から`IActiveScriptParse::ParseScriptText` または `IActiveScriptParse::AddScriptlet`に提供されるソースコンテキスト。  
  
 `uCharacterOffset`  
 からスクリプトテキストの先頭を基準とした文字オフセット。  
  
 `uNumChars`  
 からこのコンテキストの文字数。  
  
 `ppescc`  
 入出力指定された範囲のコードコンテキストの列挙子。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは `HRESULT` を返します。 有効な値を次の表に示しますが、これ以外にもあります。  
  
|値|説明|  
|-----------|-----------------|  
|`S_OK`|メソッドが成功しました。|  
  
## <a name="remarks"></a>コメント  
 スマートホストは、このメソッドを使用して `IDebugDocumentContext::EnumCodeContexts` メソッドを委任します。  
  
## <a name="see-also"></a>参照  
 [IActiveScriptDebug インターフェイス](../../winscript/reference/iactivescriptdebug-interface.md)   
 [IDebugDocumentContext::EnumCodeContexts](../../winscript/reference/idebugdocumentcontext-enumcodecontexts.md)