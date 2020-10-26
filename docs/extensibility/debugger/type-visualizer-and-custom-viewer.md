---
title: 型ビジュアライザーとカスタムビューアー |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], custom viewer
- debugging [Debugging SDK], type visualizer
ms.assetid: fd3691e6-9c78-4767-846f-43f85ada4375
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7b8def9d28279f601ff488fca457982806629c0b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80712466"
---
# <a name="type-visualizer-and-custom-viewer"></a>型ビジュアライザーとカスタムビューアー
型ビジュアライザーは、特定の形式でデータを表示するコンポーネントです。 この形式は、ビジュアライザーを実装しているユーザーに対してのみ、エンドユーザーまたはビジュアライザーのサードパーティのサプライヤーです。

 カスタムビューアーは、特定の形式でデータを表示するカスタム式エバリュエーターの一部です。 この形式は、カスタムビューアーの実装者に完全に適用されます。つまり、形式が式エバリュエーター (EE) の実装者になります。

## <a name="support-for-type-visualizers-in-an-expression-evaluator"></a>式エバリュエーターでの型ビジュアライザーのサポート
 EE は、ビジュアライザー: [Ieevisualizerservice](../../extensibility/debugger/reference/ieevisualizerservice.md) や [Ieevisualizerservice](../../extensibility/debugger/reference/ieevisualizerdataprovider.md)などのインターフェイスにアクセスできるインターフェイスのセットをサポートすることで、型ビジュアライザーをサポートしています。 ただし、EE は型ビジュアライザー自体を実装する責任を負いません。 EE は、外部ビジュアライザーが型情報にアクセスするだけを許可します。 このようなビジュアライザーは、EE と共に出荷され、別のサードパーティベンダーまたはエンドユーザーが提供する Visual Studio の適切な場所にインストールされる場合があります。

## <a name="support-for-custom-viewers-in-an-expression-evaluator"></a>式エバリュエーターでのカスタムビューアーのサポート
 EE は、データ型を表示するためのコードを提供するカスタムビューアーをサポートすることもできます。 カスタムビューアーは、必要な形式でデータを表示するすべての作業を処理する [IDebugCustomViewer](../../extensibility/debugger/reference/idebugcustomviewer.md) インターフェイスを実装します。ビューアーには、表示を完全に制御できます。また、データを変更することもできます。 EE によって提供されるカスタムビューアーには、製品の出荷時に EE が付属しています。

## <a name="see-also"></a>関連項目
- [デバッガーコンポーネント](../../extensibility/debugger/debugger-components.md)
- [式エバリュエーター](../../extensibility/debugger/expression-evaluator.md)
- [デバッグエンジン](../../extensibility/debugger/debug-engine.md)
- [IDebugCustomViewer](../../extensibility/debugger/reference/idebugcustomviewer.md)
- [IEEVisualizerService](../../extensibility/debugger/reference/ieevisualizerservice.md)
- [IEEVisualizerDataProvider](../../extensibility/debugger/reference/ieevisualizerdataprovider.md)
