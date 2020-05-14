---
title: IEEビジュアライザーサービスプロバイダ |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEEVisualizerServiceProvider
helpviewer_keywords:
- IEEVisualizerServiceProvider interface
ms.assetid: 859d1a51-1c65-4c8b-ae74-3b74b181ebcd
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 44d8a73589a4248736ac6c4d73814166056a1f90
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80717883"
---
# <a name="ieevisualizerserviceprovider"></a>IEEVisualizerServiceProvider
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターのこの実装方法は非推奨になりました。 CLR 式エバリュエーターの実装については、「 [CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)と[マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

 このインターフェイスは、IDE のビジュアライザーの種類のタスクを処理するために使用されるビジュアライザー サービスを作成できるメソッドへのアクセスを提供します。

## <a name="syntax"></a>構文

```
IEEVisualizerServiceProvider : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 Visual Studio では、ビジュアライザーサービス オブジェクトを作成するためにこのインターフェイスを実装します`CLSID`。

## <a name="notes-for-callers"></a>発信者向けのメモ
 式エバリュエーター (EE) は、このインターフェイスを取得するために[GetEEService](../../../extensibility/debugger/reference/idebugbinder3-geteeservice.md)を呼び出します。

## <a name="methods-in-vtable-order"></a>V テーブル順のメソッド

|Method|説明|
|------------|-----------------|
|[CreateVisualizerService](../../../extensibility/debugger/reference/ieevisualizerserviceprovider-createvisualizerservice.md)|ビジュアライザー サービスを作成します。|

## <a name="remarks"></a>Remarks
 インターフェイス`IEEVisualizerServiceProvider`は[、EvaluateSync](../../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)の実装中に取得されます。 このインターフェイスが作成するビジュアライザー サービスは、EE が実装を担当する[IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)インターフェイスに機能を提供するために使用されます。 EE は、型ビジュアライザーがプロパティの値を表示および変更できるようにする[IEEVisualizerDataProvider](../../../extensibility/debugger/reference/ieevisualizerdataprovider.md)インターフェイスの実装も担当します。

 これらのインターフェイスの相互作用の詳細については、「[データの視覚化と表示](../../../extensibility/debugger/visualizing-and-viewing-data.md)」を参照してください。

## <a name="requirements"></a>必要条件
 ヘッダー: ee.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [式の評価のインターフェイス](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [EvaluateSync](../../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)
- [IEEVisualizerDataProvider](../../../extensibility/debugger/reference/ieevisualizerdataprovider.md)
- [GetEEService](../../../extensibility/debugger/reference/idebugbinder3-geteeservice.md)
- [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)
- [データの視覚化と表示](../../../extensibility/debugger/visualizing-and-viewing-data.md)
