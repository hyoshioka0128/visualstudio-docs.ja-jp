---
title: 式評価の実装例 |マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80713098"
---
# <a name="sample-implementation-of-expression-evaluation"></a>式評価のサンプル実装
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターのこの実装方法は非推奨になりました。 CLR 式エバリュエーターの実装については[、「CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) 」および「[マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

 **ウォッチ**ウィンドウの式の場合は[、IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md)オブジェクトを生成する[ParseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)を呼び出します。 `IDebugExpressionContext2::ParseText`式エバリュエーター (EE) をインスタンス化し[、Parse](../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md)を呼び出して[IDebugParsedExpression](../../extensibility/debugger/reference/idebugparsedexpression.md)オブジェクトを取得します。

 は`IDebugExpressionEvaluator::Parse`、次のタスクを実行します。

1. [C++のみ]式を解析してエラーを探します。

2. インターフェイスを実行し、解析`CParsedExpression`する式をクラスに格納するクラス (この例で呼び出されるクラス) をインスタンス化します。 `IDebugParsedExpression`

3. オブジェクトから`IDebugParsedExpression`インターフェイスを`CParsedExpression`返します。

> [!NOTE]
> 次の例と MyCEE サンプルでは、式エバリュエーターは解析と評価を分離しません。

## <a name="managed-code"></a>マネージド コード
 次のコードは、マネージ`IDebugExpressionEvaluator::Parse`コードでの実装を示しています。 このバージョンのメソッドは、解析用のコードも同時に評価されるように[、解析を EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)に延期します ([ウォッチ式の評価を](../../extensibility/debugger/evaluating-a-watch-expression.md)参照)。

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
次のコードは、アンマネージ`IDebugExpressionEvaluator::Parse`コードの実装です。 このメソッドは、`Parse`ヘルパー関数 を呼び出して式を解析し、エラーをチェックしますが、このメソッドは結果の値を無視します。 正式な評価は[、評価](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)中に式が解析される EvaluateSync に延期されます (「[ウォッチ式の評価](../../extensibility/debugger/evaluating-a-watch-expression.md)」を参照)。

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
- [ウォッチ ウィンドウ式を評価する](../../extensibility/debugger/evaluating-a-watch-window-expression.md)
- [ウォッチ式を評価する](../../extensibility/debugger/evaluating-a-watch-expression.md)
