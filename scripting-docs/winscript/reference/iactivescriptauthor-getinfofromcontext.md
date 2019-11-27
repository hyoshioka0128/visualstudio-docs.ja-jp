---
title: 'IActiveScriptAuthor:: GetInfoFromContext |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptAuthor.GetInfoFromContext
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptAuthor::GetInfoFromContext
ms.assetid: 9891b095-6eb5-4473-87c0-c2e5cd2afc1a
caps.latest.revision: 15
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: b8b9ad4677d580d495c72866be57712476d6a9c7
ms.sourcegitcommit: dcbb876a5dd598f2538e62e1eabd4dc98595b53a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/28/2019
ms.locfileid: "72985325"
---
# <a name="iactivescriptauthorgetinfofromcontext"></a>IActiveScriptAuthor::GetInfoFromContext
コードブロック内の指定された文字の型情報とアンカー位置を返します。 これにより、メンバーの IntelliSense、グローバルリスト、およびパラメーターのヒントに関する情報が提供されます。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT GetInfoFromContext(  
   LPCOLESTR  pszCode,  
   ULONG      cchCode,  
   ULONG      ichCurrentPosition,  
   DWORD      dwListTypesRequested,  
   DWORD      *pdwListTypesProvided,  
   ULONG      *pichListAnchorPosition,  
   ULONG      *pichFuncAnchorPosition,  
   MEMBERID   *pmemid,  
   LONG       *piCurrentParameter,  
   IUnknown   **ppunk  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pszCode`  
 から情報の結果を生成するために使用されるコードブロック文字列のアドレス。  
  
 `cchCode`  
 からコードブロックの長さ。  
  
 `ichCurrentPosition`  
 からブロックの先頭を基準とした文字の位置。  
  
 `dwListTypesRequested`  
 から要求されたリストの型。 は、次の値の組み合わせにすることができます。  
  
|定数|値|説明|  
|--------------|-----------|-----------------|  
|SCRIPT_CMPL_NOLIST|0x0000|リストがありません。|  
|SCRIPT_CMPL_MEMBERLIST|0x0001|メンバーリスト。|  
|SCRIPT_CMPL_ENUMLIST|0x0002|列挙型リスト。|  
|SCRIPT_CMPL_PARAMLIST|0x0004|メソッドのパラメーターリストを呼び出します。|  
|SCRIPT_CMPL_GLOBALLIST|0x0008|グローバルリスト。|  
  
 SCRIPT_CMPL_GLOBALLIST 型は、または演算子を使用して他の完了項目と組み合わせることができる既定の完了項目として扱われます。 スクリプト作成エンジンは、まず、他の入力候補リスト項目の型情報を設定しようとします。 失敗した場合、エンジンは SCRIPT_CMPL_GLOBALLIST を設定します。  
  
 `pdwListTypesProvided`  
 入出力指定されたリストの種類。  
  
 `pichListAnchorPosition`  
 入出力現在の位置を格納しているコンテキストの開始インデックス。 開始インデックスは、ブロックの開始位置を基準としています。  
  
 この値は、`dwListTypesRequested` に SCRIPT_CMPL_MEMBERLIST、SCRIPT_CMPL_ENUMLIST、または SCRIPT_CMPL_GLOBALLIST が含まれている場合にのみ設定されます。 要求された他のリスト型の場合、結果は未定義になります。  
  
 `pichFuncAnchorPosition`  
 入出力現在の位置を含む関数呼び出しの開始インデックス。 開始インデックスは、ブロックの開始位置を基準としています。  
  
 この値は、現在の位置を含むコンテキストが関数呼び出しであり、`dwListTypesRequested` に SCRIPT_CMPL_PARAMLIST が含まれている場合にのみ設定されます。 それ以外の場合、結果は未定義になります。  
  
 `pmemid`  
 入出力`IProvideMultipleClassInfo``ppunk` out パラメーターの型によって定義される関数の MEMBERID。  
  
 この値は、`dwListTypesRequested` に SCRIPT_CMPL_PARAMLIST が含まれている場合にのみ設定されます。  
  
 `piCurrentParameter`  
 入出力現在の位置を格納しているパラメーターのインデックス。 現在の位置が関数名にある場合は、-1 が返されます。  
  
 `piCurrentParameter` 値は、`dwListTypesRequested` に SCRIPT_CMPL_PARAMLIST が含まれている場合にのみ設定されます。  
  
 `ppunk`  
 型情報。 `IProvideMultipleClassInfo` オブジェクトの形式で提供されます。  
  
## <a name="return-value"></a>戻り値  
 `HRESULT`。 有効な値を次の表に示しますが、これ以外にもあります。  
  
|値|説明|  
|-----------|-----------------|  
|`S_OK`|メソッドが成功しました。|  
  
## <a name="remarks"></a>コメント  
  
## <a name="see-also"></a>参照  
 [IProvideMultipleClassInfo インターフェイス](/dotnet/api/microsoft.visualstudio.ole.interop.iprovidemultipleclassinfo)   
 [IActiveScriptAuthor インターフェイス](../../winscript/reference/iactivescriptauthor-interface.md)