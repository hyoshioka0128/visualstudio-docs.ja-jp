---
title: 'IDebugDocumentHost:: GetScriptTextAttributes |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugDocumentHost.GetScriptTextAttributes
apilocation:
- scrobj.dll
helpviewer_keywords:
- IDebugDocumentHost::GetScriptTextAttributes
ms.assetid: fe459d0d-937f-4176-be81-99d5cca121a1
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 3b18f4f49fa157b78e4f1fd6c7766e929890a6c6
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72569206"
---
# <a name="idebugdocumenthostgetscripttextattributes"></a>IDebugDocumentHost::GetScriptTextAttributes
ドキュメントテキストのブロックのテキスト属性を返します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT GetScriptTextAttributes(  
   LPCOLESTR          pstrCode,  
   ULONG              uNumCodeChars,  
   LPCOLESTR          pstrDelimiter,  
   DWORD              dwFlags,  
   SOURCE_TEXT_ATTR*  pattr  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pstrCode`  
 からスクリプトブロックのテキスト。 この文字列を null で終了する必要はありません。  
  
 `uNumCodeChars`  
 からスクリプトブロックテキスト内の文字数。  
  
 `pstrDelimiter`  
 からスクリプトの終了ブロックの区切り記号のアドレス。 テキストのストリームから `pstrCode` を解析する場合、ホストは通常、2つの単一引用符 (' ') などの区切り記号を使用して、スクリプトブロックの終了を検出します。 このパラメーターには、ホストが使用する区切り文字を指定します。それにより、スクリプト エンジンで何らかの条件付きのプリミティブな前処理が可能になります (単一引用符 (') を区切り文字として使用するために 2 つの単一引用符に置き換えるなど)。 スクリプトエンジンがこの情報を使用する方法 (および if) は、スクリプトエンジンによって異なります。 ホストがスクリプトブロックの末尾を示すために区切り記号を使用しなかった場合は、このパラメーターを NULL に設定します。  
  
 `dwFlags`  
 からスクリプトブロックに関連付けられているフラグ。 次の値の組み合わせが可能です。  
  
|定数|値|説明|  
|--------------|-----------|-----------------|  
|GETATTRTYPE_DEPSCAN|0x0001|識別子とドット演算子をそれぞれ SOURCETEXT_ATTR_IDENTIFIER と SOURCETEXT_ATTR_MEMBERLOOKUP のフラグで識別する必要があることを示します。|  
|GETATTRFLAG_THIS|0x0100|現在のオブジェクトの識別子を SOURCETEXT_ATTR_THIS フラグで識別する必要があることを示します。|  
|GETATTRFLAG_HUMANTEXT|0x8000|文字列の内容とコメントのテキストを SOURCETEXT_ATTR_HUMANTEXT フラグで識別する必要があることを示します。|  
  
 `pattr`  
 [入力、出力]返された属性を格納するバッファー。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは `HRESULT` を返します。 有効な値を次の表に示しますが、これ以外にもあります。  
  
|値|説明|  
|-----------|-----------------|  
|`S_OK`|メソッドが成功しました。|  
|`E_NOTIMPL`|ホストは既定の属性のみを使用します。|  
  
## <a name="remarks"></a>コメント  
 このメソッドは、ドキュメントテキストの任意のブロックのテキスト属性を返します。 ホストが `E_NOTIMPL`を返すことは許容されます。この場合、既定の属性が使用されます。  
  
## <a name="see-also"></a>参照  
 [IDebugDocumentHost インターフェイス](../../winscript/reference/idebugdocumenthost-interface.md)   
 [SOURCE_TEXT_ATTR 列挙型](../../winscript/reference/source-text-attr-enumeration.md)