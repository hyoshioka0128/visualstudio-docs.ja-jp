---
title: 表示 (ローカル |)Microsoft Docs
description: ローカル変数と引数の一覧について説明します。これは、実行が一時停止したときに表示される、メソッドのローカル変数と総称されます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], expression evaluation
- expression evaluation, displaying locals
ms.assetid: 62264cec-845b-4233-aed7-0b038fa79250
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 564b42a15e1420027b79cb5f00c70f61649ad4f9
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105097267"
---
# <a name="display-locals"></a>ローカルの表示
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターを実装するこの方法は非推奨とされます。 CLR 式エバリュエーターの実装の詳細については、「 [clr 式](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) エバリュエーターと [マネージ式エバリュエーターサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

 実行は常にメソッドのコンテキスト内で行われます。これは、コンテナーメソッドまたは現在のメソッドとも呼ばれます。 実行が一時停止すると、Visual Studio はデバッグエンジン (DE) を呼び出してローカル変数と引数の一覧を取得します。これは、総称してメソッドのローカルと呼ばれます。 これらのローカルと値は、Visual Studio の [ **ローカル** ] ウィンドウに表示されます。

 ローカルを表示するために、DE は、EE に属する [Getmethodproperty](../../extensibility/debugger/reference/idebugexpressionevaluator-getmethodproperty.md) メソッドを呼び出し、評価コンテキスト (つまり、シンボルプロバイダー (SP)、現在の実行アドレス、およびバインダーオブジェクト) を提供します。 詳細については、「 [評価コンテキスト](../../extensibility/debugger/evaluation-context.md)」を参照してください。 呼び出しが成功した場合、メソッドは、 `IDebugExpressionEvaluator::GetMethodProperty` 現在の実行アドレスを含むメソッドを表す [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) オブジェクトを返します。

 DE は、 [IEnumDebugPropertyInfo2](../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md)オブジェクトを取得するために[enumchildren](../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)を呼び出します。このオブジェクトは、ローカルと列挙型のみを返して[DEBUG_PROPERTY_INFO](../../extensibility/debugger/reference/debug-property-info.md)構造体のリストを生成するようにフィルター処理されます。 各構造体には、ローカルのの名前、型、および値が含まれます。 型と値は、表示に適した書式設定された文字列として格納されます。 通常、名前、型、および値は、[ **ローカル** ] ウィンドウの1行にまとめて表示されます。

> [!NOTE]
> [ **クイックウォッチ** ] ウィンドウと [ **ウォッチ** ] ウィンドウには、同じ形式の名前、値、および型の変数も表示されます。 ただし、これらの値は、ではなく [GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md) を呼び出すことによって取得され `IDebugProperty2::EnumChildren` ます。

## <a name="in-this-section"></a>このセクションの内容
 [ローカルの実装のサンプル](../../extensibility/debugger/sample-implementation-of-locals.md) 例を使用して、ローカルを実装するプロセスを段階的に実行します。

## <a name="related-sections"></a>関連項目
 [評価コンテキスト](../../extensibility/debugger/evaluation-context.md) デバッグエンジン (DE) が式エバリュエーター (EE) を呼び出すと、3つの引数が渡されることについて説明します。

## <a name="see-also"></a>こちらもご覧ください
 [CLR 式エバリュエーターを記述する](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
