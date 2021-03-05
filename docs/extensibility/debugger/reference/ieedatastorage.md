---
description: このインターフェイスは、バイトの配列を表します。
title: IEEDataStorage |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEEDataStorage
helpviewer_keywords:
- IEEDataStorage interface
ms.assetid: 704e932d-2325-410e-89c4-ce88c6ec19da
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 9434138114f2b4b0615e20c1b556ff6387c715de
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102227334"
---
# <a name="ieedatastorage"></a>IEEDataStorage
このインターフェイスは、バイトの配列を表します。

## <a name="syntax"></a>構文

```
IEEDataStorage : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 式エバリュエーター (EE) は、バイトの配列を表すために、このインターフェイスを実装します ( [IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md) インターフェイスを使用してデータを取得および変更するために型ビジュアライザーによって使用されます)。 EE は、通常、外部型ビジュアライザーをサポートするために、このインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 インターフェイスのメソッドは `IPropertyProxyEESide` すべて、このインターフェイスを返します。 [Getpropertyproxy](../../../extensibility/debugger/reference/ipropertyproxyprovider-getpropertyproxy.md)を呼び出して、 [IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)インターフェイスを取得します。 [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)インターフェイスで[QueryInterface](/cpp/atl/queryinterface)を呼び出して、 [IPropertyProxyProvider](../../../extensibility/debugger/reference/ipropertyproxyprovider.md)インターフェイスを取得します。

## <a name="methods-in-vtable-order"></a>Vtable の順序でのメソッド
 インターフェイスには `IEEDataStorage` 、次のメソッドが実装されています。

|メソッド|説明|
|------------|-----------------|
|[GetData](../../../extensibility/debugger/reference/ieedatastorage-getdata.md)|指定したバッファーに、指定したデータバイト数を取得します。|
|[GetSize](../../../extensibility/debugger/reference/ieedatastorage-getsize.md)|使用可能なデータバイト数を取得します。|

## <a name="remarks"></a>解説
 このインターフェイスは、特定のオブジェクトによって保持されているデータにアクセスするために、型ビジュアライザーによって使用されます。 データはバイト配列として扱われます。これにより、型ビジュアライザーは、このデータをユーザーに提示するために必要な任意の方法で操作できます。

 カスタムビューアーでは、必要に応じてこのインターフェイスを使用することもできますが、通常はカスタムビューアーでカスタムインターフェイス、 [Getmemorybytes](../../../extensibility/debugger/reference/idebugproperty2-getmemorybytes.md) 、または [getmemorybytes](../../../extensibility/debugger/reference/idebugproperty3-getstringchars.md) (文字列指向データ用) を使用します。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)
- [型のビジュアライザーとカスタム ビューアー](../../../extensibility/debugger/type-visualizer-and-custom-viewer.md)
