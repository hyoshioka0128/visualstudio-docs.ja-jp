---
title: 'IDebugDocumentTextEvents:: onRemoveText |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugDocumentTextEvents.onRemoveText
apilocation:
- scrobj.dll
helpviewer_keywords:
- IDebugDocumentTextEvents::onRemoveText
ms.assetid: c5dfe674-c42f-4e57-9d48-8380d5aa206b
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: c302a3b1850db42824f35a306e7e94eaa8a6aa41
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72576261"
---
# <a name="idebugdocumenttexteventsonremovetext"></a>IDebugDocumentTextEvents::onRemoveText
テキストがドキュメントから削除されたことを示します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT onRemoveText(  
   ULONG  cCharacterPosition,  
   ULONG  cNumToRemove  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `cCharacterPosition`  
 から削除された最初の文字の文字位置。  
  
 `cNumToRemove`  
 から削除された文字数。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは `HRESULT` を返します。 有効な値を次の表に示しますが、これ以外にもあります。  
  
|値|説明|  
|-----------|-----------------|  
|`S_OK`|メソッドが成功しました。|  
  
## <a name="remarks"></a>コメント  
 このメソッドは、テキストがドキュメントから削除されたことを示します。  
  
## <a name="see-also"></a>参照  
 [IDebugDocumentTextEvents インターフェイス](../../winscript/reference/idebugdocumenttextevents-interface.md)   
 [IDebugDocumentTextEvents::onInsertText](../../winscript/reference/idebugdocumenttextevents-oninserttext.md)