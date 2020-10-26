---
title: IDebugExpressionEvaluator2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugExpressionEvaluator2 interface
ms.assetid: cebe649f-1c77-4d33-854f-30d4f00eceb4
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7041456bf0f3ae7930a73399d43dbf7cac6b3b32
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80729143"
---
# <a name="idebugexpressionevaluator2"></a>IDebugExpressionEvaluator2
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターを実装するこの方法は非推奨とされます。 CLR 式エバリュエーターの実装の詳細については、「 [Clr 式](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) エバリュエーターと [マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

 式エバリュエーター (EE) の拡張バージョンを表します。

## <a name="syntax"></a>構文

```
IDebugExpressionEvaluator2 : IDebugExpressionEvaluator
```

## <a name="notes-for-implementers"></a>実装側の注意
 このインターフェイスは、式エバリュエーターによって実装されます。

## <a name="methods"></a>メソッド
 このインターフェイスは、 [IDebugExpressionEvaluator](../../../extensibility/debugger/reference/idebugexpressionevaluator.md) インターフェイスのメソッドに加えて、次のメソッドを実装します。

|Method|説明|
|------------|-----------------|
|[GetService](../../../extensibility/debugger/reference/idebugexpressionevaluator2-getservice.md)|一意の識別子を指定して、サービスオブジェクトを取得します。|
|[PreloadModules](../../../extensibility/debugger/reference/idebugexpressionevaluator2-preloadmodules.md)|指定したシンボルプロバイダーによって指定されたモジュールをプリロードします。|
|[SetCallback](../../../extensibility/debugger/reference/idebugexpressionevaluator2-setcallback.md)|式エバリュエーター (EE) が、デバッガーエンジン (DE) がメトリック設定の読み取りに使用するコールバックインターフェイスを指定できるようにします。|
|[SetCorPath](../../../extensibility/debugger/reference/idebugexpressionevaluator2-setcorpath.md)|デバッガーに読み込まれている共通言語ランタイム (CLR) へのパスを設定します。|
|[SetIDebugIDECallback](../../../extensibility/debugger/reference/idebugexpressionevaluator2-setidebugidecallback.md)|初期化中に、デバッグエンジンがコールバックを式エバリュエーターに渡すことができるようにします。|
|[Terminate](../../../extensibility/debugger/reference/idebugexpressionevaluator2-terminate.md)|式エバリュエーターを停止してクリーンアップします。|

## <a name="requirements"></a>必要条件
 ヘッダー: Ee

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
