---
title: IDebugExpressionEvaluator3 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugExpressionEvaluator3 interface
ms.assetid: c27c2a14-300b-4535-be22-767c83602f69
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d25cd8cd4aec351df2a483e930bf469fbc086a68
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80729115"
---
# <a name="idebugexpressionevaluator3"></a>IDebugExpressionEvaluator3
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターを実装するこの方法は非推奨とされます。 CLR 式エバリュエーターの実装の詳細については、「 [Clr 式](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) エバリュエーターと [マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

 パーサーツリーが拡張された式エバリュエーター (EE) を表します。

## <a name="syntax"></a>構文

```
IDebugExpressionEvaluator3 : IDebugExpressionEvaluator2
```

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 このバージョンのパーサーは、シンボルプロバイダーと、評価フレームのアドレスを渡します。

## <a name="methods"></a>メソッド
 このインターフェイスは、 [IDebugExpressionEvaluator2](../../../extensibility/debugger/reference/idebugexpressionevaluator2.md) インターフェイスのメソッドに加えて、次のメソッドを実装します。

|Method|説明|
|------------|-----------------|
|[Parse2](../../../extensibility/debugger/reference/idebugexpressionevaluator3-parse2.md)|シンボルプロバイダーおよび評価フレームのアドレスを指定して、式文字列を解析済みの式に変換します。|

## <a name="requirements"></a>必要条件
 ヘッダー: Ee

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
