---
title: IEEVisualizerService |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEEVisualizerService
helpviewer_keywords:
- IEEVisualizerService interface
ms.assetid: 3bdb124b-c582-47ba-b465-13c6a1cdb702
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 40d21dcc9b1da0e1e2250adcfad59b3ef46a2113
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80717932"
---
# <a name="ieevisualizerservice"></a>IEEVisualizerService
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターを実装するこの方法は非推奨とされます。 CLR 式エバリュエーターの実装の詳細については、「 [Clr 式](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) エバリュエーターと [マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

 このインターフェイスは、 [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md) インターフェイスと [IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md) インターフェイスに機能を提供するキーメソッドを実装します。

## <a name="syntax"></a>構文

```
IEEVisualizerService : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 Visual Studio は、式エバリュエーター (EE) が型ビジュアライザーをサポートできるように、このインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 EE は、型ビジュアライザーのサポートの一部として、このインターフェイスを取得するために [Createvisualizerservice](../../../extensibility/debugger/reference/ieevisualizerserviceprovider-createvisualizerservice.md) を呼び出します。

## <a name="methods-in-vtable-order"></a>Vtable の順序でのメソッド

|メソッド|説明|
|------------|-----------------|
|[GetCustomViewerCount](../../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewercount.md)|このサービスが認識しているカスタムビューアーの数を取得します。|
|[GetCustomViewerList](../../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewerlist.md)|カスタムビューアーの一覧を取得します。|
|[GetPropertyProxy](../../../extensibility/debugger/reference/ieevisualizerservice-getpropertyproxy.md)|プロパティのプロキシオブジェクトを返します。|
|[GetValueDisplayStringCount](../../../extensibility/debugger/reference/ieevisualizerservice-getvaluedisplaystringcount.md)|指定したプロパティまたはフィールドに表示する値文字列の数を取得します。|

## <a name="remarks"></a>注釈
 IDE では、 [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md) インターフェイスを使用して、プロパティのカスタムビューアーまたは型ビジュアライザーがあるかどうかを判断します。 ビジュアライザーサービス ( [Createvisualizerservice](../../../extensibility/debugger/reference/ieevisualizerserviceprovider-createvisualizerservice.md)を使用) を作成することにより、EE は `IDebugProperty3` および [IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md) (プロパティの値の表示と変更をサポートします) に機能を提供し、型ビジュアライザーをサポートできます。

 EE が自身を実装するカスタムビューアーを持っている場合、EE は、 `CLSID` [GetCustomViewerList](../../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewerlist.md)によって返されたリストの末尾に、これらのカスタムビューアーのを追加できます。 これにより、EE は型ビジュアライザーと独自のカスタムビューアーの両方をサポートできます。 [GetCustomViewerCount](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewercount.md)にカスタムビューアーの追加が反映されていることを確認してください。

 ビジュアライザーとビューアーの違いについては、「 [型ビジュアライザーとカスタムビューアー](../../../extensibility/debugger/type-visualizer-and-custom-viewer.md) 」を参照してください。

## <a name="requirements"></a>必要条件
 ヘッダー: ee

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [式の評価のインターフェイス](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)
- [IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)
- [CreateVisualizerService](../../../extensibility/debugger/reference/ieevisualizerserviceprovider-createvisualizerservice.md)
- [型のビジュアライザーとカスタム ビューアー](../../../extensibility/debugger/type-visualizer-and-custom-viewer.md)
