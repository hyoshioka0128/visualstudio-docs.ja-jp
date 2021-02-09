---
title: IDebugExpressionContext2::P arseText |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExpressionContext2::ParseText
helpviewer_keywords:
- IDebugExpressionContext2::ParseText
ms.assetid: f58575db-f926-4ac8-83ff-7b3b86ab61e2
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: fc55cceb8db392d590ff414ac3df5b807d1e52e0
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99901638"
---
# <a name="idebugexpressioncontext2parsetext"></a>IDebugExpressionContext2::ParseText
後で評価するために、テキスト形式の式を解析します。

## <a name="syntax"></a>構文

```cpp
HRESULT ParseText(
    LPCOLESTR           pszCode,
    PARSEFLAGS          dwFlags,
    UINT                nRadix,
    IDebugExpression2** ppExpr,
    BSTR*               pbstrError,
    UINT*               pichError
);
```

```csharp
int ParseText(
    string                pszCode,
    enum_PARSEFLAGS       dwFlags,
    uint                  nRadix,
    out IDebugExpression2 ppExpr,
    out string            pbstrError,
    out uint              pichError
);
```

## <a name="parameters"></a>パラメーター
`pszCode`\
から解析する式。

`dwFlags`\
から解析を制御する [parseflags](../../../extensibility/debugger/reference/parseflags.md) 列挙のフラグの組み合わせ。

`nRadix`\
からの数値情報の解析に使用される基数 `pszCode` 。

`ppExpr`\
入出力解析された式を表す [IDebugExpression2](../../../extensibility/debugger/reference/idebugexpression2.md) オブジェクトを返します。このオブジェクトは、バインドおよび評価の準備ができています。

`pbstrError`\
入出力式にエラーが含まれている場合は、エラーメッセージを返します。

`pichError`\
入出力 `pszCode` 式にエラーが含まれている場合は、エラーの文字インデックスを返します。

## <a name="return-value"></a>戻り値
成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
このメソッドが呼び出されると、デバッグエンジン (DE) は、式を解析して、正しいかどうかを検証する必要があります。 `pbstrError` `pichError` 式が無効な場合は、パラメーターとパラメーターを入力できます。

式は評価されず、解析のみが行われることに注意してください。 後で [EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) または [evaluateasync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md) メソッドを呼び出すと、解析された式が評価されます。

## <a name="example"></a>例
次の例は、IDebugExpressionContext2 インターフェイスを公開する単純なオブジェクトに対してこのメソッドを実装する方法を示して `CEnvBlock` います。 [](../../../extensibility/debugger/reference/idebugexpressioncontext2.md) この例では、式を環境変数の名前として解析し、その変数から値を取得します。

```cpp
HRESULT CEnvBlock::ParseText(
    LPCOLESTR           pszCode,
    PARSEFLAGS          dwFlags,
    UINT                nRadix,
    IDebugExpression2 **ppExpr,
    BSTR               *pbstrError,
    UINT               *pichError)
{
    HRESULT hr = E_OUTOFMEMORY;
    // Create an integer variable with a value equal to one plus
    // twice the length of the passed expression to be parsed.
    int iAnsiLen      = 2 * (wcslen(pszCode)) + 1;
    // Allocate a character string of the same length.
    char *pszAnsiCode = (char *) malloc(iAnsiLen);

    // Check for successful memory allocation.
    if (pszAnsiCode) {
        // Map the wide-character pszCode string to the new pszAnsiCode character string.
        WideCharToMultiByte(CP_ACP, 0, pszCode, -1, pszAnsiCode, iAnsiLen, NULL, NULL);
        // Check to see if the app can succesfully get the environment variable.
        if (GetEnv(pszAnsiCode)) {

            // Create and initialize a CExpression object.
            CComObject<CExpression> *pExpr;
            CComObject<CExpression>::CreateInstance(&pExpr);
            pExpr->Init(pszAnsiCode, this, NULL);

            // Assign the pointer to the new object to the passed argument
            // and AddRef the object.
            *ppExpr = pExpr;
            (*ppExpr)->AddRef();
            hr = S_OK;
        // If the program cannot succesfully get the environment variable.
        } else {
            // Set the errror message and return E_FAIL.
            *pbstrError = SysAllocString(L"No such environment variable.");
            hr = E_FAIL;
        }
        // Free the local character string.
        free(pszAnsiCode);
    }
    return hr;
}
```

## <a name="see-also"></a>関連項目
- [IDebugExpressionContext2](../../../extensibility/debugger/reference/idebugexpressioncontext2.md)
- [PARSEFLAGS](../../../extensibility/debugger/reference/parseflags.md)
- [IDebugExpression2](../../../extensibility/debugger/reference/idebugexpression2.md)
- [EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)
- [EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)
