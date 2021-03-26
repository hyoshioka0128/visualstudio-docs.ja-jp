---
title: ローカル変数 | の実装の例Microsoft Docs
description: この記事の式エバリュエーターから Visual Studio がメソッドのローカルを取得する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], local variables
- expression evaluation, local variables
ms.assetid: 66a2e00a-f558-4e87-96b8-5ecf5509e04c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 4bf07dc6f47391af14c878021c742c2cb461bc85
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105070415"
---
# <a name="sample-implementation-of-locals"></a>ローカルの実装のサンプル
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターを実装するこの方法は非推奨とされます。 CLR 式エバリュエーターの実装の詳細については、「 [clr 式](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) エバリュエーターと [マネージ式エバリュエーターサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

 次に、Visual Studio が式エバリュエーター (EE) からメソッドのローカルを取得する方法の概要を示します。

1. Visual Studio は、デバッグエンジンの (DE) [Getdebugproperty](../../extensibility/debugger/reference/idebugstackframe2-getdebugproperty.md) を呼び出して、ローカルを含むスタックフレームのすべてのプロパティを表す [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) オブジェクトを取得します。

2. `IDebugStackFrame2::GetDebugProperty`[Getmethodproperty](../../extensibility/debugger/reference/idebugexpressionevaluator-getmethodproperty.md)を呼び出して、ブレークポイントが発生したメソッドを説明するオブジェクトを取得します。 DE は、シンボルプロバイダー ([IDebugSymbolProvider](../../extensibility/debugger/reference/idebugsymbolprovider.md))、アドレス ([IDebugAddress](../../extensibility/debugger/reference/idebugaddress.md))、バインダー ([IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md)) を提供します。

3. `IDebugExpressionEvaluator::GetMethodProperty` 指定されたオブジェクトを使用して [GetContainerField](../../extensibility/debugger/reference/idebugsymbolprovider-getcontainerfield.md) を呼び出し、指定した `IDebugAddress` アドレスを含むメソッドを表す [IDebugContainerField](../../extensibility/debugger/reference/idebugcontainerfield.md) を取得します。

4. インターフェイスは、 `IDebugContainerField` [IDebugMethodField](../../extensibility/debugger/reference/idebugmethodfield.md) インターフェイスに対して照会されます。 このインターフェイスは、メソッドのローカル変数へのアクセスを提供します。

5. `IDebugExpressionEvaluator::GetMethodProperty``CFieldProperty`メソッドのローカルを表すインターフェイスを実行するクラス (サンプルではと呼ばれます) をインスタンス化し `IDebugProperty2` ます。 `IDebugMethodField`オブジェクトは、、、およびの各オブジェクトと共に、このオブジェクトに配置され `CFieldProperty` `IDebugSymbolProvider` `IDebugAddress` `IDebugBinder` ます。

6. `CFieldProperty`オブジェクトが初期化されると、オブジェクトに対して[GetInfo](../../extensibility/debugger/reference/idebugfield-getinfo.md)が呼び出され、 `IDebugMethodField` メソッド自体に関するすべての表示可能な情報を含む[FIELD_INFO](../../extensibility/debugger/reference/field-info.md)構造が取得されます。

7. `IDebugExpressionEvaluator::GetMethodProperty` オブジェクトを `CFieldProperty` オブジェクトとして返し `IDebugProperty2` ます。

8. Visual Studio は、返されたオブジェクトに対して [Enumchildren](../../extensibility/debugger/reference/idebugproperty2-enumchildren.md) を呼び出し `IDebugProperty2` ます。フィルターは、 `guidFilterLocalsPlusArgs` メソッドのローカルを含む [IEnumDebugPropertyInfo2](../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md) オブジェクトを返します。 この列挙体は、 [Enumlocals](../../extensibility/debugger/reference/idebugmethodfield-enumlocals.md) および [enumlocals](../../extensibility/debugger/reference/idebugmethodfield-enumarguments.md)の呼び出しによって入力されます。

9. Visual Studio は、 [次](../../extensibility/debugger/reference/ienumdebugpropertyinfo2-next.md) にを呼び出して、各ローカルの [DEBUG_PROPERTY_INFO](../../extensibility/debugger/reference/debug-property-info.md) 構造を取得します。 この構造体に `IDebugProperty2` は、ローカルののインターフェイスへのポインターが含まれています。

10. Visual Studio は、ローカルの名前、値、および型を取得するために、各ローカルの [GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md) を呼び出します。 この情報は、[ **ローカル** ] ウィンドウに表示されます。

## <a name="in-this-section"></a>このセクションの内容
 [GetMethodProperty を実装](../../extensibility/debugger/implementing-getmethodproperty.md) する [Getmethodproperty](../../extensibility/debugger/reference/idebugexpressionevaluator-getmethodproperty.md)の実装について説明します。

 [ローカルの列挙](../../extensibility/debugger/enumerating-locals.md) デバッグエンジン (DE) がローカル変数または引数を列挙する呼び出しを行う方法について説明します。

 [ローカルプロパティの取得](../../extensibility/debugger/getting-local-properties.md) DE が1つ以上のローカルの名前、型、および値を取得するための呼び出しを行う方法について説明します。

 [ローカル値の取得](../../extensibility/debugger/getting-local-values.md) 評価コンテキストによって指定されたバインダーオブジェクトのサービスを必要とする、ローカルのの値を取得する方法について説明します。

 [ローカルの評価](../../extensibility/debugger/evaluating-locals.md) ローカル変数の評価方法について説明します。

## <a name="related-sections"></a>関連項目
 [評価コンテキスト](../../extensibility/debugger/evaluation-context.md) DE が式エバリュエーター (EE) を呼び出すときに渡される引数を提供します。

 [MyCEE サンプル](/previous-versions/) MyC 言語の式エバリュエーターを作成するための1つの実装方法を示します。

## <a name="see-also"></a>こちらもご覧ください
- [表示 (ローカルを)](../../extensibility/debugger/displaying-locals.md)