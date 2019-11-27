---
title: 'IActiveScriptDebug:: Getscript・ Textattributes |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptDebug.GetScriptletTextAttributes
apilocation:
- jscript.dll
helpviewer_keywords:
- IActiveScriptDebug::GetScriptletTextAttributes
ms.assetid: b3990d86-5fdf-4c9f-9678-3f4b808c7ca8
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 6a5dd9e219e51b001659225636396fe45ac815b9
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72572801"
---
# <a name="iactivescriptdebuggetscriptlettextattributes"></a>IActiveScriptDebug::GetScriptletTextAttributes
任意のスクリプトレットのテキスト属性を返します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT GetScriptletTextAttributes(  
   LPCOLESTR          pstrCode,  
   ULONG              uNumCodeChars,  
   LPCOLESTR          pstrDelimiter,  
   DWORD              dwFlags,  
   SOURCE_TEXT_ATTR*  pattr  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pstrCode`  
 からスクリプトレットのテキスト。 この文字列を null で終了することはできません。  
  
 `uNumCodeChars`  
 からスクリプトレットテキストの文字数。  
  
 `pstrDelimiter`  
 [入力] スクリプトレット末尾の区切り記号のアドレス。 `pstrCode` がテキストのストリームから解析されるとき、ホストは通常、2 つの単一引用符 ('') などの区切り文字を使用してスクリプトレットの末尾を検出します。 このパラメーターには、ホストが使用する区切り文字を指定します。それにより、スクリプト エンジンで何らかの条件付きのプリミティブな前処理が可能になります (単一引用符 (') を区切り文字として使用するために 2 つの単一引用符に置き換えるなど)。 スクリプトエンジンがこの情報を使用する方法 (および if) は、スクリプトエンジンによって異なります。 ホストがスクリプトレットの末尾を示すために区切り記号を使用しなかった場合は、このパラメーターを NULL に設定します。  
  
 `dwFlags`  
 [入力] スクリプトレットに関連付けられるフラグ。 次の値の組み合わせが可能です。  
  
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
  
## <a name="remarks"></a>コメント  
 `IDebugDocumentText` インターフェイスを実装するスマートホストは、このメソッドを使用して、`IDebugDocumentText::GetText` メソッドへの呼び出しを委任できます。  
  
 この呼び出しは、スクリプトレットが式であり、スクリプトブロックとは構文が異なる場合があるために提供されます。 同じ構文の場合、このメソッドの実装は `GetScriptTextAttributes` メソッドの実装と同じになります。  
  
## <a name="see-also"></a>参照  
 [IActiveScriptDebug インターフェイス](../../winscript/reference/iactivescriptdebug-interface.md)   
 [IActiveScriptDebug:: GetScriptTextAttributes](../../winscript/reference/iactivescriptdebug-getscripttextattributes.md)   
 [IDebugDocumentText インターフェイス](../../winscript/reference/idebugdocumenttext-interface.md)   
 [IDebugDocumentText:: GetText](../../winscript/reference/idebugdocumenttext-gettext.md)   
 [SOURCE_TEXT_ATTR 列挙型](../../winscript/reference/source-text-attr-enumeration.md)