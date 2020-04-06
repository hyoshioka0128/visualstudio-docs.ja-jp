---
title: ローカルの表示 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], expression evaluation
- expression evaluation, displaying locals
ms.assetid: 62264cec-845b-4233-aed7-0b038fa79250
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 4d44b276aeb9c6acb0ef34cc186662d49246de7d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738934"
---
# <a name="display-locals"></a>ローカル表示
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターのこの実装方法は非推奨になりました。 CLR 式エバリュエーターの実装については[、「CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) 」および「[マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

 実行は、常にメソッドのコンテキスト内で行われます。 実行が一時停止すると、Visual Studio はデバッグ エンジン (DE) を呼び出して、メソッドのローカル変数とローカル変数の一覧を取得します。 Visual Studio では、これらのローカル変数とその値が **[ローカル]** ウィンドウに表示されます。

 ローカルを表示するには、DE は、EE に属する[GetMethodProperty](../../extensibility/debugger/reference/idebugexpressionevaluator-getmethodproperty.md)メソッドを呼び出し、評価コンテキスト、つまり、シンボル プロバイダー (SP)、現在の実行アドレス、およびバインダー オブジェクトを提供します。 詳細については、「[評価コンテキスト](../../extensibility/debugger/evaluation-context.md)」を参照してください。 呼び出しが成功した`IDebugExpressionEvaluator::GetMethodProperty`場合、メソッドは、現在の実行アドレスを含むメソッドを表す[IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)オブジェクトを返します。

 DE は[EnumChildren](../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)を呼び出して[IEnumDebugPropertyInfo2](../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md)オブジェクトを取得[DEBUG_PROPERTY_INFO](../../extensibility/debugger/reference/debug-property-info.md)します。 各構造体には、ローカルの名前、型、および値が含まれます。 型と値は、表示に適した書式付き文字列として格納されます。 名前、型、および値は、通常、[**ローカル**] ウィンドウの 1 行にまとめて表示されます。

> [!NOTE]
> **[クイック ウォッチ]** ウィンドウと **[ウォッチ]** ウィンドウには、名前、値、および種類の同じ形式の変数も表示されます。 ただし、これらの値は、 の代わりに[GetPropertyInfo を](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md)呼び出すことによって取得されます`IDebugProperty2::EnumChildren`。

## <a name="in-this-section"></a>このセクションの内容
 [ローカルのサンプル実装](../../extensibility/debugger/sample-implementation-of-locals.md)例を使用して、ローカルを実装するプロセスを段階的に実行します。

## <a name="related-sections"></a>関連項目
 [評価コンテキスト](../../extensibility/debugger/evaluation-context.md)デバッグ エンジン (DE) が式エバリュエーター (EE) を呼び出すときに、3 つの引数を渡す方法について説明します。

## <a name="see-also"></a>関連項目
 [CLR 式エバリュエーターを記述する](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
