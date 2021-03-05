---
description: このインターフェイスは、ビジュアライザーサービスを作成できるメソッドへのアクセスを提供します。このメソッドは、IDE の型ビジュアライザータスクを処理するために使用されます。
title: IEEVisualizerServiceProvider |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEEVisualizerServiceProvider
helpviewer_keywords:
- IEEVisualizerServiceProvider interface
ms.assetid: 859d1a51-1c65-4c8b-ae74-3b74b181ebcd
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d4fc53ae13588a0e285e4a62691da4d88a94d5f5
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102227178"
---
# <a name="ieevisualizerserviceprovider"></a>IEEVisualizerServiceProvider
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターを実装するこの方法は非推奨とされます。 CLR 式エバリュエーターの実装の詳細については、「 [Clr 式](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) エバリュエーターと [マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

 このインターフェイスは、ビジュアライザーサービスを作成できるメソッドへのアクセスを提供します。このメソッドは、IDE の型ビジュアライザータスクを処理するために使用されます。

## <a name="syntax"></a>構文

```
IEEVisualizerServiceProvider : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 Visual Studio は、ビジュアライザーサービスオブジェクトを作成するためにこのインターフェイスを実装します。ビジュアライザーサービスオブジェクトは、 `CLSID` Visual STUDIO IDE に型ビジュアライザーのクラス id を提供するために使用されます。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 式エバリュエーター (EE) は、このインターフェイスを取得するために [GetEEService](../../../extensibility/debugger/reference/idebugbinder3-geteeservice.md) を呼び出します。

## <a name="methods-in-vtable-order"></a>Vtable の順序でのメソッド

|メソッド|説明|
|------------|-----------------|
|[CreateVisualizerService](../../../extensibility/debugger/reference/ieevisualizerserviceprovider-createvisualizerservice.md)|ビジュアライザーサービスを作成します|

## <a name="remarks"></a>解説
 `IEEVisualizerServiceProvider`インターフェイスは、 [EvaluateSync](../../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)の実装中に取得されます。 このインターフェイスによって作成されるビジュアライザーサービスは、 [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md) インターフェイスに機能を提供するために使用されます。このインターフェイスは、EE が実装する役割を担います。 EE は、型ビジュアライザーがプロパティの値を表示および変更できるようにする [Ieevisualizerdataprovider](../../../extensibility/debugger/reference/ieevisualizerdataprovider.md) インターフェイスを実装する役割も担います。

 これらのインターフェイスの相互作用の詳細については [、「データの視覚化と表示](../../../extensibility/debugger/visualizing-and-viewing-data.md) 」を参照してください。

## <a name="requirements"></a>必要条件
 ヘッダー: ee

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [式の評価のインターフェイス](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [EvaluateSync](../../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)
- [IEEVisualizerDataProvider](../../../extensibility/debugger/reference/ieevisualizerdataprovider.md)
- [GetEEService](../../../extensibility/debugger/reference/idebugbinder3-geteeservice.md)
- [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)
- [データの視覚化と表示](../../../extensibility/debugger/visualizing-and-viewing-data.md)
