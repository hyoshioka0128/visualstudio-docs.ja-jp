---
title: 'IDebugDocumentTextEvents:: onInsertText |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugDocumentTextEvents.onInsertText
apilocation:
- scrobj.dll
helpviewer_keywords:
- IDebugDocumentTextEvents::onInsertText
ms.assetid: 775881de-497a-47a9-86ab-823d77745a72
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: c926caf8ff99cf183e41b2caf825aa828fb60de4
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72572905"
---
# <a name="idebugdocumenttexteventsoninserttext"></a>IDebugDocumentTextEvents::onInsertText
新しいテキストがドキュメントに追加されたことを示します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT onInsertText(  
   ULONG  cCharacterPosition,  
   ULONG  cNumToInsert  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `cCharacterPosition`  
 から新しいテキストが挿入された文字位置。  
  
 `cNumToInsert`  
 から挿入された文字数。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは `HRESULT` を返します。 有効な値を次の表に示しますが、これ以外にもあります。  
  
|値|説明|  
|-----------|-----------------|  
|`S_OK`|メソッドが成功しました。|  
  
## <a name="remarks"></a>コメント  
 このメソッドは、通常、Web ブラウザーなどのコンテンツをプログレッシブに読み込むホストによって呼び出されます。  
  
## <a name="see-also"></a>参照  
 [IDebugDocumentTextEvents インターフェイス](../../winscript/reference/idebugdocumenttextevents-interface.md)   
 [IDebugDocumentTextEvents::onRemoveText](../../winscript/reference/idebugdocumenttextevents-onremovetext.md)