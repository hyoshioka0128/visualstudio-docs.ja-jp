---
title: IPropertyProxyEESide |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IPropertyProxyEESide
helpviewer_keywords:
- IPropertyProxyEESide interface
ms.assetid: cf227cf8-39d9-4758-8f7e-a697aebb1926
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f0331365716c8399c1b2a565fc8046482df5d80f
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99938903"
---
# <a name="ipropertyproxyeeside"></a>IPropertyProxyEESide
このインターフェイスには、関連付けられたオブジェクトのデータを表示するメソッドが用意されています。 このインターフェイスは、型ビジュアライザーのサポートの一部です。

## <a name="syntax"></a>構文

```
IPropertyProxyEESide : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 式エバリュエーターは、型ビジュアライザーをサポートするためにこのインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 このインターフェイスを取得するには、 [Getpropertyproxy](../../../extensibility/debugger/reference/ipropertyproxyprovider-getpropertyproxy.md) を呼び出します。 [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)インターフェイスで[QueryInterface](/cpp/atl/queryinterface)を呼び出して、 [IPropertyProxyProvider](../../../extensibility/debugger/reference/ipropertyproxyprovider.md)インターフェイスを取得します。

## <a name="methods-in-vtable-order"></a>Vtable の順序でのメソッド
 このインターフェイスには、次のメソッドが実装されています。

|Method|説明|
|------------|-----------------|
|[InitSourceDataProvider](../../../extensibility/debugger/reference/ipropertyproxyeeside-initsourcedataprovider.md)|オブジェクトのデータにアクセスできるように、データソースプロバイダーを初期化します。|
|[GetManagedViewerCreationData](../../../extensibility/debugger/reference/ipropertyproxyeeside-getmanagedviewercreationdata.md)|オブジェクトのアセンブリに関する情報を取得します。|
|[GetInitialData](../../../extensibility/debugger/reference/ipropertyproxyeeside-getinitialdata.md)|オブジェクトの初期データを取得します。|
|[CreateReplacementObject](../../../extensibility/debugger/reference/ipropertyproxyeeside-createreplacementobject.md)|既存のデータストレージのコピーを作成します。|
|[InPlaceUpdateObject](../../../extensibility/debugger/reference/ipropertyproxyeeside-inplaceupdateobject.md)|既存のデータストレージへの参照を作成します。|
|[ResolveAssemblyRef](../../../extensibility/debugger/reference/ipropertyproxyeeside-resolveassemblyref.md)|このオブジェクトを含むアセンブリのコンテキストで、特定のアセンブリに関する情報を取得します。|

## <a name="remarks"></a>解説
 型ビジュアライザーは、このインターフェイスを使用して、このインターフェイスが含まれているオブジェクトに関連付けられている値にアクセスします。 データは、 [Ieedatastorage](../../../extensibility/debugger/reference/ieedatastorage.md) インターフェイスを介してアクセスされます。このインターフェイスは、データの読み取り専用ビューを提供します。

## <a name="requirements"></a>要件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [型のビジュアライザーとカスタム ビューアー](../../../extensibility/debugger/type-visualizer-and-custom-viewer.md)
- [IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
