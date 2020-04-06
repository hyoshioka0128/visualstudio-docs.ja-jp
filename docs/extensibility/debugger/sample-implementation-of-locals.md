---
title: ローカルの実装例 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], local variables
- expression evaluation, local variables
ms.assetid: 66a2e00a-f558-4e87-96b8-5ecf5509e04c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6b70e0f9091d40ed6b5fc44934606f42ccd84b21
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80713074"
---
# <a name="sample-implementation-of-locals"></a>ローカルのサンプル実装
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターのこの実装方法は非推奨になりました。 CLR 式エバリュエーターの実装については[、「CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) 」および「[マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

 Visual Studio が式エバリュエーター (EE) からメソッドのローカルを取得する方法の概要を次に示します。

1. デバッグ エンジン (DE) を呼び出す[GetDebugProperty](../../extensibility/debugger/reference/idebugstackframe2-getdebugproperty.md)を取得する[IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)オブジェクトをスタック フレームのすべてのプロパティを表す、ローカルを含みます。

2. `IDebugStackFrame2::GetDebugProperty`ブレークポイントが発生したメソッドを記述するオブジェクトを取得する[GetMethodProperty](../../extensibility/debugger/reference/idebugexpressionevaluator-getmethodproperty.md)を呼び出します。 DE は、シンボル プロバイダー ([IDebugSymbolProvider](../../extensibility/debugger/reference/idebugsymbolprovider.md)) 、アドレス ([IDebugAddress](../../extensibility/debugger/reference/idebugaddress.md)) 、およびバインダー ([IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md)) を提供します。

3. `IDebugExpressionEvaluator::GetMethodProperty`指定されたアドレスを含むメソッド`IDebugAddress`を表す[IDebugContainerField](../../extensibility/debugger/reference/idebugcontainerfield.md)を取得するには、指定されたオブジェクトを使用して[GetContainerField](../../extensibility/debugger/reference/idebugsymbolprovider-getcontainerfield.md)を呼び出します。

4. インターフェイス`IDebugContainerField`は、[インターフェイスに対して](../../extensibility/debugger/reference/idebugmethodfield.md)クエリされます。 メソッドのローカルにアクセスできるインターフェイスです。

5. `IDebugExpressionEvaluator::GetMethodProperty`メソッドのローカルを表す`CFieldProperty``IDebugProperty2`インターフェイスを実行するクラス (サンプルで呼び出されます) をインスタンス化します。 オブジェクト`IDebugMethodField`は、 、 `CFieldProperty` 、`IDebugAddress`および`IDebugBinder`オブジェクト`IDebugSymbolProvider`と共にこのオブジェクトに配置されます。

6. オブジェクトが`CFieldProperty`初期化されると[、GetInfo](../../extensibility/debugger/reference/idebugfield-getinfo.md)メソッド自体に関`IDebugMethodField`するすべての表示可能な情報を含む[FIELD_INFO](../../extensibility/debugger/reference/field-info.md)構造体を取得するために、オブジェクトに対して GetInfo が呼び出されます。

7. `IDebugExpressionEvaluator::GetMethodProperty`オブジェクトを`CFieldProperty``IDebugProperty2`オブジェクトとして返します。

8. メソッドのローカルを含む[IEnumDebugPropertyInfo2](../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md)オブジェクトを返すフィルター`IDebugProperty2``guidFilterLocalsPlusArgs`を使用して、返されたオブジェクトの[列挙子](../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)を呼び出します。 この列挙体は、 [EnumLocals](../../extensibility/debugger/reference/idebugmethodfield-enumlocals.md)と[EnumArguments](../../extensibility/debugger/reference/idebugmethodfield-enumarguments.md)の呼び出しによって入力されます。

9. Visual Studio は[、ローカル](../../extensibility/debugger/reference/ienumdebugpropertyinfo2-next.md)ごとに[DEBUG_PROPERTY_INFO](../../extensibility/debugger/reference/debug-property-info.md)構造を取得するために Next を呼び出します。 この構造体には、ローカルの`IDebugProperty2`インターフェイスへのポインターが含まれています。

10. ローカルの名前、値、および型を取得する各ローカルの[GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md)を呼び出します。 この情報は、[**ローカル**] ウィンドウに表示されます。

## <a name="in-this-section"></a>このセクションの内容
 [プロパティを実装します。](../../extensibility/debugger/implementing-getmethodproperty.md)の実装について説明[します](../../extensibility/debugger/reference/idebugexpressionevaluator-getmethodproperty.md)。

 [ローカルの列挙](../../extensibility/debugger/enumerating-locals.md)デバッグ エンジン (DE) がローカル変数または引数を列挙する呼び出しを行う方法について説明します。

 [ローカル プロパティを取得する](../../extensibility/debugger/getting-local-properties.md)1 つ以上のローカルの名前、型、および値を取得する呼び出しを DE がどのように行うかを説明します。

 [ローカル値を取得する](../../extensibility/debugger/getting-local-values.md)評価コンテキストによって与えられたバインダー オブジェクトのサービスを必要とするローカルの値の取得について説明します。

 [ローカルを評価する](../../extensibility/debugger/evaluating-locals.md)ローカルの評価方法について説明します。

## <a name="related-sections"></a>関連項目
 [評価コンテキスト](../../extensibility/debugger/evaluation-context.md)DE が式エバリュエーター (EE) を呼び出すときに渡される引数を提供します。

 [MyCEE サンプル](https://msdn.microsoft.com/library/624a018b-9179-402f-9d48-3aec87b48f4f)MyC 言語の式エバリュエーターを作成するための 1 つの実装方法を示します。

## <a name="see-also"></a>関連項目
- [ローカルの表示](../../extensibility/debugger/displaying-locals.md)
