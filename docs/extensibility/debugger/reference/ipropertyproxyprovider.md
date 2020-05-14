---
title: を提供する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IPropertyProxyProvider
helpviewer_keywords:
- IPropertyProxyProvider interface
ms.assetid: 52e9f7fc-6fe0-4d23-890b-5673dca8c3cb
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f71d993c7f99cade5b866e67298132a325986e3a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80714796"
---
# <a name="ipropertyproxyprovider"></a>IPropertyProxyProvider
このインターフェイスは、オブジェクトのデータを表示および変更するためのプロキシ インターフェイスを提供します。

## <a name="syntax"></a>構文

```
IPropertyProxyProvider : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 式エバリュエーター (EE) は、型ビジュアライザーの EE のサポートの一部として[IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)インターフェイスを実装する同じオブジェクトにこのインターフェイスを実装します。

## <a name="notes-for-callers"></a>発信者向けのメモ
 この[QueryInterface](/cpp/atl/queryinterface)インターフェイスを取得するには`IDebugProperty3`、インターフェイスでクエリ インターフェイスを呼び出します。

## <a name="methods-in-vtable-order"></a>V テーブル順のメソッド
 インターフェイス`IPropertyProxyProvider`は、次のメソッドを実装します。

|Method|説明|
|------------|-----------------|
|[GetPropertyProxy](../../../extensibility/debugger/reference/ipropertyproxyprovider-getpropertyproxy.md)|オブジェクトのデータを表示するプロパティ プロキシ インターフェイスを取得します。|

## <a name="remarks"></a>Remarks
 EE はこのインターフェイスを実装しますが、通常は[GetPropertyProxy](../../../extensibility/debugger/reference/ipropertyproxyprovider-getpropertyproxy.md)[によって実装](../../../extensibility/debugger/reference/ieevisualizerservice-getpropertyproxy.md)されます。 IEEVisualizer サービス インターフェイスの取得の詳細については、「[データの視覚化と表示](../../../extensibility/debugger/visualizing-and-viewing-data.md)」を参照してください。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [GetPropertyProxy](../../../extensibility/debugger/reference/ieevisualizerservice-getpropertyproxy.md)
- [型のビジュアライザーとカスタム ビューアー](../../../extensibility/debugger/type-visualizer-and-custom-viewer.md)
- [データの視覚化と表示](../../../extensibility/debugger/visualizing-and-viewing-data.md)
