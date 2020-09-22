---
title: 'IDebugObject2:: IsEncOutdated |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugObject2::IsEncOutdated
helpviewer_keywords:
- IDebugObject2::IsEncOutdated method
ms.assetid: d3a8c02d-895b-478c-9957-d663130f308e
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: fa4acd0476a0df75644738840da562db97a34bf6
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841600"
---
# <a name="idebugobject2isencoutdated"></a>IDebugObject2::IsEncOutdated
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このメソッドは、このオブジェクトまたは親コンテナーのエディットコンティニュの状態が古いかどうかを判断します。 カスタム式エバリュエーターでは、このメソッドは実装されず、常にを返し `E_NOTIMPL` ます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT IsEncOutdated(  
   BOOL* pfEncOutdated  
);  
```  
  
```csharp  
int IsEncOutdated(  
   out int pfEncOutdated  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pfEncOutdated`  
 入出力`TRUE`エディットコンティニュの状態が古い場合は0以外 ()。それ以外の場合は 0 ( `FALSE` )。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
> [!NOTE]
> カスタム式エバリュエーターは常にを返す必要があり `E_NOTIMPL` ます。  
  
## <a name="see-also"></a>参照  
 [IDebugObject2](../../../extensibility/debugger/reference/idebugobject2.md)
