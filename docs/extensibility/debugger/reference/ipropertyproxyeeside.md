---
title: Iプロパティプロキシーサイド |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IPropertyProxyEESide
helpviewer_keywords:
- IPropertyProxyEESide interface
ms.assetid: cf227cf8-39d9-4758-8f7e-a697aebb1926
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c89cecbf22091a45e31c307c5b523ac8aa4c924e
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80714856"
---
# <a name="ipropertyproxyeeside"></a>IPropertyProxyEESide
このインターフェイスには、関連付けられたオブジェクトのデータを表示するメソッドが用意されています。 このインターフェイスは、型ビジュアライザーのサポートの一部です。

## <a name="syntax"></a>構文

```
IPropertyProxyEESide : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 式エバリュエーターは、型のビジュアライザーをサポートするためにこのインターフェイスを実装します。

## <a name="notes-for-callers"></a>発信者向けのメモ
 このインターフェイスを取得するには[、GetPropertyProxy](../../../extensibility/debugger/reference/ipropertyproxyprovider-getpropertyproxy.md)を呼び出します。 インターフェイスを取得するには、[インターフェイス](../../../extensibility/debugger/reference/idebugproperty3.md)[を呼び](/cpp/atl/queryinterface)出[します](../../../extensibility/debugger/reference/ipropertyproxyprovider.md)。

## <a name="methods-in-vtable-order"></a>V テーブル順のメソッド
 このインターフェイスでは、次のメソッドが実装されています。

|Method|説明|
|------------|-----------------|
|[InitSourceDataProvider](../../../extensibility/debugger/reference/ipropertyproxyeeside-initsourcedataprovider.md)|オブジェクトのデータにアクセスできるように、データ ソース プロバイダーを初期化します。|
|[GetManagedViewerCreationData](../../../extensibility/debugger/reference/ipropertyproxyeeside-getmanagedviewercreationdata.md)|オブジェクトのアセンブリに関する情報を取得します。|
|[GetInitialData](../../../extensibility/debugger/reference/ipropertyproxyeeside-getinitialdata.md)|オブジェクトの初期データを取得します。|
|[CreateReplacementObject](../../../extensibility/debugger/reference/ipropertyproxyeeside-createreplacementobject.md)|既存のデータ ストレージのコピーを作成します。|
|[InPlaceUpdateObject](../../../extensibility/debugger/reference/ipropertyproxyeeside-inplaceupdateobject.md)|既存のデータ ストレージへの参照を作成します。|
|[ResolveAssemblyRef](../../../extensibility/debugger/reference/ipropertyproxyeeside-resolveassemblyref.md)|このオブジェクトを含むアセンブリのコンテキスト内の特定のアセンブリに関する情報を取得します。|

## <a name="remarks"></a>Remarks
 型ビジュアライザーは、このインターフェイスを使用して、このインターフェイスが属するオブジェクトに関連付けられた値にアクセスします。 データは、データの読み取り専用ビューを提供する[IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)インターフェイスを介してアクセスされます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [型のビジュアライザーとカスタム ビューアー](../../../extensibility/debugger/type-visualizer-and-custom-viewer.md)
- [IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
