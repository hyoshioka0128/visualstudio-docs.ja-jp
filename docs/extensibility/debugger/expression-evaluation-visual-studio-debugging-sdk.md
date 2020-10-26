---
title: 式の評価 (Visual Studio デバッグ SDK) |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], expression evaluation
- expression evaluation
ms.assetid: 5044ced5-c18c-4534-b0bf-cc3e50cd57ac
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: e41179fd530818f5ac59aa54420ede1b4eafa1ec
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80738717"
---
# <a name="expression-evaluation-visual-studio-debugging-sdk"></a>式の評価 (Visual Studio デバッグ SDK)
中断モードでは、IDE は複数のプログラム変数を含む単純な式を評価する必要があります。 この評価を行うには、デバッグエンジン (DE) が IDE のウィンドウのいずれかに入力された式を解析して評価する必要があります。

 式は、 [IDebugExpressionContext2::P arseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) メソッドを使用して作成され、結果の [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) インターフェイスによって表されます。

 **IDebugExpression2**インターフェイスは DE によって実装され、式の評価結果を ide に表示するために、 [IDEBUGPROPERTY2](../../extensibility/debugger/reference/idebugproperty2.md)インターフェイスを ide に返すために**evalasync**メソッドを呼び出します。 [IDebugProperty2:: GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md) は、式の値を [ **ウォッチ** ] ウィンドウまたは [ **ローカル** ] ウィンドウに配置するために使用される構造体を返します。

 デバッグパッケージまたはセッションデバッグマネージャー (SDM) は、 [IDebugExpression2:: EvaluateAsync](../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md) または [EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) を呼び出して、評価の結果を表す [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) インターフェイスを取得します。 `IDebugProperty2` には、式の名前、型、および値を返すメソッドがあります。 この情報は、さまざまなデバッガーウィンドウに表示されます。

## <a name="using-expression-evaluation"></a>式の評価の使用
 式の評価を使用するには、次の表に示すように、 [IDebugExpressionContext2::P arseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) メソッドと [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) インターフェイスのすべてのメソッドを実装する必要があります。

|Method|説明|
|------------|-----------------|
|[EvaluateAsync](../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)|式を非同期的に評価します。|
|[中止](../../extensibility/debugger/reference/idebugexpression2-abort.md)|非同期式の評価を終了します。|
|[EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)|式を同期的に評価します。|

 同期および非同期評価を行うには、 [IDebugProperty2:: GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md) メソッドを実装する必要があります。 非同期式の評価には、 [IDebugExpressionEvaluationCompleteEvent2](../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md)の実装が必要です。

## <a name="see-also"></a>関連項目
- [実行制御と状態の評価](../../extensibility/debugger/execution-control-and-state-evaluation.md)
