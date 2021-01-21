---
title: 式の評価 |Microsoft Docs
description: '[自動変数]、[ウォッチ]、[クイックウォッチ]、または [イミディエイト] ウィンドウから渡された文字列から作成される式の評価について説明します。'
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- expressions [Debugging SDK], evaluating
- debugging [Debugging SDK], expression evaluation
- expression evaluation
ms.assetid: 5ccfcc80-dea5-48a1-8bae-6a26f8d3bc56
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b43fc91de129407f2fd01e12951cffee4028186f
ms.sourcegitcommit: 8e9c38da7bcfbe9a461c378083846714933a0e1e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/09/2020
ms.locfileid: "96914596"
---
# <a name="evaluate-expressions"></a>式の評価
式は、[ **自動変数**]、[ **ウォッチ**]、[ **クイックウォッチ**]、または [ **イミディエイト** ] ウィンドウから渡された文字列から作成されます。 式が評価されると、変数または引数の名前と型、およびその値を含む、印刷可能な文字列が生成されます。 この文字列は、対応する IDE ウィンドウに表示されます。

## <a name="implementation"></a>実装
 式は、ブレークポイントでプログラムが停止したときに評価されます。 式自体は、 [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) インターフェイスによって表されます。これは、指定された式の評価コンテキスト内でバインドおよび評価の準備ができている解析済みの式を表します。 スタックフレームは、 [IDebugExpressionContext2](../../extensibility/debugger/reference/idebugexpressioncontext2.md) インターフェイスを実装することによってデバッグエンジン (DE) が提供する式の評価コンテキストを決定します。

 ユーザー文字列と[IDebugExpressionContext2](../../extensibility/debugger/reference/idebugexpressioncontext2.md)インターフェイスが指定されている場合、デバッグエンジン (DE) は、ユーザー文字列を[IDebugExpressionContext2::P arsetext](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)メソッドに渡すことによって[IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md)インターフェイスを取得できます。 返される IDebugExpression2 インターフェイスには、評価のために準備された解析済みの式が含まれます。

 インターフェイスを使用して `IDebugExpression2` 、DE は、 [IDebugExpression2:: EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) または [IDebugExpression2:: evaluateasync](../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)を使用して、同期または非同期の式の評価によって式の値を取得できます。 この値は、変数または引数の名前および型と共に IDE に送信され、表示されます。 値、名前、および型は、 [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) インターフェイスによって表されます。

 式の評価を有効にするには、DE で [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) インターフェイスと [IDebugExpressionContext2](../../extensibility/debugger/reference/idebugexpressioncontext2.md) インターフェイスを実装する必要があります。 同期と非同期のどちらの評価でも、 [IDebugProperty2:: GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md) メソッドの実装が必要です。

## <a name="see-also"></a>関連項目
- [スタックフレーム](../../extensibility/debugger/stack-frames.md)
- [式の評価コンテキスト](../../extensibility/debugger/expression-evaluation-context.md)
- [タスクをデバッグする](../../extensibility/debugger/debugging-tasks.md)
