---
title: IEE ビジュアライザーサービス |マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80717932"
---
# <a name="ieevisualizerservice"></a>IEEVisualizerService
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターのこの実装方法は非推奨になりました。 CLR 式エバリュエーターの実装については、「 [CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)と[マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

 このインターフェイスは、[インターフェイス](../../../extensibility/debugger/reference/idebugproperty3.md)に機能を提供するキー メソッド[を](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)実装します。

## <a name="syntax"></a>構文

```
IEEVisualizerService : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 Visual Studio では、式エバリュエーター (EE) が型のビジュアライザーをサポートできるように、このインターフェイスを実装します。

## <a name="notes-for-callers"></a>発信者向けのメモ
 EE は[、型のビジュアライザー](../../../extensibility/debugger/reference/ieevisualizerserviceprovider-createvisualizerservice.md)のサポートの一部としてこのインターフェイスを取得する CreateVisualizerService を呼び出します。

## <a name="methods-in-vtable-order"></a>V テーブル順のメソッド

|Method|説明|
|------------|-----------------|
|[GetCustomViewerCount](../../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewercount.md)|このサービスが認識しているカスタム ビューアーの数を取得します。|
|[GetCustomViewerList](../../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewerlist.md)|カスタム ビューアーの一覧を取得します。|
|[GetPropertyProxy](../../../extensibility/debugger/reference/ieevisualizerservice-getpropertyproxy.md)|プロパティのプロキシ オブジェクトを返します。|
|[GetValueDisplayStringCount](../../../extensibility/debugger/reference/ieevisualizerservice-getvaluedisplaystringcount.md)|指定したプロパティまたはフィールドに表示する値の文字列の数を取得します。|

## <a name="remarks"></a>Remarks
 IDE は[IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)インターフェイスを使用して、プロパティにカスタム ビューアーまたは型ビジュアライザーがあるかどうかを判断します。 ビジュアライザー サービスを作成することで[(VisualizerService](../../../extensibility/debugger/reference/ieevisualizerserviceprovider-createvisualizerservice.md)を使用して)、EE`IDebugProperty3`は、インターフェイスと[IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md) (プロパティの値の表示と変更をサポート) インターフェイスに機能を提供し、それによって型ビジュアライザーをサポートできます。

 EE に独自に実装されたカスタム ビューアーがある場合、EE は`CLSID`[、GetCustomViewerList](../../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewerlist.md)によって返されるリストの末尾に、それらのカスタム ビューアーの s を追加できます。 これにより、EE は型ビジュアライザーと独自のカスタム ビューアーの両方をサポートできます。 [カスタム](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewercount.md)ビューアーの追加が反映されていることを確認してください。

 [ビジュアライザーとビューアー](../../../extensibility/debugger/type-visualizer-and-custom-viewer.md)の違いについては、「タイプ ビジュアライザー」と「カスタム ビューアー」をご参照ください。

## <a name="requirements"></a>必要条件
 ヘッダー: ee.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [式の評価のインターフェイス](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)
- [IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)
- [CreateVisualizerService](../../../extensibility/debugger/reference/ieevisualizerserviceprovider-createvisualizerservice.md)
- [型のビジュアライザーとカスタム ビューアー](../../../extensibility/debugger/type-visualizer-and-custom-viewer.md)
