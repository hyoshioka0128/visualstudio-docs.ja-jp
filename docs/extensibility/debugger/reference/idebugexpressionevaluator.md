---
title: Iデバッグ式エバリュエーター |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExpressionEvaluator
helpviewer_keywords:
- IDebugExpressionEvaluator interface
ms.assetid: 0636d8c3-625a-49fa-94b6-516f22b7e1bc
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7e8dd910e4edc110abb40dde14b4cb85ff54a70a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80729375"
---
# <a name="idebugexpressionevaluator"></a>IDebugExpressionEvaluator
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターのこの実装方法は非推奨になりました。 CLR 式エバリュエーターの実装については、「 [CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)と[マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

このインターフェイスは、式エバリュエーターを表します。

## <a name="syntax"></a>構文

```
IDebugExpressionEvaluator : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
式エバリュエーターはこのインターフェイスを実装する必要があります。

## <a name="notes-for-callers"></a>発信者向けのメモ
このインターフェイスを取得するには、エバリュエーターの`CoCreateInstance`クラス ID (CLSID) を使用してメソッドを使用して式エバリュエーターをインスタンス化します。 例を参照してください。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
次の表に`IDebugExpressionEvaluator`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[解析](../../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md)|式文字列を解析された式に変換します。|
|[GetMethodProperty](../../../extensibility/debugger/reference/idebugexpressionevaluator-getmethodproperty.md)|メソッドのローカル変数、引数、およびその他のプロパティを取得します。|
|[GetMethodLocationProperty](../../../extensibility/debugger/reference/idebugexpressionevaluator-getmethodlocationproperty.md)|メソッドの場所とオフセットをメモリ アドレスに変換します。|
|[SetLocale](../../../extensibility/debugger/reference/idebugexpressionevaluator-setlocale.md)|印刷可能な結果を作成するために使用する言語を決定します。|
|[SetRegistryRoot](../../../extensibility/debugger/reference/idebugexpressionevaluator-setregistryroot.md)|レジストリ ルートを設定します。 サイド バイ サイド デバッグに使用されます。|

## <a name="remarks"></a>Remarks
一般的な状況では、デバッグ エンジン (DE) は、式エバリュエーター (EE) を[ParseText](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)の呼び出しの結果としてインスタンス化します。 DE は使用する EE の言語とベンダーを知っているので、DE はレジストリから EE の CLSID を取得します[(SDK のヘルパー](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)関数は、`GetEEMetric`この取得に役立ちます)。

EE がインスタンス化された後、DE は[、式を解析](../../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md)し[、IDebugParsedExpression](../../../extensibility/debugger/reference/idebugparsedexpression.md)オブジェクトに格納する Parse を呼び出します。 後で[、EvaluateSync](../../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)の呼び出しは式を評価します。

## <a name="requirements"></a>必要条件
ヘッダー: ee.h

名前空間: を使用します。

アセンブリ:

## <a name="example"></a>例
この例では、ソース コード内のシンボル プロバイダーとアドレスを指定して、式エバリュエーターをインスタンス化する方法を示します。 この例では、`GetEEMetric`デバッグ ライブラリ dbgmetric.lib の SDK[ヘルパー](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)の関数を使用しています。

```cpp
IDebugExpressionEvaluator GetExpressionEvaluator(IDebugSymbolProvider pSymbolProvider,
                                                 IDebugAddress *pSourceAddress)
{
    // This is typically defined globally but is specified here just
    // for this example.
    static const WCHAR strRegistrationRoot[] = L"Software\\Microsoft\\VisualStudio\\8.0Exp";

    IDebugExpressionEvaluator *pEE = NULL;
    if (pSymbolProvider != NULL && pSourceAddress != NULL) {
        HRESULT hr         = S_OK;
        GUID  languageGuid = { 0 };
        GUID  vendorGuid   = { 0 };

        hr = pSymbolProvider->GetLanguage(pSourceAddress,
                                          &languageGuid,
                                          &vendorGuid);
        if (SUCCEEDED(hr)) {
            CLSID clsidEE = { 0 };
            CComPtr<IDebugExpressionEvaluator> spExpressionEvaluator;
            // Get the expression evaluator's CLSID from the registry.
            ::GetEEMetric(languageGuid,
                          vendorGuid,
                          metricCLSID,
                          &clsidEE,
                          strRegistrationRoot);
            if (!IsEqualGUID(clsidEE,GUID_NULL)) {
                // Instantiate the expression evaluator.
                spExpressionEvaluator.CoCreateInstance(clsidEE);
            }
            if (spExpressionEvaluator != NULL) {
                pEE = spExpressionEvaluator.Detach();
            }
        }
    }
    return pEE;
}
```

## <a name="see-also"></a>関連項目
- [式の評価のインターフェイス](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [ParseText](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)
- [IDebugParsedExpression](../../../extensibility/debugger/reference/idebugparsedexpression.md)
- [EvaluateSync](../../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)
- [デバッグ用の SDK ヘルパー](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)
