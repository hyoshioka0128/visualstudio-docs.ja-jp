---
title: 'IDebugReference2:: SetValueAsReference |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugReference2::SetValueAsReference
helpviewer_keywords:
- IDebugReference2::SetValueAsReference
ms.assetid: 94a545d2-16b9-45e9-b2e7-4e49ff90aad0
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2b14ca1293a709dce35f2e8aa45a7fa22bf29845
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68178188"
---
# <a name="idebugreference2setvalueasreference"></a>IDebugReference2::SetValueAsReference
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

別の参照から参照の値を設定します。 将来使用するために予約されています。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT SetValueAsReference (   
   IDebugReference2** rgpArgs,  
   DWORD              dwArgCount,  
   IDebugReference2*  pValue,  
   DWORD              dwTimeout  
);  
```  
  
```cpp#  
int SetValueAsReference (   
   IDebugReference2[] rgpArgs,  
   uint               dwArgCount,  
   IDebugReference2   pValue,  
   uint               dwTimeout  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `rgpArgs`  
 から参照値の設定方法を決定するために使用される [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md) オブジェクトの配列。  
  
 `dwArgCount`  
 から配列内の参照の数。  
  
 `pValue`  
 からプロパティ値の設定元の [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md) オブジェクト。  
  
 `dwTimeout`  
 からこのメソッドから戻る前に待機する最大時間 (ミリ秒単位)。 `INFINITE`無期限に待機するには、を使用します。  
  
## <a name="return-value"></a>戻り値  
 常に `E_NOTIMPL` を返します。  
  
## <a name="see-also"></a>参照  
 [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)
