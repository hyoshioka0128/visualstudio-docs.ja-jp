---
title: 'IDebugDocumentHelper:: AddDeferredText |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugDocumentHelper.AddDeferredText
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugDocumentHelper::AddDeferredText
ms.assetid: 9463cfb0-76cc-45ee-b32c-f37dce2b2e0e
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 1aae73e44059b1f07fa4cb54f40cdcd12e564a8f
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72577048"
---
# <a name="idebugdocumenthelperadddeferredtext"></a>IDebugDocumentHelper::AddDeferredText
指定されたテキストが使用可能であることをヘルパーに通知しますが、文字は提供しません。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT AddDeferredText(  
   ULONG  cChars,  
   DWORD  dwTextStartCookie  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `cChars`  
 から追加する (Unicode) 文字の数。  
  
 `dwTextStartCookie`  
 からテキストの開始位置を表すホスト定義のクッキー。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは `HRESULT` を返します。 有効な値を次の表に示しますが、これ以外にもあります。  
  
|値|説明|  
|-----------|-----------------|  
|`S_OK`|メソッドが成功しました。|  
|`E_FAIL`|メソッドが失敗しました。|  
  
## <a name="remarks"></a>コメント  
 このメソッドを使用すると、ホストは、必要になるまで追加する文字の指定を遅らせることができ、ヘルパーは正確な通知とサイズ情報を生成できます。 `dwTextStartCookie` パラメーターは、ホストによって定義された、テキストの開始位置を表すクッキーです。 後続の `IDebugDocumentText::GetText` への呼び出しでは、この cookie を提供する必要があります。 たとえば、DBCS のテキストを表すホストでは、cookie にバイトオフセットを指定できます。  
  
 `IDebugDocumentText::GetText` の1回の呼び出しで、`AddDeferredText`の複数の呼び出しから文字を取得できると想定されています。 ヘルパークラスでは、同じ範囲の遅延文字を複数回要求することもできます。  
  
> [!NOTE]
> `AddDeferredText` の呼び出しは、`AddUnicodeText` または `AddDBCSText`の呼び出しと混在させることはできません。 このエラーが発生すると、`E_FAIL` が返されます。  
  
## <a name="see-also"></a>参照  
 [IDebugDocumentHelper インターフェイス](../../winscript/reference/idebugdocumenthelper-interface.md)   
 [IDebugDocumentHelper:: AddUnicodeText](../../winscript/reference/idebugdocumenthelper-addunicodetext.md)   
 [IDebugDocumentHelper:: AddDBCSText](../../winscript/reference/idebugdocumenthelper-adddbcstext.md)   
 [IDebugDocumentText::GetText](../../winscript/reference/idebugdocumenttext-gettext.md)