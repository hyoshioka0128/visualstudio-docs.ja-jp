---
title: 式の評価 |マイクロソフトドキュメント
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
ms.openlocfilehash: 18e342704cbb4abd7de9667576ce331ef8fbf60a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738835"
---
# <a name="evaluate-expressions"></a>式の評価
式は、[**自動**] ウィンドウ 、[ウォッチ] ウィンドウ、[**クイック****ウォッチ**] ウィンドウ、または **[イミディエイト**] ウィンドウから渡された文字列から作成されます。 式が評価されると、変数または引数の名前と型とその値を含む、印刷可能な文字列が生成されます。 この文字列は、対応する IDE ウィンドウに表示されます。

## <a name="implementation"></a>実装
 プログラムがブレークポイントで停止したときに式が評価されます。 式自体は、指定された式の評価コンテキスト内でバインディングと評価の準備が整った解析済みの式を表す[IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md)インターフェイスによって表されます。 スタック フレームは、デバッグ エンジン (DE) が[IDebugExpressionContext2](../../extensibility/debugger/reference/idebugexpressioncontext2.md)インターフェイスを実装することによって提供する式の評価コンテキストを決定します。

 ユーザー文字列と[IDebugExpressionContext2](../../extensibility/debugger/reference/idebugexpressioncontext2.md)インターフェイスを指定すると、デバッグ エンジン (DE) は、ユーザー文字列を[IDebugExpressionContext2::ParseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)メソッドに渡すことによって[IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md)インターフェイスを取得できます。 返される IDebugExpression2 インターフェイスには、解析済み式が含まれています。

 インターフェイスを`IDebugExpression2`使用すると、DE は[、同期式または](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)非同期式の評価を使用して式の値[を](../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)取得できます。 この値は、変数または引数の名前と型とともに IDE に送信され、表示されます。 値、名前、および型は[、IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)インターフェイスによって表されます。

 式の評価を有効にするには、DE が[IDebugExpression2 インターフェイスと IDebugExpressionContext2](../../extensibility/debugger/reference/idebugexpression2.md)インターフェイス[を](../../extensibility/debugger/reference/idebugexpressioncontext2.md)実装する必要があります。 同期評価と非同期評価の両方で、メソッドの実装[が](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md)必要です。

## <a name="see-also"></a>関連項目
- [スタック フレーム](../../extensibility/debugger/stack-frames.md)
- [式評価コンテキスト](../../extensibility/debugger/expression-evaluation-context.md)
- [デバッグ タスク](../../extensibility/debugger/debugging-tasks.md)
