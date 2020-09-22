---
title: ウォッチ式の評価 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- expression evaluation, watch expressions
- watch expressions
ms.assetid: 8317cd52-6fea-4e8f-a739-774dc06bd44b
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: fd33a7c225e0cdc14ac3f1af9f4c78a7c1459615
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841428"
---
# <a name="evaluating-a-watch-expression"></a>ウォッチ式の評価
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターを実装するこの方法は非推奨とされます。 CLR 式エバリュエーターの実装の詳細については、「 [Clr 式](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) エバリュエーターと [マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。  
  
 Visual Studio でウォッチ式の値を表示する準備が整うと、 [EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) が呼び出され、 [EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)が呼び出されます。 これにより、式の値と型を含む [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) オブジェクトが生成されます。  
  
 のこの実装では、 `IDebugParsedExpression::EvaluateSync` 式が解析され、同時に評価されます。 この実装では、次のタスクを実行します。  
  
1. 式を解析して評価し、値とその型を保持する汎用オブジェクトを生成します。 C# では、これはとして、C++ ではとして表され `object` ます。これは、として表され `VARIANT` ます。  
  
2. `CValueProperty`インターフェイスを実装 `IDebugProperty2` し、返される値をクラスに格納するクラス (この例ではと呼ばれる) をインスタンス化します。  
  
3. `IDebugProperty2`オブジェクトからインターフェイスを返し `CValueProperty` ます。  
  
## <a name="managed-code"></a>マネージド コード  
 これは、マネージコードでのの実装です `IDebugParsedExpression::EvaluateSync` 。 ヘルパーメソッドは、 `Tokenize` 式を解析ツリーに解析します。 ヘルパー関数は、 `EvalToken` トークンを値に変換します。 ヘルパー関数は、 `FindTerm` 解析ツリーを再帰的に走査し、 `EvalToken` 値を表す各ノードに対してを呼び出し、式に任意の操作 (加算または減算) を適用します。  
  
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
 これは、 `IDebugParsedExpression::EvaluateSync` アンマネージコードでのの実装です。 ヘルパー関数は、 `Evaluate` 式を解析して評価し、 `VARIANT` 結果の値を保持するを返します。 ヘルパー関数は `VariantValueToProperty` 、を `VARIANT` オブジェクトにバンドルし `CValueProperty` ます。  
  
```  
[C++]  
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
  
## <a name="see-also"></a>参照  
 [ウォッチウィンドウの式の評価](../../extensibility/debugger/evaluating-a-watch-window-expression.md)   
 [式の評価の実装のサンプル](../../extensibility/debugger/sample-implementation-of-expression-evaluation.md)
