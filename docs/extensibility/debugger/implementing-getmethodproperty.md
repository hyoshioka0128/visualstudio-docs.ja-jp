---
title: GetMethodProperty | を実装するMicrosoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80738513"
---
# <a name="implement-getmethodproperty"></a>GetMethodProperty を実装する
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターを実装するこの方法は非推奨とされます。 CLR 式エバリュエーターの実装の詳細については、「 [clr 式](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) エバリュエーターと [マネージ式エバリュエーターサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

Visual Studio は、デバッグエンジンの (DE) [Getdebugproperty](../../extensibility/debugger/reference/idebugstackframe2-getdebugproperty.md)を呼び出します。このプロパティは [getdebugproperty](../../extensibility/debugger/reference/idebugexpressionevaluator-getmethodproperty.md) を呼び出して、スタックフレームの現在のメソッドに関する情報を取得します。

のこの実装で `IDebugExpressionEvaluator::GetMethodProperty` は、次のタスクを実行します。

1. [GetContainerField](../../extensibility/debugger/reference/idebugsymbolprovider-getcontainerfield.md)を呼び出し、 [IDebugAddress](../../extensibility/debugger/reference/idebugaddress.md)オブジェクトを渡します。 シンボルプロバイダー (SP) は、指定されたアドレスを含むメソッドを表す [IDebugContainerField](../../extensibility/debugger/reference/idebugcontainerfield.md) を返します。

2. から [IDebugMethodField](../../extensibility/debugger/reference/idebugmethodfield.md) を取得し `IDebugContainerField` ます。

3. `CFieldProperty` [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)インターフェイスを実装し、 `IDebugMethodField` SP から返されたオブジェクトを格納するクラス (この例ではと呼ばれます) をインスタンス化します。

4. `IDebugProperty2`オブジェクトからインターフェイスを返し `CFieldProperty` ます。

## <a name="managed-code"></a>マネージド コード
この例は、マネージコードでのの実装を示して `IDebugExpressionEvaluator::GetMethodProperty` います。

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

## <a name="unmanaged-code"></a>アンマネージコード
この例は、アンマネージコードでのの実装を示して `IDebugExpressionEvaluator::GetMethodProperty` います。

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
- [ローカルの実装のサンプル](../../extensibility/debugger/sample-implementation-of-locals.md)
