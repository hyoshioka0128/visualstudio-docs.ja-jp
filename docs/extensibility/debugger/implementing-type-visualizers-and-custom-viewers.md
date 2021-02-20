---
title: 型ビジュアライザーとカスタムビューアーの実装 |Microsoft Docs
description: 型ビジュアライザーとカスタムビューアーを実装する方法について説明します。これにより、ユーザーは数値のダンプよりも意味のある方法でデータを表示できます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], custom viewer
- debugging [Debugging SDK], type visualizer
ms.assetid: abef18c0-8272-4451-b82a-b4624edaba7d
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8cf456dca27a45a2674f7138a6c0b21b12750c81
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99945969"
---
# <a name="implement-type-visualizers-and-custom-viewers"></a>型ビジュアライザーとカスタムビューアーを実装する
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターを実装するこの方法は非推奨とされます。 CLR 式エバリュエーターの実装の詳細については、「 [clr 式](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) エバリュエーターと [マネージ式エバリュエーターサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

 型ビジュアライザーおよびカスタムビューアーを使用すると、特定の型のデータを、数値の単純な16進数ダンプよりもわかりやすい方法で表示できます。 式エバリュエーター (EE) では、カスタムビューアーを特定の種類のデータまたは変数に関連付けることができます。 これらのカスタムビューアーは、EE によって実装されます。 EE は外部型ビジュアライザーもサポートしていますが、これは別のサードパーティベンダーまたはエンドユーザーからのものである可能性があります。

## <a name="discussion"></a>ディスカッション

### <a name="type-visualizers"></a>型ビジュアライザー
 Visual Studio では、ウォッチウィンドウに表示されるすべてのオブジェクトについて、型ビジュアライザーとカスタムビューアーの一覧が要求されます。 式エバリュエーター (EE) は、型ビジュアライザーおよびカスタムビューアーをサポートするために必要なすべての型のリストを提供します。 [GetCustomViewerCount](../../extensibility/debugger/reference/idebugproperty3-getcustomviewercount.md)と[GetCustomViewerList](../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md)を呼び出すと、型ビジュアライザーとカスタムビューアーにアクセスするプロセス全体が開始されます (「呼び出し元のシーケンスの詳細については、「[データの視覚化と表示](../../extensibility/debugger/visualizing-and-viewing-data.md)」を参照してください)。

### <a name="custom-viewers"></a>カスタムビューアー
 カスタムビューアーは、特定のデータ型に対して EE で実装され、 [IDebugCustomViewer](../../extensibility/debugger/reference/idebugcustomviewer.md) インターフェイスによって表されます。 カスタムビューアーは、その特定のカスタムビューアーを実装する EE が実行されている場合にのみ使用できるため、型ビジュアライザーほど柔軟ではありません。 カスタムビューアーの実装は、型ビジュアライザーのサポートを実装するよりも簡単です。 ただし、型ビジュアライザーをサポートすると、エンドユーザーがデータを視覚化するための柔軟性が最大限に高まります。 この説明の残りの部分では、型ビジュアライザーのみを考慮します。

## <a name="interfaces"></a>インターフェイス
 EE は、Visual Studio で使用される型ビジュアライザーをサポートするために、次のインターフェイスを実装します。

- [IEEVisualizerDataProvider](../../extensibility/debugger/reference/ieevisualizerdataprovider.md)

- [IPropertyProxyEESide](../../extensibility/debugger/reference/ipropertyproxyeeside.md)

- [IPropertyProxyProvider](../../extensibility/debugger/reference/ipropertyproxyprovider.md)

- [IEEDataStorage](../../extensibility/debugger/reference/ieedatastorage.md)

- [IDebugProperty3](../../extensibility/debugger/reference/idebugproperty3.md)

- [IDebugObject](../../extensibility/debugger/reference/idebugobject.md)

  EE は、型ビジュアライザーをサポートするために次のインターフェイスを使用します。

- [IEEVisualizerService](../../extensibility/debugger/reference/ieevisualizerservice.md)

- [IEEVisualizerServiceProvider](../../extensibility/debugger/reference/ieevisualizerserviceprovider.md)

- [IDebugBinder3](../../extensibility/debugger/reference/idebugbinder3.md)

## <a name="see-also"></a>関連項目
- [CLR 式エバリュエーターの記述](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
- [データの視覚化と表示](../../extensibility/debugger/visualizing-and-viewing-data.md)
- [IDebugCustomViewer](../../extensibility/debugger/reference/idebugcustomviewer.md)
