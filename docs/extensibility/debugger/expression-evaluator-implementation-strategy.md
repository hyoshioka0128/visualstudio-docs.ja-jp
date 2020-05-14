---
title: 式エバリュエータ実装戦略 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- expression evaluation, implementation strategy
- debug engines, implementation strategies
ms.assetid: 1bccaeb3-8109-4128-ae79-16fd8fbbaaa2
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 3922689c20c839b3c0c2b2440bc9fefd5d25c80a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738675"
---
# <a name="expression-evaluator-implementation-strategy"></a>式エバリュエーター実装戦略
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターのこの実装方法は非推奨になりました。 CLR 式エバリュエーターの実装については[、「CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) 」および「[マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

 式エバリュエーター (EE) を迅速に作成する方法の 1 つは、まずローカル変数を **[ローカル**] ウィンドウに表示するために必要な最小限のコードを実装することです。 ローカル変数の名前、型、値が **[ローカル]** ウィンドウの各行に表示され、3 つすべてが[IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)オブジェクトによって表されることを理解すると便利です。 ローカル変数の名前、型、および値は、その`IDebugProperty2`[GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md)メソッドを呼び出すことによってオブジェクトから取得されます。 ローカル変数を **[ローカル**] ウィンドウに表示する方法の詳細については、「ローカル変数の[表示](../../extensibility/debugger/displaying-locals.md)」を参照してください。

## <a name="discussion"></a>ディスカッション
 可能な実装シーケンスは[、IDebug 式エバリュエーター](../../extensibility/debugger/reference/idebugexpressionevaluator.md)の実装から始まります。 ローカルを表示するには[、Parse](../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md)メソッドと[GetMethodProperty](../../extensibility/debugger/reference/idebugexpressionevaluator-getmethodproperty.md)メソッドを実装する必要があります。 呼`IDebugExpressionEvaluator::GetMethodProperty`び出`IDebugProperty2`しは、メソッドを表[すオブジェクトを](../../extensibility/debugger/reference/idebugmethodfield.md)返します。 メソッド自体は、[**ローカル**] ウィンドウには表示されません。

 次に[EnumChildren](../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)メソッドを実装する必要があります。 デバッグ エンジン (DE) は、このメソッドを呼び出して、 の`IDebugProperty2::EnumChildren`引数`guidFilter`を渡`guidFilterLocalsPlusArgs`すことによって、ローカル変数と引数の一覧を取得します。 `IDebugProperty2::EnumChildren`を呼び出す[EnumArguments](../../extensibility/debugger/reference/idebugmethodfield-enumarguments.md)と[EnumLocals](../../extensibility/debugger/reference/idebugmethodfield-enumlocals.md)を 1 つの列挙体で結果を結合します。 詳細については、「[ローカルの表示](../../extensibility/debugger/displaying-locals.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [式エバリュエーターの実装](../../extensibility/debugger/implementing-an-expression-evaluator.md)
- [ローカル表示](../../extensibility/debugger/displaying-locals.md)
