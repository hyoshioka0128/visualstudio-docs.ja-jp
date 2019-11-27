---
title: 'IScriptNode:: CreateChildHandler |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IScriptNode.CreateChildHandler
apilocation:
- scrobj.dll
helpviewer_keywords:
- IScriptNode::CreateChildHandler
ms.assetid: 4ce5eb10-1a3f-43b0-a4b7-599a397ed3a2
caps.latest.revision: 14
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 9e024bb7d6a81b35994edddfe9e71666b0ee8df0
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72573595"
---
# <a name="iscriptnodecreatechildhandler"></a>IScriptNode::CreateChildHandler
`IScriptNode`の子インスタンスとしてスクリプトレットを追加します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT CreateChildHandler(  
   LPCOLESTR          pszDefaultName,  
   LPCOLESTR          *prgpszNames,  
   ULONG              cpszNames,  
   LPCOLESTR          pszEvent,  
   LPCOLESTR          pszDelimiter,  
   ITypeInfo*         ptiSignature,  
   ULONG              iMethodSignature,  
   ULONG              isn,  
   DWORD              dwCookie,  
   IScriptEntry       **ppse  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pszDefaultName`  
 からスクリプトレットに関連付ける既定の名前のアドレス。  
  
 `prgpszNames`  
 [in、size_is (`cpszNames`)]ホスト上の完全修飾名からの識別子の一覧。  
  
 `cpszNames`  
 から`prgpszNames` パラメーターの識別子の数。  
  
 `pszEvent`  
 からスクリプトレットに関連付けられたイベント名を識別するバッファーアドレス。  
  
 `pszDelimiter`  
 からスクリプトの終了ブロックの区切り記号のアドレス。 解析の場合、ホストは通常、スクリプトブロックの終了を検出するために区切り記号 (2 つの単一引用符など) を使用します。  
  
 区切り記号によって、スクリプト作成エンジンによる前処理が有効になります。 たとえば、区切り記号として使用する単一引用符を2つの単一引用符で置き換えることができます。 エンジンは、区切り記号の使用方法を決定します。  
  
 スクリプトブロックの末尾を識別するために区切り記号を使用しない場合は、NULL に設定します。  
  
 `ptiSignature`  
 から関数オブジェクトの型情報。  
  
 `iMethodSignature`  
 から`ITypeInfo``ptiSignature` パラメーター内の関数のインデックス。  
  
 `isn`  
 から親の子のインデックス。  
  
 `dwCookie`  
 からエントリをホストオブジェクトに関連付けるために使用されるアプリケーション定義の値。  
  
 `ppse`  
 入出力子インスタンスの `IScriptEntry` インターフェイスへのポインターを受け取る変数のアドレス。  
  
## <a name="return-value"></a>戻り値  
 `HRESULT`。 有効な値を次の表に示しますが、これ以外にもあります。  
  
|値|説明|  
|-----------|-----------------|  
|`S_OK`|メソッドが成功しました。|  
  
## <a name="remarks"></a>コメント  
 スクリプトレットは、イベントハンドラーを指定します。 このメソッドは、Web ページを表す `IScriptNode` オブジェクトによって呼び出された場合に、スクリプトレットを作成します。 このメソッドは、他のインターフェイスによって呼び出された場合は成功しません。  
  
## <a name="see-also"></a>参照  
 [Iscriptnode インターフェイス](../../winscript/reference/iscriptnode-interface.md)   
 [IScriptEntry インターフェイス](../../winscript/reference/iscriptentry-interface.md)