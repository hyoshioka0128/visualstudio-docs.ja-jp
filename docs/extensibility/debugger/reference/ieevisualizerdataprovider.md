---
title: データプロバイダ |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEEVisualizerDataProvider
helpviewer_keywords:
- IEEVisualizerDataProvider interface
ms.assetid: 5fdfe6e3-b94e-4edb-acc5-41d8773d8ca5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a10f306b6c507f6db7add17931b8a38d926a37d9
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80718053"
---
# <a name="ieevisualizerdataprovider"></a>IEEVisualizerDataProvider
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターのこの実装方法は非推奨になりました。 CLR 式エバリュエーターの実装については、「 [CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)と[マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

 このインターフェイスは、型のビジュアライザーを使用してオブジェクトの値を変更する機能を提供します。

## <a name="syntax"></a>構文

```
IEEVisualizerDataProvider : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 式エバリュエーターは、型ビジュアライザーを使用してプロパティ オブジェクトのデータを変更するサポートをこのインターフェイスを実装します。

## <a name="notes-for-callers"></a>発信者向けのメモ
 このインターフェイスは、CreateVisualizerService の呼び出しを通じて[IEEVisualizerService](../../../extensibility/debugger/reference/ieevisualizerservice.md)オブジェクトを[作成](../../../extensibility/debugger/reference/ieevisualizerserviceprovider-createvisualizerservice.md)するときに使用されます。 詳細については[、データの視覚化と表示](../../../extensibility/debugger/visualizing-and-viewing-data.md)を参照してください。

## <a name="methods-in-vtable-order"></a>V テーブル順のメソッド

|Method|説明|
|------------|-----------------|
|[CanSetObjectForVisualizer](../../../extensibility/debugger/reference/ieevisualizerdataprovider-cansetobjectforvisualizer.md)|ビジュアライザーが表しているオブジェクト (およびその後の値) を更新できるかどうかを判断します。|
|[GetNewObjectForVisualizer](../../../extensibility/debugger/reference/ieevisualizerdataprovider-getnewobjectforvisualizer.md)|このビジュアライザーのオブジェクトの再評価を強制します。|
|[GetObjectForVisualizer](../../../extensibility/debugger/reference/ieevisualizerdataprovider-getobjectforvisualizer.md)|このビジュアライザーの既存のオブジェクトを取得します (評価は行われません)。|
|[SetObjectForVisualizer](../../../extensibility/debugger/reference/ieevisualizerdataprovider-setobjectforvisualizer.md)|ビジュアライザーのオブジェクトを更新し、ビジュアライザーが提示する値を変更します。|

## <a name="remarks"></a>Remarks
 ビジュアライザー サービス[(IEEVisualizerService](../../../extensibility/debugger/reference/ieevisualizerservice.md)インターフェイスによって表され[、CreateVisualizerService](../../../extensibility/debugger/reference/ieevisualizerserviceprovider-createvisualizerservice.md)によって返される) は、`IEEVisualizerDataProvider`インターフェイスを実装するオブジェクトへの参照を保持します。 その結果、`IEEVisualizerDataProvider`オブジェクトが`IEEVisualizerService`オブジェクトへの参照を保持している場合[、IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)を実装するオブジェクトと同じオブジェクトにインターフェイスを実装しないでください。 推奨される方法は、オブジェクト`IEEVisualizerDataProvider`を呼び出`IUnknown::AddRef`さずに委任`IDebugProperty2`する別のオブジェクトに実装することです。

## <a name="requirements"></a>必要条件
 ヘッダー: ee.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [式の評価のインターフェイス](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [IEEVisualizerService](../../../extensibility/debugger/reference/ieevisualizerservice.md)
- [IEEVisualizerServiceProvider](../../../extensibility/debugger/reference/ieevisualizerserviceprovider.md)
- [データの視覚化と表示](../../../extensibility/debugger/visualizing-and-viewing-data.md)
