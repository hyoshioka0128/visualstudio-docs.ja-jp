---
title: 'IEEVisualizerServiceProvider:: CreateVisualizerService |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IEEVisualizerServiceProvider::CreateVisualizerService
helpviewer_keywords:
- IEEVisualizerServiceProvider::CreateVisualizerService method
ms.assetid: f366f7c9-358d-46c8-993f-32ff86539833
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: ed8327690c42f54a33209b2f0acfa45a138ec51c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68155085"
---
# <a name="ieevisualizerserviceprovidercreatevisualizerservice"></a>IEEVisualizerServiceProvider::CreateVisualizerService
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このメソッドは、ビジュアライザーサービスを作成します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT CreateVisualizerService(  
   IDebugBinder*              binder,  
   IDebugSymbolProvider*      pSymProv,  
   IDebugAddress*             pAddress,  
   IEEVisualizerDataProvider* dataProvider,  
   IEEVisualizerService**     ppService  
);  
```  
  
```csharp  
int CreateVisualizerService(  
   IDebugBinder binder,  
   IDebugSymbolProvider      pSymProv,  
   IDebugAddress             pAddress,  
   IEEVisualizerDataProvider dataProvider,  
   out IEEVisualizerService  ppService  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `binder`  
 から[EvaluateSync](../../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)に渡される[IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)オブジェクト。  
  
 `pSymProv`  
 からに渡される [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md) オブジェクト `IDebugParsedExpression::EvaluateSync` 。  
  
 `pAddress`  
 からに渡される [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) オブジェクト `IDebugParsedExression::EvaluateSync` 。  
  
 `dataProvider`  
 から [Ieevisualizerdataprovider](../../../extensibility/debugger/reference/ieevisualizerdataprovider.md) インターフェイス (式エバリュエーターによって提供される) を実装するオブジェクト。  
  
 `ppService`  
 入出力作成されたサービス。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 、、およびの各パラメーターは、 `binder` `pSymProv` `pAddress` すべてメソッドに渡されました `IDebugParsedExpression::EvaluateSync` 。 `CreateVisualizerService` は `IDebugParsedExpression::EvaluateSync` 、式エバリュエーターによる型ビジュアライザーのサポートの一部として、からのみ呼び出されます。  
  
## <a name="see-also"></a>参照  
 [IEEVisualizerServiceProvider](../../../extensibility/debugger/reference/ieevisualizerserviceprovider.md)   
 [EvaluateSync](../../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)   
 [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)   
 [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)   
 [IEEVisualizerDataProvider](../../../extensibility/debugger/reference/ieevisualizerdataprovider.md)
