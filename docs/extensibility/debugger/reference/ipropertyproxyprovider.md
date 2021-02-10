---
title: IPropertyProxyProvider |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IPropertyProxyProvider
helpviewer_keywords:
- IPropertyProxyProvider interface
ms.assetid: 52e9f7fc-6fe0-4d23-890b-5673dca8c3cb
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f6082b06e6235a93b0e198d973b40efb728bd815
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99962133"
---
# <a name="ipropertyproxyprovider"></a>IPropertyProxyProvider
このインターフェイスは、オブジェクトのデータを表示および変更するためのプロキシインターフェイスを提供します。

## <a name="syntax"></a>構文

```
IPropertyProxyProvider : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 式エバリュエーター (EE) は、EE の型ビジュアライザーのサポートの一部として、 [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md) インターフェイスを実装する同じオブジェクトにこのインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 インターフェイスの [QueryInterface](/cpp/atl/queryinterface) を呼び出して、 `IDebugProperty3` このインターフェイスを取得します。

## <a name="methods-in-vtable-order"></a>Vtable の順序でのメソッド
 インターフェイスには `IPropertyProxyProvider` 、次のメソッドが実装されています。

|Method|説明|
|------------|-----------------|
|[GetPropertyProxy](../../../extensibility/debugger/reference/ipropertyproxyprovider-getpropertyproxy.md)|オブジェクトのデータを表示するプロパティプロキシインターフェイスを取得します。|

## <a name="remarks"></a>解説
 EE はこのインターフェイスを実装しますが、 [getpropertyproxy](../../../extensibility/debugger/reference/ipropertyproxyprovider-getpropertyproxy.md) の実装は通常、 [getpropertyproxy](../../../extensibility/debugger/reference/ieevisualizerservice-getpropertyproxy.md)によって処理されます。 IEEVisualizerService インターフェイスの取得の詳細については、「 [データの視覚化と表示](../../../extensibility/debugger/visualizing-and-viewing-data.md) 」を参照してください。

## <a name="requirements"></a>要件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [GetPropertyProxy](../../../extensibility/debugger/reference/ieevisualizerservice-getpropertyproxy.md)
- [型のビジュアライザーとカスタム ビューアー](../../../extensibility/debugger/type-visualizer-and-custom-viewer.md)
- [データの視覚化と表示](../../../extensibility/debugger/visualizing-and-viewing-data.md)
