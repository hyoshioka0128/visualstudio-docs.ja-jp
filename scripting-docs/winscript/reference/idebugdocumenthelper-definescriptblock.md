---
title: IDebugDocumentHelper::D efineScriptBlock |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugDocumentHelper.DefineScriptBlock
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugDocumentHelper::DefineScriptBlock
ms.assetid: e4120377-f04f-44b1-950b-2beba06c9c12
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 6a2418b18e80ac86b672b3847f24ef9084ed1252
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72576973"
---
# <a name="idebugdocumenthelperdefinescriptblock"></a>IDebugDocumentHelper::DefineScriptBlock
特定の範囲の文字が、指定されたスクリプトエンジンによって処理されるスクリプトブロックであることをヘルパーに示します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT DefineScriptBlock(  
   ULONG           ulCharOffset,  
   ULONG           cChars,  
   IActiveScript*  pas,  
   BOOL            fScriptlet,  
   DWORD_PTR*      pdwSourceContext  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `ulCharOffset`  
 からスクリプトブロックの開始位置。  
  
 `cChars`  
 からスクリプトブロック内の文字数。  
  
 `pas`  
 からこのスクリプトブロックのスクリプトエンジン。  
  
 `fScriptlet`  
 からスクリプトブロックがスクリプトレットであるかどうかを示すフラグです。  
  
 `pdwSourceContext`  
 入出力スクリプトブロックのソースコンテキスト。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは `HRESULT` を返します。 有効な値を次の表に示しますが、これ以外にもあります。  
  
|値|説明|  
|-----------|-----------------|  
|`S_OK`|メソッドが成功しました。|  
  
## <a name="remarks"></a>コメント  
 スマートホストは、ドキュメントに埋め込みスクリプトブロックが含まれている場合に、このメソッドを使用できます。 言語エンジンは、そのコードに他の言語用の埋め込みスクリプトが含まれている場合に、このメソッドを使用できます。  
  
 スクリプトエンジンは、すべての構文の色分けと、スクリプトブロック内のコードコンテキストの参照を担当します。  
  
 `DefineScriptBlock` メソッドは、テキストが追加された後 (たとえば、`IDebugDocumentHelper::AddDBCSText` メソッドを使用して)、スクリプトブロックが解析される前に (たとえば、`IActiveScriptParse ::ParseScriptText` メソッドを使用して) 呼び出す必要があります。  
  
## <a name="see-also"></a>参照  
 [IDebugDocumentHelper インターフェイス](../../winscript/reference/idebugdocumenthelper-interface.md)   
 [IDebugDocumentHelper:: AddDBCSText](../../winscript/reference/idebugdocumenthelper-adddbcstext.md)   
 [IDebugDocumentHelper::AddUnicodeText](../../winscript/reference/idebugdocumenthelper-addunicodetext.md)