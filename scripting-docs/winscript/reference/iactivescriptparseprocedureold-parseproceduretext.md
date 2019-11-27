---
title: IActiveScriptParseProcedureOld::P arseProcedureText |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptParseProcedureOld.ParseProcedureText
apilocation:
- jscript.dll
helpviewer_keywords:
- IActiveScriptParseProcedureOld::ParseProcedureText
ms.assetid: 21a21313-35ce-432d-b9a6-7999065f19ac
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 116cbc7fac0d53b55c9766945d56ecebd27b6785
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72577449"
---
# <a name="iactivescriptparseprocedureoldparseproceduretext"></a>IActiveScriptParseProcedureOld::ParseProcedureText
指定されたコードプロシージャを解析し、名前空間に匿名プロシージャを追加します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT ParseProcedureText(  
   LPCOLESTR    pstrCode,  
   LPCOLESTR    pstrFormalParams,  
   LPCOLESTR    pstrItemName,  
   IUnknown*    punkContext,  
   LPCOLESTR    pstrDelimiter,  
   DWORD_PTR    dwSourceContextCookie,  
   ULONG        ulStartingLineNumber,  
   DWORD        dwFlags,  
   IDispatch**  ppdisp  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pstrCode`  
 から評価するプロシージャテキスト。 この文字列の解釈はスクリプト言語によって異なります。  
  
 `pstrFormalParams`  
 からプロシージャの仮パラメーター名。 パラメーター名は、スクリプトエンジンの適切な区切り記号で区切る必要があります。 名前をかっこで囲むことはできません。  
  
 `pstrItemName`  
 からプロシージャを評価するコンテキストを提供する名前付きアイテムの名前。 このパラメーターが `NULL`場合、コードはスクリプトエンジンのグローバルコンテキストで評価されます。  
  
 `punkContext`  
 からコンテキストオブジェクト。 このオブジェクトはデバッグ環境用に予約されています。アクティブなランタイム コンテキストを表すためにデバッガーによって指定される場合があります。 このパラメーターが `NULL`場合、エンジンは `pstrItemName` を使用してコンテキストを識別します。  
  
 `pstrDelimiter`  
 からプロシージャの末尾の区切り記号。 テキストのストリームから `pstrCode` を解析する場合、ホストは通常、2つの単一引用符 (' ') などの区切り記号を使用して、プロシージャの終了を検出します。 このパラメーターは、ホストが使用する区切り記号を指定します。これにより、スクリプトエンジンはいくつかの条件付きのプリミティブなプリプロセスを提供できます (たとえば、区切り記号として使用するために単一引用符 ['] を2つの単一引用符に置き換えるなど)。 スクリプトエンジンがこの情報を使用する方法 (および if) は、スクリプトエンジンによって異なります。 ホストが区切り記号を使用してプロシージャの終了をマークしなかった場合は、このパラメーターを `NULL` に設定します。  
  
 `dwSourceContextCookie`  
 からデバッグの目的で使用されるアプリケーション定義の値。  
  
 `ulStartingLineNumber`  
 から解析を開始する行を指定する0から始まる値。  
  
 `dwFlags`  
 からプロシージャに関連付けられているフラグ。 は、これらの値の組み合わせにすることができます。  
  
|定数|値|意味|  
|--------------|-----------|-------------|  
|SCRIPTPROC_ISEXPRESSION|0x00000020|`pstrCode` 内のコードが、プロシージャの戻り値を表す式であることを示します。|  
|SCRIPTPROC_IMPLICIT_THIS|0x00000100|`this` ポインターがプロシージャのスコープに含まれることを示します。|  
|SCRIPTPROC_IMPLICIT_PARENTS|0x00000200|`this` ポインターの親がプロシージャのスコープに含まれることを示します。|  
  
 `ppdisp`  
 入出力既定のメソッドがこのメソッドによって解析されるプロシージャであるディスパッチラッパーを返します。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは `HRESULT` を返します。 有効な値を次の表に示しますが、これ以外にもあります。  
  
|値|説明|  
|-----------|-----------------|  
|`S_OK`|メソッドが成功しました。|  
|`E_INVALIDARG`|引数が無効です。|  
|`E_POINTER`|無効なポインターが指定されました。|  
|`E_NOTIMPL`|このメソッドはサポートされていません。 スクリプトエンジンでは、名前空間に対するプロシージャの実行時追加はサポートされていません。|  
|`E_UNEXPECTED`|呼び出しは想定されていませんでした (たとえば、スクリプトエンジンが初期化されていない状態か、閉じられた状態です)。|  
|`OLESCRIPT_E_SYNTAX`|プロシージャで、指定されていない構文エラーが発生しました。|  
|`S_FALSE`|スクリプトエンジンはディスパッチオブジェクトをサポートしていません。`ppdisp`パラメーターが `NULL`に設定されています。|  
  
## <a name="remarks"></a>コメント  
 この呼び出し中に評価されるスクリプトコードはありません。代わりに、プロシージャを `ppdisp` のメソッドにコンパイルして、後でスクリプトによって呼び出すことができます。  
  
 このインターフェイスは、`IActiveScriptParseProcedure` インターフェイスを優先して非推奨とされます。 `IActiveScriptParseProcedure::ParseProcedureText` メソッドはこのメソッドに似ていますが、プロシージャ名を指定することができます。 どのような状況でも、`IActiveScriptParseProcedure::ParseProcedureText` を使用する必要があります。  
  
## <a name="see-also"></a>参照  
 [IActiveScriptParseProcedureOld インターフェイス](../../winscript/reference/iactivescriptparseprocedureold-interface.md)   
 [IActiveScriptParseProcedure::ParseProcedureText](../../winscript/reference/iactivescriptparseprocedure-parseproceduretext.md)