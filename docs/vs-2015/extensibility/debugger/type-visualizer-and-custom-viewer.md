---
title: 型ビジュアライザーとカスタムビューアー |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], custom viewer
- debugging [Debugging SDK], type visualizer
ms.assetid: fd3691e6-9c78-4767-846f-43f85ada4375
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a85be2978abe35e91096b55fba5ec5281be25fbe
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68185316"
---
# <a name="type-visualizer-and-custom-viewer"></a>型のビジュアライザーとカスタム ビューアー
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

型ビジュアライザーは、非常に特殊な形式でデータを表示するコンポーネントです。 この形式は、ビジュアライザーの実装者に完全に対応しています。ビジュアライザーのエンドユーザーまたはサードパーティのサプライヤーです。  
  
 カスタムビューアーは、非常に特殊な形式でデータを表示するカスタム式エバリュエーターの一部です。 この形式は、カスタムビューアーの実装者に完全に適用されます。つまり、形式が式エバリュエーター (EE) の実装者になります。  
  
## <a name="support-for-type-visualizers-in-an-expression-evaluator"></a>式エバリュエーターでの型ビジュアライザーのサポート  
 EE は、ビジュアライザー: [Ieevisualizerservice](../../extensibility/debugger/reference/ieevisualizerservice.md) や [Ieevisualizerservice](../../extensibility/debugger/reference/ieevisualizerdataprovider.md)などのインターフェイスにアクセスできるインターフェイスのセットをサポートすることで、型ビジュアライザーをサポートできます。 ただし、EE は型ビジュアライザー自体を実装する責任がないことに注意してください。 EE では、外部ビジュアライザーが型情報にアクセスできるだけです。 このようなビジュアライザーは、EE と共に出荷され、別のサードパーティベンダーまたはエンドユーザーが提供する Visual Studio の適切な場所にインストールされる場合があります。  
  
## <a name="support-for-custom-viewers-in-an-expression-evaluator"></a>式エバリュエーターでのカスタムビューアーのサポート  
 EE は、データ型を表示するためのコードを提供するカスタムビューアーをサポートすることもできます。 カスタムビューアーは、必要な形式でデータを表示するすべての作業を処理する [IDebugCustomViewer](../../extensibility/debugger/reference/idebugcustomviewer.md) インターフェイスを実装します。ビューアーには、表示を完全に制御できます。また、データの変更を許可することもできます。 EE によって提供されるカスタムビューアーには、製品の出荷時に EE が付属しています。  
  
## <a name="see-also"></a>参照  
 [デバッガーコンポーネント](../../extensibility/debugger/debugger-components.md)   
 [式エバリュエーター](../../extensibility/debugger/expression-evaluator.md)   
 [デバッグエンジン](../../extensibility/debugger/debug-engine.md)   
 [IDebugCustomViewer](../../extensibility/debugger/reference/idebugcustomviewer.md)   
 [IEEVisualizerService](../../extensibility/debugger/reference/ieevisualizerservice.md)   
 [IEEVisualizerDataProvider](../../extensibility/debugger/reference/ieevisualizerdataprovider.md)
