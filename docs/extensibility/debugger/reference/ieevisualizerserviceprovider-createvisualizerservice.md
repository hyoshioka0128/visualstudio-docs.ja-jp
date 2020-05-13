---
title: IEEビジュアライザーサービスプロバイダー::ビジュアライザーサービスの作成 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEEVisualizerServiceProvider::CreateVisualizerService
helpviewer_keywords:
- IEEVisualizerServiceProvider::CreateVisualizerService method
ms.assetid: f366f7c9-358d-46c8-993f-32ff86539833
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e05677122b7d4e4eb025a9382ede1509374de894
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80717910"
---
# <a name="ieevisualizerserviceprovidercreatevisualizerservice"></a>IEEVisualizerServiceProvider::CreateVisualizerService
このメソッドは、ビジュアライザー サービスを作成します。

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

## <a name="parameters"></a>パラメーター
`binder`\
[in][評価同期](../../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)に渡される[IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)オブジェクト。

`pSymProv`\
[in]に[渡](../../../extensibility/debugger/reference/idebugsymbolprovider.md)されたオブジェクト。 `IDebugParsedExpression::EvaluateSync`

`pAddress`\
[in]に渡[されるオブジェクト。](../../../extensibility/debugger/reference/idebugaddress.md) `IDebugParsedExression::EvaluateSync`

`dataProvider`\
[in][インターフェイス](../../../extensibility/debugger/reference/ieevisualizerdataprovider.md)を実装するオブジェクト (式エバリュエーターによって提供されます)。

`ppService`\
[アウト]作成されたサービス。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 `binder`、 `pSymProv`、および`pAddress`パラメーターはすべてメソッドに`IDebugParsedExpression::EvaluateSync`渡されました。 `CreateVisualizerService`は、式エバリュ`IDebugParsedExpression::EvaluateSync`エーターが型ビジュアライザーをサポートする一部としてのみ呼び出されます。

## <a name="see-also"></a>関連項目
- [IEEVisualizerServiceProvider](../../../extensibility/debugger/reference/ieevisualizerserviceprovider.md)
- [EvaluateSync](../../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)
- [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)
- [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)
- [IEEVisualizerDataProvider](../../../extensibility/debugger/reference/ieevisualizerdataprovider.md)
