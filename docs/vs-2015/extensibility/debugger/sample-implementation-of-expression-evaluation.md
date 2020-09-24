---
title: 式の評価の実装例 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- expression evaluators
- debugging [Debugging SDK], expression evaluators
- expression evaluation, examples
ms.assetid: 2a5f04b8-6c65-4232-bddd-9093653a22c4
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a7a19247b296d7e00a15051e75dd53536133c426
ms.sourcegitcommit: bccc6503542e1517e0e96a9f02f5a89d69c60c25
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/24/2020
ms.locfileid: "91147240"
---
# <a name="sample-implementation-of-expression-evaluation"></a>式の評価の実装のサンプル
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターを実装するこの方法は非推奨とされます。 CLR 式エバリュエーターの実装の詳細については、「 [Clr 式](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) エバリュエーターと [マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。  
  
 **ウォッチ**ウィンドウ式の場合、Visual Studio は[parsetext](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)を呼び出して、 [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md)オブジェクトを生成します。 `IDebugExpressionContext2::ParseText` 式エバリュエーター (EE) をインスタンス化し、 [Parse](../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md) を呼び出して [IDebugParsedExpression](../../extensibility/debugger/reference/idebugparsedexpression.md) オブジェクトを取得します。  
  
 のこの実装で `IDebugExpressionEvaluator::Parse` は、次のタスクを実行します。  
  
1. [C++ のみ]式を解析してエラーを探します。  
  
2. `CParsedExpression`インターフェイスを実装 `IDebugParsedExpression` し、解析する式をクラスに格納するクラス (この例ではと呼ばれる) をインスタンス化します。  
  
3. `IDebugParsedExpression`オブジェクトからインターフェイスを返し `CParsedExpression` ます。  
  
> [!NOTE]
> 次に示す MyCEE サンプルの例では、式エバリュエーターが評価から解析を分離していません。  
  
## <a name="managed-code"></a>マネージド コード  
 これは、マネージコードでのの実装です `IDebugExpressionEvaluator::Parse` 。 このバージョンのメソッドは、解析用のコードも同時に評価されるため、 [EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md) への解析を延期することに注意してください (「 [ウォッチ式の評価](../../extensibility/debugger/evaluating-a-watch-expression.md)」を参照してください)。  
  
```csharp  
namespace EEMC  
{  
    public class CParsedExpression : IDebugParsedExpression  
    {  
        public HRESULT Parse(  
                string                 expression,   
                uint                   parseFlags,  
                uint                   radix,  
            out string                 errorMessage,   
            out uint                   errorPosition,   
            out IDebugParsedExpression parsedExpression)  
        {   
            errorMessage = "";  
            errorPosition = 0;  
  
            parsedExpression =  
                new CParsedExpression(parseFlags, radix, expression);  
            return COM.S_OK;  
        }  
    }  
}  
```  
  
## <a name="unmanaged-code"></a>アンマネージ コード  
 これは、 `IDebugExpressionEvaluator::Parse` アンマネージコードでのの実装です。 このメソッドは、ヘルパー関数を呼び出し `Parse` て、式を解析し、エラーをチェックしますが、このメソッドは結果の値を無視します。 正式な評価は、評価時に式が解析される [EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md) に遅延されます (「 [ウォッチ式の評価](../../extensibility/debugger/evaluating-a-watch-expression.md)」を参照してください)。  
  
```cpp#  
STDMETHODIMP CExpressionEvaluator::Parse(  
        in    LPCOLESTR                 pszExpression,  
        in    PARSEFLAGS                flags,  
        in    UINT                      radix,  
        out   BSTR                     *pbstrErrorMessages,  
        inout UINT                     *perrorCount,  
        out   IDebugParsedExpression  **ppparsedExpression  
    )  
{  
    if (pbstrErrorMessages == NULL)  
        return E_INVALIDARG;  
    else  
        *pbstrErrormessages = 0;  
  
    if (pparsedExpression == NULL)  
        return E_INVALIDARG;  
    else  
        *pparsedExpression = 0;  
  
    if (perrorCount == NULL)  
        return E_INVALIDARG;  
  
    HRESULT hr;  
    // Look for errors in the expression but ignore results  
    hr = ::Parse( pszExpression, pbstrErrorMessages );  
    if (hr != S_OK)  
        return hr;  
  
    CParsedExpression* pparsedExpr = new CParsedExpression( radix, flags, pszExpression );  
    if (!pparsedExpr)  
        return E_OUTOFMEMORY;  
  
    hr = pparsedExpr->QueryInterface( IID_IDebugParsedExpression,  
                                      reinterpret_cast<void**>(ppparsedExpression) );  
    pparsedExpr->Release();  
  
    return hr;  
}  
```  
  
## <a name="see-also"></a>関連項目  
 [ウォッチウィンドウの式の評価](../../extensibility/debugger/evaluating-a-watch-window-expression.md)   
 [ウォッチ式の評価](../../extensibility/debugger/evaluating-a-watch-expression.md)
