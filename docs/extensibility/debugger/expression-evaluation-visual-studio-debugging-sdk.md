---
title: 式の評価 (Visual Studio デバッグ SDK) |マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738717"
---
# <a name="expression-evaluation-visual-studio-debugging-sdk"></a>式の評価 (デバッグ SDK)
中断モードの間、IDE は、複数のプログラム変数を含む単純な式を評価する必要があります。 その評価を完了するには、デバッグ エンジン (DE) は、IDE のウィンドウの 1 つに入力された式を解析し、評価する必要があります。

 式は、メソッドを使用して作成[:Pされます](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)。 [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md)

 **IDebugExpression2**インターフェイスは、DE によって実装され、IDE で式の評価の結果を表示するために、IDE に[IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)インターフェイスを返す**その EvalAsync**メソッドを呼び出します。 [IDebugProperty2::GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md)は、式の値を**ウォッチ**ウィンドウまたは**ローカル**ウィンドウに配置するために使用される構造体を返します。

 デバッグ パッケージまたはセッション デバッグ マネージャー (SDM) は、評価の結果を表す[IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)インターフェイスを取得するために[IDebugExpression2::評価非同期](../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)または[評価同期](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)を呼び出します。 `IDebugProperty2`には、式の名前、型、および値を返すメソッドがあります。 この情報は、さまざまなデバッガー ウィンドウに表示されます。

## <a name="using-expression-evaluation"></a>式の評価を使用する
 式の評価を使用するには、次の表に示すように[、IDebugExpressionContext2::ParseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)メソッドと[IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md)インターフェイスのすべてのメソッドを実装する必要があります。

|Method|説明|
|------------|-----------------|
|[EvaluateAsync](../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)|式を非同期的に評価します。|
|[中止](../../extensibility/debugger/reference/idebugexpression2-abort.md)|非同期式の評価を終了します。|
|[EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)|式を同期的に評価します。|

 同期および非同期の評価では、[メソッド](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md)を実装する必要があります。 非同期式の評価には[、IDebug 式の評価完了イベント 2](../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md)の実装が必要です。

## <a name="see-also"></a>関連項目
- [実行制御と状態評価](../../extensibility/debugger/execution-control-and-state-evaluation.md)
