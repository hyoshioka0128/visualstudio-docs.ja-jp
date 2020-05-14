---
title: ストレージ |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEEDataStorage
helpviewer_keywords:
- IEEDataStorage interface
ms.assetid: 704e932d-2325-410e-89c4-ce88c6ec19da
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ad7da71d31e1093d87d68bb39958a71a117f5d5f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80718180"
---
# <a name="ieedatastorage"></a>IEEDataStorage
このインターフェイスはバイト配列を表します。

## <a name="syntax"></a>構文

```
IEEDataStorage : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 式エバリュエーター (EE) は、このインターフェイスを実装してバイト配列を表します (型ビジュアライザーが[IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)インターフェイスを通じてデータを取得および変更するために使用します)。 EE は通常、外部型ビジュアライザーをサポートするためにこのインターフェイスを実装します。

## <a name="notes-for-callers"></a>発信者向けのメモ
 インターフェイスのメソッドはすべて`IPropertyProxyEESide`、このインターフェイスを返します。 インターフェイス[を取得](../../../extensibility/debugger/reference/ipropertyproxyprovider-getpropertyproxy.md)するには、プロパティ[プロキシを](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)呼び出します。 インターフェイスを取得するには、[インターフェイス](../../../extensibility/debugger/reference/idebugproperty3.md)[を呼び](/cpp/atl/queryinterface)出[します](../../../extensibility/debugger/reference/ipropertyproxyprovider.md)。

## <a name="methods-in-vtable-order"></a>V テーブル順のメソッド
 この`IEEDataStorage`インターフェイスは、次のメソッドを実装します。

|Method|説明|
|------------|-----------------|
|[GetData](../../../extensibility/debugger/reference/ieedatastorage-getdata.md)|指定されたバッファーに指定されたデータ バイト数を取得します。|
|[GetSize](../../../extensibility/debugger/reference/ieedatastorage-getsize.md)|使用可能なデータバイト数を取得します。|

## <a name="remarks"></a>Remarks
 このインターフェイスは、型ビジュアライザーが特定のオブジェクトが保持するデータにアクセスするために使用されます。 データはバイト配列として扱われ、型ビジュアライザーは、ユーザーに提示するために必要な方法でデータを操作できます。

 カスタム ビューアーは、必要に応じてこのインターフェイスを使用することもできますが、通常はカスタム ビューアーは、カスタム インターフェイス[GetMemoryBytes](../../../extensibility/debugger/reference/idebugproperty2-getmemorybytes.md)または[GetStringChars](../../../extensibility/debugger/reference/idebugproperty3-getstringchars.md) (文字列指向のデータ) を使用します。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)
- [型のビジュアライザーとカスタム ビューアー](../../../extensibility/debugger/type-visualizer-and-custom-viewer.md)
