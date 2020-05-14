---
title: 型ビジュアライザーとカスタム ビューアー |マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80712466"
---
# <a name="type-visualizer-and-custom-viewer"></a>型ビジュアライザーとカスタム ビューアー
型ビジュアライザーは、特定の形式でデータを表示するコンポーネントです。 形式は、エンド ユーザーまたはビジュアライザーのサード パーティサプライヤーであるビジュアライザーを実装するユーザーに完全にかかかります。

 カスタム ビューアーは、特定の形式でデータを表示するカスタム式エバリュエーターの一部です。 この形式は、カスタム ビューアーの実装者に完全に適用されます。

## <a name="support-for-type-visualizers-in-an-expression-evaluator"></a>式エバリュエーターでの型ビジュアライザーのサポート
 EE は、ビジュアライザーにアクセスできる一連のインターフェイスをサポートすることにより、型[ビジュアライザー](../../extensibility/debugger/reference/ieevisualizerservice.md)をサポート[します。](../../extensibility/debugger/reference/ieevisualizerdataprovider.md) ただし、EE は型ビジュアライザー自体を実装する責任はありません。 このようなビジュアライザーは、EE と共に出荷され、別のサード パーティ ベンダーによって、またはエンド ユーザーによって提供される Visual Studio の適切な場所にインストールされる場合があります。

## <a name="support-for-custom-viewers-in-an-expression-evaluator"></a>式エバリュエーターでのカスタム ビューアーのサポート
 EE は、データ型を表示するためのコードを EE 自身が提供するカスタム ビューアーもサポートできます。 カスタム ビューアーは、必要な形式でデータを表示するすべての職務を処理する[IDebugCustomViewer](../../extensibility/debugger/reference/idebugcustomviewer.md)インターフェイスを実装します。ビューアーは、表示を完全に制御し、データを変更することもできます。 EE から提供されるカスタム ビューアは、製品の出荷時に EE に付属します。

## <a name="see-also"></a>関連項目
- [デバッガー コンポーネント](../../extensibility/debugger/debugger-components.md)
- [式エバリュエーター](../../extensibility/debugger/expression-evaluator.md)
- [デバッグ エンジン](../../extensibility/debugger/debug-engine.md)
- [IDebugCustomViewer](../../extensibility/debugger/reference/idebugcustomviewer.md)
- [IEEVisualizerService](../../extensibility/debugger/reference/ieevisualizerservice.md)
- [IEEVisualizerDataProvider](../../extensibility/debugger/reference/ieevisualizerdataprovider.md)
