---
title: 'IDebugDocumentText:: GetText |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugDocumentText.GetText
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugDocumentText::GetText
ms.assetid: 3c940a30-6c0f-4deb-aa4d-21a0bdef8461
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: e6472c40802fff4dad6e5ecc8f2729c95459e09f
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72572072"
---
# <a name="idebugdocumenttextgettext"></a>IDebugDocumentText::GetText
文字位置の範囲に関連付けられている文字または文字の属性を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT GetText(  
   ULONG              cCharacterPosition,  
   WCHAR*             pcharText,  
   SOURCE_TEXT_ATTR*  pstaTextAttr,  
   ULONG*             pcNumChars,  
   ULONG              cMaxChars  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `cCharacterPosition`  
 から文字位置の範囲の開始位置。  
  
 `pcharText`  
 [入力、出力]文字テキストバッファー。 バッファーは `cMaxChars` 文字を保持するのに十分な大きさである必要があります。 このパラメーターが NULL の場合、メソッドは文字を返しません。  
  
 `pstaTextAttr`  
 [入力、出力]文字属性バッファー。 バッファーは `cMaxChars` 文字を保持するのに十分な大きさである必要があります。 このパラメーターが NULL の場合、メソッドは属性を返しません。  
  
 `pcNumChars`  
 [入力、出力]返された文字/属性の数。 このメソッドを呼び出す前に、このパラメーターを0に設定する必要があります。  
  
 `cMaxChars`  
 から文字位置の範囲内の文字数。 返される最大文字数も指定します。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは `HRESULT` を返します。 有効な値を次の表に示しますが、これ以外にもあります。  
  
|値|説明|  
|-----------|-----------------|  
|`S_OK`|メソッドが成功しました。|  
  
## <a name="remarks"></a>コメント  
 このメソッドは、文字位置の範囲に関連付けられている文字または文字の属性を取得します。 文字位置の範囲は、文字位置と文字数で指定します。  
  
## <a name="see-also"></a>参照  
 [IDebugDocumentText インターフェイス](../../winscript/reference/idebugdocumenttext-interface.md)   
 [SOURCE_TEXT_ATTR 列挙型](../../winscript/reference/source-text-attr-enumeration.md)