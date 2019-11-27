---
title: 'IActiveScriptAuthor:: Getscript・ Textattributes |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptAuthor.GetScriptletTextAttributes
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptAuthor::GetScriptletTextAttributes
ms.assetid: 082edfce-6c5b-4e5e-b942-31b423a4fa1d
caps.latest.revision: 10
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 4cd0090b9ade47ad37acf6d285ec7f072f1ea5af
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72576170"
---
# <a name="iactivescriptauthorgetscriptlettextattributes"></a>IActiveScriptAuthor::GetScriptletTextAttributes
スクリプトレットのテキスト属性を返します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT GetScriptletTextAttributes(  
   LPCOLESTR pszCode,  
   ULONG cch,  
   LPCOLESTR pszDelimiter,  
   DWORD dwFlags,  
   SOURCE_TEXT_ATTR *pattr  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pszCode`  
 [in、size_is (`cch`)]スクリプトレットのテキスト。 この文字列は null で終了する必要はありません。  
  
 `cch`  
 から`pszCode` パラメーターと `pattr` パラメーターに使用されるサイズ。  
  
 `pszDelimiter`  
 からスクリプトレットの末尾の区切り記号のアドレス。 テキストのストリームから `pszCode` を解析する場合、ホストは通常、スクリプトレットの末尾を検出するために区切り記号 (2 つの単一引用符など) を使用します。 スクリプトレットの末尾を識別するために区切り記号を使用しない場合は、このパラメーターを NULL に設定します。  
  
 `dwFlags`  
 からスクリプトレットのテキスト属性に関連付けられているフラグ。 には、次の値の組み合わせを指定できます。  
  
|定数|値|説明|  
|--------------|-----------|-----------------|  
|GETATTRTYPE_DEPSCAN|0x0001|SOURCETEXT_ATTR_IDENTIFIER 属性を持つ識別子を識別し、SOURCETEXT_ATTR_MEMBERLOOKUP 属性を持つドット演算子を識別します。|  
|GETATTRFLAG_THIS|0x0100|SOURCETEXT_ATTR_THIS 属性を持つ現在のオブジェクトを識別します。|  
|GETATTRFLAG_HUMANTEXT|0x8000|SOURCETEXT_ATTR_HUMANTEXT 属性を持つ文字列の内容とコメントテキストを識別します。|  
  
 `pattr`  
 [in、out、size_is (`cch`)]スクリプトレットコードの色情報。  
  
## <a name="return-value"></a>戻り値  
 `HRESULT`。 有効な値を次の表に示しますが、これ以外にもあります。  
  
|値|説明|  
|-----------|-----------------|  
|`S_OK`|メソッドが成功しました。|  
  
## <a name="remarks"></a>コメント  
  
## <a name="see-also"></a>参照  
 [IActiveScriptAuthor インターフェイス](../../winscript/reference/iactivescriptauthor-interface.md)   
 [IActiveScriptAuthor:: GetScriptTextAttributes](../../winscript/reference/iactivescriptauthor-getscripttextattributes.md)   
 [SOURCE_TEXT_ATTR 列挙型](../../winscript/reference/source-text-attr-enumeration.md)