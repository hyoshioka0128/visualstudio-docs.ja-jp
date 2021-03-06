---
description: このインターフェイスは、型ビジュアライザーを使用してオブジェクトの値を変更する機能を提供します。
title: IEEVisualizerDataProvider |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEEVisualizerDataProvider
helpviewer_keywords:
- IEEVisualizerDataProvider interface
ms.assetid: 5fdfe6e3-b94e-4edb-acc5-41d8773d8ca5
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9c2bea2a99b259ac255a4244501ee246fd83e8b5
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102222888"
---
# <a name="ieevisualizerdataprovider"></a>IEEVisualizerDataProvider
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターを実装するこの方法は非推奨とされます。 CLR 式エバリュエーターの実装の詳細については、「 [Clr 式](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) エバリュエーターと [マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

 このインターフェイスは、型ビジュアライザーを使用してオブジェクトの値を変更する機能を提供します。

## <a name="syntax"></a>構文

```
IEEVisualizerDataProvider : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 式エバリュエーターは、このインターフェイスを実装して、型ビジュアライザーを使用してプロパティオブジェクトのデータを変更できるようにします。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 このインターフェイスは、 [Createvisualizerservice](../../../extensibility/debugger/reference/ieevisualizerserviceprovider-createvisualizerservice.md)の呼び出しを通じて[ieevisualizerservice](../../../extensibility/debugger/reference/ieevisualizerservice.md)オブジェクトを作成するときに使用されます。 詳細については [、「データの視覚化と表示](../../../extensibility/debugger/visualizing-and-viewing-data.md) 」を参照してください。

## <a name="methods-in-vtable-order"></a>Vtable の順序でのメソッド

|メソッド|説明|
|------------|-----------------|
|[CanSetObjectForVisualizer](../../../extensibility/debugger/reference/ieevisualizerdataprovider-cansetobjectforvisualizer.md)|このビジュアライザーが表すオブジェクト (およびその後の値) を更新できるかどうかを判断します。|
|[GetNewObjectForVisualizer](../../../extensibility/debugger/reference/ieevisualizerdataprovider-getnewobjectforvisualizer.md)|このビジュアライザーのオブジェクトを強制的に再評価します。|
|[GetObjectForVisualizer](../../../extensibility/debugger/reference/ieevisualizerdataprovider-getobjectforvisualizer.md)|このビジュアライザーの既存のオブジェクトを取得します (評価は行われません)。|
|[SetObjectForVisualizer](../../../extensibility/debugger/reference/ieevisualizerdataprovider-setobjectforvisualizer.md)|ビジュアライザーによって表示される値を変更して、このビジュアライザーのオブジェクトを更新します。|

## <a name="remarks"></a>解説
 ビジュアライザーサービス ( [Ieevisualizerservice](../../../extensibility/debugger/reference/ieevisualizerservice.md) インターフェイスによって表され、 [Createvisualizerservice](../../../extensibility/debugger/reference/ieevisualizerserviceprovider-createvisualizerservice.md)によって返される) は、インターフェイスを実装するオブジェクトへの参照を保持し `IEEVisualizerDataProvider` ます。 その結果、 `IEEVisualizerDataProvider` そのオブジェクトがオブジェクトへの参照を保持している場合、 [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) を実装するオブジェクトにインターフェイスを実装することはできません `IEEVisualizerService` 。循環参照の結果と、オブジェクトが破棄されるとデッドロックが発生します。 を `IEEVisualizerDataProvider` 呼び出さずにオブジェクトがデリゲートする別のオブジェクトにを実装する方法をお勧めし `IDebugProperty2` `IUnknown::AddRef` ます。

## <a name="requirements"></a>必要条件
 ヘッダー: ee

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [式の評価のインターフェイス](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [IEEVisualizerService](../../../extensibility/debugger/reference/ieevisualizerservice.md)
- [IEEVisualizerServiceProvider](../../../extensibility/debugger/reference/ieevisualizerserviceprovider.md)
- [データの視覚化と表示](../../../extensibility/debugger/visualizing-and-viewing-data.md)
