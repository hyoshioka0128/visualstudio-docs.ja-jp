---
title: 'IScriptNode:: CreateChildEntry |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IScriptNode. CreateChildEntry
apilocation:
- scrobj.dll
helpviewer_keywords:
- IScriptNode::CreateChildEntry
ms.assetid: b9682505-4457-40e9-8691-235843637506
caps.latest.revision: 17
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: c58ff83c43a1418e6fb7bd8945afa181af60c68a
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72573618"
---
# <a name="iscriptnode-createchildentry"></a>IScriptNode::CreateChildEntry
`IScriptEntry`の子インスタンスを追加します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT CreateChildEntry(  
   ULONG              isn,  
   DWORD              dwCookie,  
   LPCOLESTR          pszDelimiter,  
   IScriptEntry       **ppse  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `isn`  
 から親の子のインデックス。  
  
 `dwCookie`  
 から子エントリをホストオブジェクトに関連付けるために使用されるアプリケーション定義の値。  
  
 `pszDelimiter`  
 からスクリプトの終了ブロックの区切り記号のアドレス。 解析の場合、ホストは通常、スクリプトブロックの終了を検出するために区切り記号 (2 つの単一引用符など) を使用します。  
  
 区切り記号を使用すると、スクリプト作成エンジンで前処理を行うことができます。 たとえば、区切り記号として使用する単一引用符を2つの単一引用符で置き換えることができます。 エンジンは、区切り記号の使用方法を決定します。  
  
 区切り記号によってスクリプトブロックの終了がマークされない場合は、NULL に設定します。  
  
 `ppse`  
 入出力子インスタンスの `IScriptEntry` インターフェイスへのポインターを受け取る変数のアドレス。  
  
 Web ページを表す `IScriptNode` オブジェクトの場合、このパラメーターは、スクリプトブロックを指定する `IScriptEntry` インスタンスを返します。  
  
 スクリプトブロックを表す `IScriptEntry` オブジェクトの場合、このパラメーターは関数オブジェクトを指定する `IScriptEntry` インスタンスを返します。  
  
 関数オブジェクトを表す `IScriptEntry` オブジェクトの場合、このメソッドは失敗します。  
  
 `IScriptScriptlet` オブジェクトの場合、このメソッドは失敗します。  
  
## <a name="return-value"></a>戻り値  
 `HRESULT`。 有効な値を次の表に示しますが、これ以外にもあります。  
  
|値|説明|  
|-----------|-----------------|  
|`S_OK`|メソッドが成功しました。|  
  
## <a name="remarks"></a>コメント  
 `IScriptNode` インターフェイスは、Web ページまたはその要素を表します。 `IScriptEntry` インターフェイス (`IScriptNode`から派生) は、スクリプトブロックまたは関数オブジェクトを表します。 `IScriptScriptlet` インターフェイス (`IScriptEntry`から派生) は、イベントハンドラーを表します。  
  
## <a name="see-also"></a>参照  
 [Iscriptnode インターフェイス](../../winscript/reference/iscriptnode-interface.md)   
 [IScriptEntry インターフェイス](../../winscript/reference/iscriptentry-interface.md)