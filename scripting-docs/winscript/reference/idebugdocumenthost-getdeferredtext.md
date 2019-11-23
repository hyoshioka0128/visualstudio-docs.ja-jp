---
title: 'IDebugDocumentHost:: GetDeferredText |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugDocumentHost.GetDeferredText
apilocation:
- scrobj.dll
helpviewer_keywords:
- IDebugDocumentHost::GetDeferredText
ms.assetid: 527da666-fef5-4db3-a319-e68d466a7721
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 273b4eb52b7263d34c347dff3a00479945b809df
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72569422"
---
# <a name="idebugdocumenthostgetdeferredtext"></a>IDebugDocumentHost::GetDeferredText
元のホストドキュメントで `IDebugDocumentHelper::AddDeferredText` メソッドを使用して追加された文字の範囲を返します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT GetDeferredText(  
   DWORD              dwTextStartCookie,  
   WCHAR*             pcharText,  
   SOURCE_TEXT_ATTR*  pstaTextAttr,  
   ULONG*             pcNumChars,  
   ULONG              cMaxChars  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `dwTextStartCookie`  
 からテキストの開始位置を表すホスト定義のクッキー。  
  
 `pcharText`  
 [入力、出力]文字テキストバッファー。 このパラメーターが `NULL`場合、このメソッドは文字を返しません。  
  
 `pstaTextAttr`  
 [入力、出力]文字属性バッファー。 このパラメーターが `NULL`場合、このメソッドは属性を返しません。  
  
 `pcNumChars`  
 [入力、出力]返される文字/属性の実際の数を示します。 このメソッドを呼び出す前に、このパラメーターを0に設定する必要があります。  
  
 `cMaxChars`  
 から返す最大文字数。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは `HRESULT` を返します。 有効な値を次の表に示しますが、これ以外にもあります。  
  
|値|説明|  
|-----------|-----------------|  
|`S_OK`|メソッドが成功しました。|  
|`E_NOTIMPL`|このメソッドは実装されていません。|  
  
## <a name="remarks"></a>コメント  
 ホストが `IDebugDocumentHelper::AddDeferredText`を呼び出さない場合、このメソッドは `E_NOTIMPL`を返す可能性があります。  
  
> [!NOTE]
> このメソッドは、元のドキュメントからテキストを返します。 ホストは、ドキュメントに対する編集やその他の変更を追跡しません。  
  
## <a name="see-also"></a>参照  
 [IDebugDocumentHost インターフェイス](../../winscript/reference/idebugdocumenthost-interface.md)   
 [IDebugDocumentHelper:: AddDeferredText](../../winscript/reference/idebugdocumenthelper-adddeferredtext.md)   
 [SOURCE_TEXT_ATTR 列挙型](../../winscript/reference/source-text-attr-enumeration.md)