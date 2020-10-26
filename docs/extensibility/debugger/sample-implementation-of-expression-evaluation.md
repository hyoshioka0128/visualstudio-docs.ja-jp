---
title: 式の評価の実装例 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- expression evaluators
- debugging [Debugging SDK], expression evaluators
- expression evaluation, examples
ms.assetid: 2a5f04b8-6c65-4232-bddd-9093653a22c4
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: cf994a61ed9283463cd01aa468018f6acce5e209
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80713098"
---
# <a name="sample-implementation-of-expression-evaluation"></a>式の評価の実装例
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターを実装するこの方法は非推奨とされます。 CLR 式エバリュエーターの実装の詳細については、「 [clr 式](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) エバリュエーターと [マネージ式エバリュエーターサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

 **ウォッチ**ウィンドウ式の場合、Visual Studio は[parsetext](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)を呼び出して、 [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md)オブジェクトを生成します。 `IDebugExpressionContext2::ParseText` 式エバリュエーター (EE) をインスタンス化し、 [Parse](../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md) を呼び出して [IDebugParsedExpression](../../extensibility/debugger/reference/idebugparsedexpression.md) オブジェクトを取得します。

 は、 `IDebugExpressionEvaluator::Parse` 次のタスクを実行します。

1. [C++ のみ]式を解析してエラーを探します。

2. `CParsedExpression`インターフェイスを実行 `IDebugParsedExpression` し、解析する式をクラスに格納するクラス (この例ではと呼ばれる) をインスタンス化します。

3. `IDebugParsedExpression`オブジェクトからインターフェイスを返し `CParsedExpression` ます。

> [!NOTE]
> 次に示す MyCEE サンプルの例では、式エバリュエーターが評価から解析を分離していません。

## <a name="managed-code"></a>マネージド コード
 次のコードは、マネージコードでのの実装を示して `IDebugExpressionEvaluator::Parse` います。 このバージョンのメソッドは、解析用のコードも同時に評価されるため、解析を [EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md) に延期します (「 [ウォッチ式の評価](../../extensibility/debugger/evaluating-a-watch-expression.md)」を参照してください)。

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

## <a name="unmanaged-code"></a>アンマネージコード
次のコードは、 `IDebugExpressionEvaluator::Parse` アンマネージコードでのの実装です。 このメソッドは、ヘルパー関数を呼び出し `Parse` て、式を解析し、エラーをチェックしますが、このメソッドは結果の値を無視します。 正式な評価は、評価時に式が解析される [EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md) に遅延されます (「 [ウォッチ式の評価](../../extensibility/debugger/evaluating-a-watch-expression.md)」を参照してください)。

```cpp
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
- [ウォッチウィンドウ式の評価](../../extensibility/debugger/evaluating-a-watch-window-expression.md)
- [ウォッチ式の評価](../../extensibility/debugger/evaluating-a-watch-expression.md)
