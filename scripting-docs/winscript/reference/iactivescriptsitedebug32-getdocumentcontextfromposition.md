---
title: 'IActiveScriptSiteDebug32:: GetDocumentContextFromPosition |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 53348dff-35a6-4303-b263-90c10af06bf3
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
ms.openlocfilehash: b43b16f46cc62b6c70460d79c194b5e0d2cfede0
ms.sourcegitcommit: 9a9c61ca115c22d33bb902153eb0853789c7be4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85835278"
---
# <a name="iactivescriptsitedebug32getdocumentcontextfromposition"></a>IActiveScriptSiteDebug32::GetDocumentContextFromPosition
言語エンジンがを委任するために使用し `IDebugCodeContext::GetSourceContext` ます。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT GetDocumentContextFromPosition(  
   DWORD_PTR                dwSourceContext,  
   ULONG                    uCharacterOffset,  
   ULONG                    uNumChars,  
   IDebugDocumentContext**  ppsc  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `dwSourceContext`  
 からまたはに提供されるソースコンテンツ `ParseScriptText` `AddScriptlet` 。  
  
 `uCharacterOffset`  
 からスクリプトブロックまたはスクリプトレットの開始位置を基準とした文字オフセット。  
  
 `uNumChars`  
 からこのコンテキストの文字数。  
  
 `ppsc`  
 入出力この文字位置の範囲に対応するドキュメントコンテキスト。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは `HRESULT` を返します。 有効な値を次の表に示しますが、これ以外にもあります。  
  
|[値]|説明|  
|-----------|-----------------|  
|`S_OK`|メソッドが成功しました。|  
  
## <a name="remarks"></a>Remarks  
 言語エンジンは、このメソッドを使用してを委任 `IDebugCodeContext::GetSourceContext` します。  
  
## <a name="see-also"></a>関連項目  
 [IActiveScriptSiteDebug32 インターフェイス](../../winscript/reference/iactivescriptsitedebug32-interface.md)