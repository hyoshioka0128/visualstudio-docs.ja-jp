---
title: ローカルプロパティの取得 |Microsoft Docs
description: マネージコードとアンマネージコードの例を使用して、Visual Studio が EnumChildren を使用してローカルプロパティを取得する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- expression evaluation, getting local properties
- debugging [Debugging SDK], local properties
- expression evaluation, local properties
ms.assetid: 6c3a79e8-1ba1-4863-97c3-0216c3d9f092
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 17b6d104f88999ba7dd8e115a752a78853af6603
ms.sourcegitcommit: bbed6a0b41ac4c4a24e8581ff3b34d96345ddb00
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2020
ms.locfileid: "96560019"
---
# <a name="get-local-properties"></a>ローカルプロパティの取得
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターを実装するこの方法は非推奨とされます。 CLR 式エバリュエーターの実装の詳細については、「 [clr 式](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) エバリュエーターと [マネージ式エバリュエーターサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

Visual Studio は、 [Enumchildren](../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)を呼び出して、[**ローカル**] ウィンドウに表示されるすべてのローカルへのアクセスを提供する [IEnumDebugPropertyInfo2](../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md)オブジェクトを取得します。 次に、Visual Studio は、[ [次へ](../../extensibility/debugger/reference/ienumdebugpropertyinfo2-next.md) ] を呼び出して、各ローカルに表示される情報を取得します。 この例では、クラスはインターフェイスを実装して `CEnumPropertyInfo` `IEnumDebugPropertyInfo2` います。

のこの実装で `IEnumDebugPropertyInfo2::Next` は、次のタスクを実行します。

1. 情報を格納する配列をクリアします。

2. 返される配列に返された[DEBUG_PROPERTY_INFO](../../extensibility/debugger/reference/debug-property-info.md)を格納して、各ローカルに対して[Next](../../extensibility/debugger/reference/ienumdebugfields-next.md)を呼び出します。 この[IEnumDebugFields](../../extensibility/debugger/reference/ienumdebugfields.md) `CEnumPropertyInfo` クラスがインスタンス化されたときに、IEnumDebugFields オブジェクトが指定されました。

## <a name="managed-code"></a>マネージド コード
この例では、 `IEnumDebugPropertyInfo2::EnumChildren` マネージコードでのメソッドのローカル変数のの実装を示します。

```csharp
namespace EEMC
{
    public class CEnumMethodField : IEnumDebugFields
    {
        public HRESULT Next(
                uint                  count,
                DEBUG_PROPERTY_INFO[] properties,
            out uint                  fetched)
        {
            if (count > properties.Length)
                throw new COMException();

            // Zero out the array.
            for (int i= 0; i < count; i++)
            {
                properties[i].bstrFullName = "";
                properties[i].bstrName = "";
                properties[i].bstrType = "";
                properties[i].bstrValue = "";
                properties[i].dwAttrib = 0;
                properties[i].dwFields = 0;
                properties[i].pProperty = null;
            }
            fetched = 0;

            // COM interop.
            HRESULT hr;
            uint innerFetched;
            IDebugField[] field = new IDebugField[1];

            while (fetched < count)
            {
                field[0] = null;
                innerFetched = 0;

                // Get next field.
                if (fetched < fieldCount)
                    hr = fields.Next(1, field, ref innerFetched);
                // No more fields.
                else return COM.S_FALSE;

                if (hr != COM.S_OK || innerFetched != 1 || field[0] == null)
                    throw new COMException("CEnumPropertyInfo.Next");

                // Get property from field.
                CFieldProperty fieldProperty =
                        new CFieldProperty(provider, address, binder, field[0]);

                DEBUG_PROPERTY_INFO[] property =
                        new DEBUG_PROPERTY_INFO[1];
                fieldProperty.GetPropertyInfo((uint) infoFlags, radix, 0, null, 0, property);
                properties[fetched++] = property[0];
            }
            return COM.S_OK;
        }
    }
}
```

## <a name="unmanaged-code"></a>アンマネージコード
 この例は、 `IEnumDebugPropertyInfo2::EnumChildren` アンマネージコード内のメソッドのローカルのの実装を示しています。

```cpp
STDMETHODIMP CEnumPropertyInfo::Next(
    in  ULONG                count,
    out DEBUG_PROPERTY_INFO* pelements,
    out ULONG*               pfetched )
{
    if (pfetched)
        *pfetched = 0;
    if (!pelements)
        return E_INVALIDARG;
    else
        memset( pelements, 0, count * sizeof(DEBUG_PROPERTY_INFO));

    HRESULT hr  = S_OK;
    ULONG   idx = 0;
    while (idx < count)
    {
        ULONG        fetchedFields;
        IDebugField* pfield;

        //get the next field
        hr = m_fields->Next( 1, &pfield, &fetchedFields );
        if (FAILED(hr))
            return hr;
        if (fetchedFields != 1)
            return E_FAIL;
        idx++;

        //create a CFieldProperty to retrieve the DEBUG_PROPERTY_INFO
        CFieldProperty* pproperty =
            new CFieldProperty( m_provider, m_address, m_binder, pfield );
        pfield->Release();
        if (!pproperty)
            return E_OUTOFMEMORY;

        hr = pproperty->Init();
        if (FAILED(hr))
        {
            pproperty->Release();
            return hr;
        }

        hr = pproperty->GetPropertyInfo( m_infoFlags,
                                         m_radix,
                                         0,
                                         NULL,
                                         0,
                                         pelements + idx - 1);
        pproperty->Release();
        if (FAILED(hr))
            return hr;
    }

    if (pfetched)
        *pfetched = idx;
    return hr;
}
```

## <a name="see-also"></a>関連項目
- [ローカルの実装のサンプル](../../extensibility/debugger/sample-implementation-of-locals.md)
- [ローカルの列挙](../../extensibility/debugger/enumerating-locals.md)
