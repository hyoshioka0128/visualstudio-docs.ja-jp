---
title: ローカル変数 | の実装の例Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], local variables
- expression evaluation, local variables
ms.assetid: 66a2e00a-f558-4e87-96b8-5ecf5509e04c
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 6e943fd7ba27fe21029bab4d818803186147476e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65704885"
---
# <a name="sample-implementation-of-locals"></a>ローカルの実装のサンプル
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターを実装するこの方法は非推奨とされます。 CLR 式エバリュエーターの実装の詳細については、「 [Clr 式](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) エバリュエーターと [マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。  
  
 次に、Visual Studio が式エバリュエーター (EE) からメソッドのローカルを取得する方法の概要を示します。  
  
1. Visual Studio は、デバッグエンジンの (DE) [Getdebugproperty](../../extensibility/debugger/reference/idebugstackframe2-getdebugproperty.md) を呼び出して、ローカルを含むスタックフレームのすべてのプロパティを表す [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) オブジェクトを取得します。  
  
2. `IDebugStackFrame2::GetDebugProperty`[Getmethodproperty](../../extensibility/debugger/reference/idebugexpressionevaluator-getmethodproperty.md)を呼び出して、ブレークポイントが発生したメソッドを説明するオブジェクトを取得します。 DE は、シンボルプロバイダー ([IDebugSymbolProvider](../../extensibility/debugger/reference/idebugsymbolprovider.md))、アドレス ([IDebugAddress](../../extensibility/debugger/reference/idebugaddress.md))、バインダー ([IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md)) を提供します。  
  
3. `IDebugExpressionEvaluator::GetMethodProperty` 指定されたオブジェクトを使用して [GetContainerField](../../extensibility/debugger/reference/idebugsymbolprovider-getcontainerfield.md) を呼び出し、 `IDebugAddress` 指定したアドレスを含むメソッドを表す [IDebugContainerField](../../extensibility/debugger/reference/idebugcontainerfield.md) を取得します。  
  
4. インターフェイスは、 `IDebugContainerField` [IDebugMethodField](../../extensibility/debugger/reference/idebugmethodfield.md) インターフェイスに対して照会されます。 これは、メソッドのローカル変数へのアクセスを提供するインターフェイスです。  
  
5. `IDebugExpressionEvaluator::GetMethodProperty``CFieldProperty`メソッドのローカルを表すインターフェイスを実装するクラス (サンプルではと呼ばれます) をインスタンス化し `IDebugProperty2` ます。 `IDebugMethodField`オブジェクトは `CFieldProperty` `IDebugSymbolProvider` 、、、およびの各オブジェクトと共に、このオブジェクトに配置され `IDebugAddress` `IDebugBinder` ます。  
  
6. `CFieldProperty`オブジェクトが初期化されると、オブジェクトに対して[GetInfo](../../extensibility/debugger/reference/idebugfield-getinfo.md)が呼び出され、 `IDebugMethodField` メソッド自体に関するすべての表示可能な情報を含む[FIELD_INFO](../../extensibility/debugger/reference/field-info.md)構造を取得します。  
  
7. `IDebugExpressionEvaluator::GetMethodProperty` オブジェクトを `CFieldProperty` オブジェクトとして返し `IDebugProperty2` ます。  
  
8. Visual Studio は、フィルターを使用して、返されたオブジェクトで [Enumchildren](../../extensibility/debugger/reference/idebugproperty2-enumchildren.md) を呼び出し `IDebugProperty2` `guidFilterLocalsPlusArgs` ます。 これにより、メソッドのローカル変数を含む [IEnumDebugPropertyInfo2](../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md) オブジェクトが返されます。 この列挙体は、 [Enumlocals](../../extensibility/debugger/reference/idebugmethodfield-enumlocals.md) および [enumlocals](../../extensibility/debugger/reference/idebugmethodfield-enumarguments.md)の呼び出しによって入力されます。  
  
9. Visual Studio は、 [次](../../extensibility/debugger/reference/ienumdebugpropertyinfo2-next.md) にを呼び出して、各ローカルの [DEBUG_PROPERTY_INFO](../../extensibility/debugger/reference/debug-property-info.md) 構造を取得します。 この構造体に `IDebugProperty2` は、ローカルののインターフェイスへのポインターが含まれています。  
  
10. Visual Studio は、ローカルの名前、値、および型を取得するために、各ローカルの [GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md) を呼び出します。 これは、[ **ローカル** ] ウィンドウに表示される情報です。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [GetMethodProperty の実装](../../extensibility/debugger/implementing-getmethodproperty.md)  
 [Getmethodproperty](../../extensibility/debugger/reference/idebugexpressionevaluator-getmethodproperty.md)の実装について説明します。  
  
 [ローカルの列挙](../../extensibility/debugger/enumerating-locals.md)  
 デバッグエンジン (DE) がローカル変数または引数を列挙する呼び出しを行う方法について説明します。  
  
 [ローカル プロパティの取得](../../extensibility/debugger/getting-local-properties.md)  
 DE が1つ以上のローカルの名前、型、および値を取得するための呼び出しを行う方法について説明します。  
  
 [ローカル値の取得](../../extensibility/debugger/getting-local-values.md)  
 評価コンテキストによって指定されたバインダーオブジェクトのサービスを必要とする、ローカルの値の取得について説明します。  
  
 [ローカル変数の評価](../../extensibility/debugger/evaluating-locals.md)  
 ローカル変数の評価方法について説明します。  
  
## <a name="related-sections"></a>関連項目  
 [評価コンテキスト](../../extensibility/debugger/evaluation-context.md)  
 DE が式エバリュエーター (EE) を呼び出すときに渡される引数を提供します。  
  
 [MyCEE サンプル](https://msdn.microsoft.com/624a018b-9179-402f-9d48-3aec87b48f4f)  
 MyC 言語の式エバリュエーターを作成するための1つの実装方法を示します。  
  
## <a name="see-also"></a>参照  
 [ローカルの表示](../../extensibility/debugger/displaying-locals.md)
