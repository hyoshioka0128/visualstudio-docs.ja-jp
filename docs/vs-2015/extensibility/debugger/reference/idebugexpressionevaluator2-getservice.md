---
title: 'IDebugExpressionEvaluator2:: GetService |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- IDebugExpressionEvaluator2::GetService
- GetService
ms.assetid: f8988a9e-9d18-42af-84a7-55f41e9adf63
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: af73b23cfaf0b282403e8e6a94d6f05db419bd41
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62540343"
---
# <a name="idebugexpressionevaluator2getservice"></a>IDebugExpressionEvaluator2::GetService
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

一意の識別子を指定して、サービスオブジェクトを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT GetService (  
   GUID        uid,  
   IUnknown ** ppService  
);  
```  
  
```csharp  
int GetService (  
   Guid       uid,  
   out object ppService  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `uid`  
 から取得するサービスの一意識別子。  
  
 `ppService`  
 入出力サービスを表すオブジェクトを返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 これは、別の式エバリュエーターからサービスを取得するために、サードパーティの式エバリュエーターによって使用される場合があります。 たとえば、このメソッドを使用して、ビジュアライザーサービスのインターフェイスを既定の式エバリュエーターから取得できます。 サードパーティの式エバリュエーターは、このインターフェイスを実装する必要がない可能性があります。  
  
## <a name="see-also"></a>参照  
 [IDebugExpressionEvaluator2](../../../extensibility/debugger/reference/idebugexpressionevaluator2.md)
