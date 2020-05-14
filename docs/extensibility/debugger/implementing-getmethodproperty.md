---
title: プロパティを実装する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- GetMethodProperty method
- IDebugExpressionEvaluator2 property
ms.assetid: 6305874f-a2c4-4432-834c-07530ea84bff
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 252d09eee9c69ca75cb46d28dde807f2c500737f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738513"
---
# <a name="implement-getmethodproperty"></a>プロパティを実装します。
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターのこの実装方法は非推奨になりました。 CLR 式エバリュエーターの実装については[、「CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) 」および「[マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

デバッグ エンジン (DE)[を](../../extensibility/debugger/reference/idebugstackframe2-getdebugproperty.md)呼び出します。 [GetMethodProperty](../../extensibility/debugger/reference/idebugexpressionevaluator-getmethodproperty.md)

この実装は`IDebugExpressionEvaluator::GetMethodProperty`、次のタスクを実行します。

1. を[呼び](../../extensibility/debugger/reference/idebugsymbolprovider-getcontainerfield.md)出し、[オブジェクト](../../extensibility/debugger/reference/idebugaddress.md)を渡します。 シンボル プロバイダー (SP) は、指定されたアドレスを含むメソッドを表す[IDebugContainerField](../../extensibility/debugger/reference/idebugcontainerfield.md)を返します。

2. から[フィールドを](../../extensibility/debugger/reference/idebugmethodfield.md)取得します`IDebugContainerField`。

3. [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)インターフェイス`CFieldProperty`を実装し、SP から返される`IDebugMethodField`オブジェクトを含むクラス (この例で呼び出されます) をインスタンス化します。

4. オブジェクトから`IDebugProperty2`インターフェイスを`CFieldProperty`返します。

## <a name="managed-code"></a>マネージド コード
この例では、マネージ`IDebugExpressionEvaluator::GetMethodProperty`コードの実装を示します。

```csharp
namespace EEMC
{
    [GuidAttribute("462D4A3D-B257-4AEE-97CD-5918C7531757")]
    public class EEMCClass : IDebugExpressionEvaluator
    {
        public HRESULT GetMethodProperty(
                IDebugSymbolProvider symbolProvider,
                IDebugAddress        address,
                IDebugBinder         binder,
                int                  includeHiddenLocals,
            out IDebugProperty2      property)
        {
            IDebugContainerField containerField = null;
            IDebugMethodField methodField       = null;
            property = null;

            // Get the containing method field.
            symbolProvider.GetContainerField(address, out containerField);
            methodField = (IDebugMethodField) containerField;

            // Return the property of method field.
            property = new CFieldProperty(symbolProvider, address, binder, methodField);
            return COM.S_OK;
        }
    }
}
```

## <a name="unmanaged-code"></a>アンマネージ コード
この例では、アンマネージ`IDebugExpressionEvaluator::GetMethodProperty`コードの実装を示します。

```
[CPP]
STDMETHODIMP CExpressionEvaluator::GetMethodProperty(
        in IDebugSymbolProvider *pprovider,
        in IDebugAddress        *paddress,
        in IDebugBinder         *pbinder,
        in BOOL                  includeHiddenLocals,
        out IDebugProperty2    **ppproperty
    )
{
    if (pprovider == NULL)
        return E_INVALIDARG;

    if (ppproperty == NULL)
        return E_INVALIDARG;
    else
        *ppproperty = 0;

    HRESULT hr;
    IDebugContainerField* pcontainer = NULL;

    hr = pprovider->GetContainerField(paddress, &pcontainer);
    if (FAILED(hr))
        return hr;

    IDebugMethodField*    pmethod    = NULL;
    hr = pcontainer->QueryInterface( IID_IDebugMethodField,
            reinterpret_cast<void**>(&pmethod));
    pcontainer->Release();
    if (FAILED(hr))
        return hr;

    CFieldProperty* pfieldProperty = new CFieldProperty( pprovider,
                                                         paddress,
                                                         pbinder,
                                                         pmethod );
    pmethod->Release();
    if (!pfieldProperty)
        return E_OUTOFMEMORY;

    hr = pfieldProperty->Init();
    if (FAILED(hr))
    {
        pfieldProperty->Release();
        return hr;
    }

    hr = pfieldProperty->QueryInterface( IID_IDebugProperty2,
            reinterpret_cast<void**>(ppproperty));
    pfieldProperty->Release();

    return hr;
}
```

## <a name="see-also"></a>関連項目
- [ローカルのサンプル実装](../../extensibility/debugger/sample-implementation-of-locals.md)
