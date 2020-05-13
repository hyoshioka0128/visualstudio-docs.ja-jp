---
title: 型ビジュアライザーとカスタム ビューアーの実装 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], custom viewer
- debugging [Debugging SDK], type visualizer
ms.assetid: abef18c0-8272-4451-b82a-b4624edaba7d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c2ebbb5c8e27df4ae4baf2d9a9f1c3314188e2b3
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738499"
---
# <a name="implement-type-visualizers-and-custom-viewers"></a>型ビジュアライザーとカスタム ビューアーを実装する
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターのこの実装方法は非推奨になりました。 CLR 式エバリュエーターの実装については[、「CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) 」および「[マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

 型ビジュアライザーとカスタム ビューアーを使用すると、数値の単純な 16 進数ダンプよりも意味のある方法で特定の型のデータを表示できます。 式エバリュエーター (EE) は、カスタム ビューアーを特定の種類のデータまたは変数に関連付けることができます。 これらのカスタム ビューアーは EE によって実装されます。 EE は、外部型ビジュアライザーもサポートできます。

## <a name="discussion"></a>ディスカッション

### <a name="type-visualizers"></a>型ビジュアライザー
 Visual Studio では、ウォッチ ウィンドウに表示されるすべてのオブジェクトについて、ビジュアライザーの種類とカスタム ビューアーの一覧を要求します。 式エバリュエーター (EE) は、型ビジュアライザーとカスタム ビューアーをサポートする必要があるすべての型に対して、このようなリストを提供します。 [GetCustomViewerCount](../../extensibility/debugger/reference/idebugproperty3-getcustomviewercount.md)と[GetCustomViewerList](../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md)への呼び出しは、型ビジュアライザーとカスタム ビューアーにアクセスするプロセス全体を開始します (呼び出し元シーケンスの詳細については、「[データの視覚化と表示](../../extensibility/debugger/visualizing-and-viewing-data.md)」を参照)。

### <a name="custom-viewers"></a>カスタム ビューアー
 カスタム ビューアーは、特定のデータ型の EE に実装され[、IDebugCustomViewer](../../extensibility/debugger/reference/idebugcustomviewer.md)インターフェイスによって表されます。 カスタム ビューアーは、その特定のカスタム ビューアーを実装する EE が実行されている場合にのみ使用できるため、型ビジュアライザーほど柔軟ではありません。 カスタム ビューアーの実装は、型ビジュアライザーのサポートを実装するよりも簡単です。 ただし、サポート型ビジュアライザーは、エンド ユーザーがデータを視覚化する最大の柔軟性を提供します。 この議論の残りの部分は、型のビジュアライザーのみに関するものです。

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
