---
title: 'IDebugDocumentHelper:: Init |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugDocumentHelper.Init
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugDocumentHelper::Init
ms.assetid: 1dd5a01f-0779-4109-8c6c-f16f5a3835bf
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 13e6379052707aa44c0fa52f4cb30db2c4c4fa99
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72576860"
---
# <a name="idebugdocumenthelperinit"></a>IDebugDocumentHelper::Init
`Init` メソッドは、名前と初期属性を使用してデバッグドキュメントヘルパーを初期化します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT Init(  
   IDebugApplication*  pda,  
   LPCOLESTR           pszShortName,  
   LPCOLESTR           pszLongName,  
   TEXT_DOC_ATTR       docAttr  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pda`  
 からこのドキュメントに関連付けられているデバッグアプリケーション。  
  
 `pszShortName`  
 からドキュメントの短い名前を格納している null で終わる文字列。  
  
 `pszLongName`  
 からドキュメントの長い名前を格納している null で終わる文字列。  
  
 `docAttr`  
 からテキストドキュメントの属性を指定します。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは `HRESULT` を返します。 有効な値を次の表に示しますが、これ以外にもあります。  
  
|値|説明|  
|-----------|-----------------|  
|`S_OK`|メソッドが成功しました。|  
  
## <a name="remarks"></a>コメント  
 このメソッドは、名前と初期属性を使用してデバッグドキュメントヘルパーを初期化します。  
  
 `IDebugDocumentHelper::Attach` が呼び出されるまで、このドキュメントはツリーに表示されません。  
  
## <a name="see-also"></a>参照  
 [IDebugDocumentHelper:: Attach](../../winscript/reference/idebugdocumenthelper-attach.md)   
 [IDebugDocumentHelper インターフェイス](../../winscript/reference/idebugdocumenthelper-interface.md)   
 [TEXT_DOC_ATTR 定数](../../winscript/reference/text-doc-attr-constants.md)