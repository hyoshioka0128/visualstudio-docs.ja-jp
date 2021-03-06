---
description: このメソッドは、ビジュアライザーサービスを作成します。
title: 'IEEVisualizerServiceProvider:: CreateVisualizerService |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEEVisualizerServiceProvider::CreateVisualizerService
helpviewer_keywords:
- IEEVisualizerServiceProvider::CreateVisualizerService method
ms.assetid: f366f7c9-358d-46c8-993f-32ff86539833
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b304dd8fe2845cf6c1201e6e128f8b89ec47b1b6
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102222823"
---
# <a name="ieevisualizerserviceprovidercreatevisualizerservice"></a>IEEVisualizerServiceProvider::CreateVisualizerService
このメソッドは、ビジュアライザーサービスを作成します。

## <a name="syntax"></a>構文

```cpp
HRESULT CreateVisualizerService(
   IDebugBinder*              binder,
   IDebugSymbolProvider*      pSymProv,
   IDebugAddress*             pAddress,
   IEEVisualizerDataProvider* dataProvider,
   IEEVisualizerService**     ppService
);
```

```csharp
int CreateVisualizerService(
   IDebugBinder binder,
   IDebugSymbolProvider      pSymProv,
   IDebugAddress             pAddress,
   IEEVisualizerDataProvider dataProvider,
   out IEEVisualizerService  ppService
);
```

## <a name="parameters"></a>パラメーター
`binder`\
から[EvaluateSync](../../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)に渡される[IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)オブジェクト。

`pSymProv`\
からに渡される [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md) オブジェクト `IDebugParsedExpression::EvaluateSync` 。

`pAddress`\
からに渡される [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) オブジェクト `IDebugParsedExression::EvaluateSync` 。

`dataProvider`\
から [Ieevisualizerdataprovider](../../../extensibility/debugger/reference/ieevisualizerdataprovider.md) インターフェイス (式エバリュエーターによって提供される) を実装するオブジェクト。

`ppService`\
入出力作成されたサービス。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
 、、およびの各パラメーターは、 `binder` `pSymProv` `pAddress` すべてメソッドに渡されました `IDebugParsedExpression::EvaluateSync` 。 `CreateVisualizerService` は `IDebugParsedExpression::EvaluateSync` 、式エバリュエーターによる型ビジュアライザーのサポートの一部として、からのみ呼び出されます。

## <a name="see-also"></a>関連項目
- [IEEVisualizerServiceProvider](../../../extensibility/debugger/reference/ieevisualizerserviceprovider.md)
- [EvaluateSync](../../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)
- [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)
- [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)
- [IEEVisualizerDataProvider](../../../extensibility/debugger/reference/ieevisualizerdataprovider.md)
