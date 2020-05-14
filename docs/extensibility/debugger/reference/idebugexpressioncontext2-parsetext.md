---
title: Iデバッグエクスプレッションコンテキスト2::Pテキストを意味します。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExpressionContext2::ParseText
helpviewer_keywords:
- IDebugExpressionContext2::ParseText
ms.assetid: f58575db-f926-4ac8-83ff-7b3b86ab61e2
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a8494c9c90c4cb6e94115c542a25e12e948f7064
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80729653"
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
[in]解析する式。

`dwFlags`\
[in]解析を制御する[PARSEFLAGS](../../../extensibility/debugger/reference/parseflags.md)列挙体のフラグの組み合わせ。

`nRadix`\
[in]の数値情報の解析に使用される基数`pszCode`。

`ppExpr`\
[アウト]バインディングと評価の準備が整った、解析された式を表す[IDebugExpression2](../../../extensibility/debugger/reference/idebugexpression2.md)オブジェクトを返します。

`pbstrError`\
[アウト]式にエラーが含まれている場合は、エラー メッセージを返します。

`pichError`\
[アウト]式にエラーが含まれている場合に`pszCode`、 でエラーの文字インデックスを返します。

## <a name="return-value"></a>戻り値
成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
このメソッドが呼び出されると、デバッグ エンジン (DE) は式を解析し、正しいかどうかを検証する必要があります。 式`pbstrError`が`pichError`無効な場合は、 および パラメーターを入力できます。

式は評価されず、解析されるだけであることに注意してください。 後で呼び出す[、EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)メソッドまたは[EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)メソッドは、解析された式を評価します。

## <a name="example"></a>例
次の例は[、IDebugExpressionContext2](../../../extensibility/debugger/reference/idebugexpressioncontext2.md)インターフェイス`CEnvBlock`を公開する単純なオブジェクトに対してこのメソッドを実装する方法を示しています。 この例では、解析する式を環境変数の名前として検討し、その変数から値を取得します。

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
