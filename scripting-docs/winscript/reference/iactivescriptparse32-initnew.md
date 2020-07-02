---
title: 'IActiveScriptParse32:: InitNew |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 7c77aa16-f391-4c93-9f1a-4e529a9930b2
caps.latest.revision: 3
author: mikejo5000
ms.author: mikejo
ms.openlocfilehash: 887e4ce44662cc591fee64f5e0549edcdcbc14af
ms.sourcegitcommit: 9a9c61ca115c22d33bb902153eb0853789c7be4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85835707"
---
# <a name="iactivescriptparse32initnew"></a>IActiveScriptParse32::InitNew
スクリプトエンジンを初期化します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT InitNew(void);  
```  
  
## <a name="return-value"></a>戻り値  
 `S_OK`成功した場合はを返し、 `E_FAIL` 初期化中にエラーが発生した場合はを返します。  
  
## <a name="remarks"></a>Remarks  
 スクリプトエンジンを使用する前に、 `IPersist*::Load` 、 `IPersist*::InitNew` 、またはのいずれかのメソッドを呼び出す必要があります `IActiveScriptParse32::InitNew` 。 このメソッドのセマンティクスはと同じ `IPersistStreamInit::InitNew` であり、このメソッドはスクリプトエンジンに対して自身を初期化するように指示します。 またはとの両方を呼び出すことはできません `IPersist*::InitNew` 。また、 `IActiveScriptParse32::InitNew` 、、 `IPersist*::Load` `IPersist*::InitNew` `IActiveScriptParse32::InitNew` またはを複数回呼び出すことも有効 `IPersist*::Load` ではありません。  
  
## <a name="see-also"></a>関連項目  
 [IActiveScriptParse32](../../winscript/reference/iactivescriptparse32.md)