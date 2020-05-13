---
title: ウォッチ式の評価 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- expression evaluation, watch expressions
- watch expressions
ms.assetid: 8317cd52-6fea-4e8f-a739-774dc06bd44b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9a239e430338e88a0be4bc35ad1c357925f7d8f5
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738855"
---
# <a name="evaluate-a-watch-expression"></a>ウォッチ式を評価する
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターのこの実装方法は非推奨になりました。 CLR 式エバリュエーターの実装については[、「CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) 」および「[マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

Visual Studio でウォッチ式の値を表示する準備が整うと[、EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)が呼び出され、次に[EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)が呼び出されます。 このプロセスは、式の値と型を含む[IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)オブジェクトを生成します。

のこの実装`IDebugParsedExpression::EvaluateSync`では、式が解析され、同時に評価されます。 この実装では、次のタスクを実行します。

1. 式を解析して評価し、値とその型を保持するジェネリック オブジェクトを生成します。 C# では、これは C++`object`では while として表され、これは`VARIANT`.

2. インターフェイスを実装し、返`CValueProperty`される値を`IDebugProperty2`クラスに格納するクラス (この例で呼び出される) をインスタンス化します。

3. オブジェクトから`IDebugProperty2`インターフェイスを`CValueProperty`返します。

## <a name="managed-code"></a>マネージド コード
これは、in マネージ`IDebugParsedExpression::EvaluateSync`コードの実装です。 ヘルパー メソッド`Tokenize`は、式を解析ツリーに解析します。 ヘルパー関数`EvalToken`は、トークンを値に変換します。 ヘルパー関数`FindTerm`は、解析ツリーを再帰的に走査`EvalToken`し、値を表す各ノードを呼び出し、式に任意の操作 (加算または減算) を適用します。

```csharp
namespace EEMC
{
    public class CParsedExpression : IDebugParsedExpression
    {
        public HRESULT EvaluateSync(
            uint evalFlags,
            uint timeout,
            IDebugSymbolProvider provider,
            IDebugAddress address,
            IDebugBinder binder,
            string resultType,
            out IDebugProperty2 result)
        {
            HRESULT retval = COM.S_OK;
            this.evalFlags = evalFlags;
            this.timeout = timeout;
            this.provider = provider;
            this.address = address;
            this.binder = binder;
            this.resultType = resultType;

            try
            {
                IDebugField field = null;
                // Tokenize, then parse.
                tokens = Tokenize(expression);
                result = new CValueProperty(
                        expression,
                        (int) FindTerm(EvalToken(tokens[0], out field),1),
                        field,
                        binder);
            }
            catch (ParseException)
            {
                result = new CValueProperty(expression, "Huh?");
                retval = COM.E_INVALIDARG;
            }
            return retval;
        }
    }
}
```

## <a name="unmanaged-code"></a>アンマネージ コード
これは、アンマネージ コード`IDebugParsedExpression::EvaluateSync`の実装です。 ヘルパー関数`Evaluate`は、式を解析して評価し、結果の`VARIANT`値を保持する値を返します。 ヘルパー関数`VariantValueToProperty`は、 を`VARIANT`オブジェクトに`CValueProperty`バンドルします。

```cpp
STDMETHODIMP CParsedExpression::EvaluateSync(
    in  DWORD                 evalFlags,
    in  DWORD                 dwTimeout,
    in  IDebugSymbolProvider* pprovider,
    in  IDebugAddress*        paddress,
    in  IDebugBinder*         pbinder,
    in  BSTR                  bstrResultType,
    out IDebugProperty2**     ppproperty )
{
    // dwTimeout parameter is ignored in this implementation.
    if (pprovider == NULL)
        return E_INVALIDARG;

    if (paddress == NULL)
        return E_INVALIDARG;

    if (pbinder == NULL)
        return E_INVALIDARG;

    if (ppproperty == NULL)
        return E_INVALIDARG;
    else
        *ppproperty = 0;

    HRESULT hr;
    VARIANT value;
    BSTR    bstrErrorMessage = NULL;
    hr = ::Evaluate( pprovider,
                     paddress,
                     pbinder,
                     m_expr,
                     &bstrErrorMessage,
                     &value );
    if (hr != S_OK)
    {
        if (bstrErrorMessage == NULL)
            return hr;

        //we can display better messages ourselves.
        HRESULT hrLocal = S_OK;
        VARIANT varType;
        VARIANT varErrorMessage;

        VariantInit( &varType );
        VariantInit( &varErrorMessage );
        varErrorMessage.vt      = VT_BSTR;
        varErrorMessage.bstrVal = bstrErrorMessage;

        CValueProperty* valueProperty = new CValueProperty();
        if (valueProperty != NULL)
        {
            hrLocal = valueProperty->Init(m_expr, varType, varErrorMessage);
            if (SUCCEEDED(hrLocal))
            {
                hrLocal = valueProperty->QueryInterface( IID_IDebugProperty2,
                        reinterpret_cast<void**>(ppproperty) );
            }
        }

        VariantClear(&varType);
        VariantClear(&varErrorMessage); //frees BSTR
        if (!valueProperty)
            return hr;
        valueProperty->Release();
        if (FAILED(hrLocal))
            return hr;
    }
    else
    {
        if (bstrErrorMessage != NULL)
            SysFreeString(bstrErrorMessage);

        hr = VariantValueToProperty( pprovider,
                                     paddress,
                                     pbinder,
                                     m_radix,
                                     m_expr,
                                     value,
                                     ppproperty );
        VariantClear(&value);
        if (FAILED(hr))
            return hr;
    }

    return S_OK;
}
```

## <a name="see-also"></a>関連項目
- [ウォッチ ウィンドウ式を評価する](../../extensibility/debugger/evaluating-a-watch-window-expression.md)
- [式評価のサンプル実装](../../extensibility/debugger/sample-implementation-of-expression-evaluation.md)
