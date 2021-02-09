---
title: ローカル値の取得 |Microsoft Docs
description: マネージコードとアンマネージコードの GetPropertyInfo を使用して、Visual Studio がローカル変数の値を取得する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- expression evaluation, local values
- debugging [Debugging SDK], local values
- expression evaluation, getting local values
ms.assetid: a10b0764-65ac-476f-bf42-b4a9c38e20de
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 64b3d4876622aabc831c0142a041964aa8dfe807
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99921261"
---
# <a name="get-local-values"></a>ローカル値の取得
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターを実装するこの方法は非推奨とされます。 CLR 式エバリュエーターの実装の詳細については、「 [clr 式](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) エバリュエーターと [マネージ式エバリュエーターサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

ローカルのの値を取得するために、Visual Studio はそのローカルの [GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md) を呼び出します。 この実装では、クラスは、 `CFieldProperty` 各ローカルの IDebugProperty2 インターフェイスを実装します。

のこの実装で `IDebugProperty2::GetPropertyInfo` は、次のタスクを実行します。

1. クラスのインスタンス化および初期化時に入力された [FIELD_INFO](../../extensibility/debugger/reference/field-info.md) 構造体から、ローカルの名前、プロパティ、および属性を取得します。

2. [IDebugField](../../extensibility/debugger/reference/idebugfield.md)オブジェクトからローカルの型を取得します。

3. オブジェクトからローカルの値を取得し `IDebugField` ます。 このフィールドは、 [IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md) オブジェクトを使用してローカルのメモリ位置にバインドされ、結果として得られる [IDebugObject](../../extensibility/debugger/reference/idebugobject.md) オブジェクトから値が取得されます。

4. [DEBUG_PROPERTY_INFO](../../extensibility/debugger/reference/debug-property-info.md)構造体で、要求されたすべてのプロパティを返します。

## <a name="managed-code"></a>マネージド コード
この例は、 `IDebugProperty2::GetPropertyInfo` マネージコードでのメソッドのローカルのの実装を示しています。 また、 `Field.GetType` フィールドの型を取得するために使用されるヘルパー関数も示しています。 `Field.GetValue` は、[ [ローカルの評価](../../extensibility/debugger/evaluating-locals.md)] に表示されます。 ヘルパー関数 `Field.MapModifiersToAttributes` (示されていません) は、フィールドの [FIELD_MODIFIERS](../../extensibility/debugger/reference/field-modifiers.md) フラグを [DBG_ATTRIB_FLAGS](../../extensibility/debugger/reference/dbg-attrib-flags.md) の値に変換するだけです。

```csharp
namespace EEMC
{
    public class CFieldProperty : IDebugProperty2
    {
        public HRESULT GetPropertyInfo(
            uint                  dwFields,
            uint                  radix,
            uint                  timeout,
            IDebugReference2[]    refArgs,
            uint                  argCount,
            DEBUG_PROPERTY_INFO[] infoArray)
        {
            DEBUGPROP_INFO_FLAGS flags = (DEBUGPROP_INFO_FLAGS) dwFields;
            DEBUGPROP_INFO_FLAGS infoFields = DEBUGPROP_INFO_FLAGS.DEBUGPROP_INFO_NONE;

            // Initialize the structure.
            DEBUG_PROPERTY_INFO info = infoArray[0];
            info.pProperty = null;

            // Fill in the full name, if requested.
            if (0 != (flags & DEBUGPROP_INFO_FLAGS.DEBUGPROP_INFO_FULLNAME))
            {
                info.bstrFullName = fieldInfo.bstrFullName;
                infoFields |= DEBUGPROP_INFO_FLAGS.DEBUGPROP_INFO_FULLNAME;
            }
            // Fill in the name, if requested.
            if (0 != (flags & DEBUGPROP_INFO_FLAGS.DEBUGPROP_INFO_NAME))
            {
                info.bstrName = fieldInfo.bstrName;
                infoFields |= DEBUGPROP_INFO_FLAGS.DEBUGPROP_INFO_NAME;
            }
            // Fill in the type, if requested.
            if (0 != (flags & DEBUGPROP_INFO_FLAGS.DEBUGPROP_INFO_TYPE))
            {
                if (fieldType == null)
                    fieldType = Field.GetType(field, out fieldSize);
                if (fieldType == null)
                    info.bstrType = "unknown";
                else
                    info.bstrType = fieldType.ToString();
                infoFields |= DEBUGPROP_INFO_FLAGS.DEBUGPROP_INFO_TYPE;
            }
            // The property associated with this property is this property.
            if (0 != (flags & DEBUGPROP_INFO_FLAGS.DEBUGPROP_INFO_PROP))
            {
                info.pProperty = this;
                infoFields |= DEBUGPROP_INFO_FLAGS.DEBUGPROP_INFO_PROP;
            }
            // Get the property value, if requested.
            if (0 != (flags & DEBUGPROP_INFO_FLAGS.DEBUGPROP_INFO_VALUE))
            {
                if (fieldType == null)
                    fieldType = Field.GetType(field, out fieldSize);
                if (fieldType == null)
                    info.bstrValue = "?";
                else
                {
                    object o = Field.GetValue(binder, field, fieldType, fieldSize);
                    if (o == null)
                        info.bstrValue = "?";
                    else
                        info.bstrValue = o.ToString();
                }
                infoFields |= DEBUGPROP_INFO_FLAGS.DEBUGPROP_INFO_VALUE;
            }
            // Get the property attributes, if requested.
            if (0 != (flags & DEBUGPROP_INFO_FLAGS.DEBUGPROP_INFO_ATTRIB))
            {
                info.dwAttrib =
                    (ulong) Field.MapModifiersToAttributes(
                        (FIELD_MODIFIERS) fieldInfo.dwModifiers,
                        fieldKind);
                infoFields |= DEBUGPROP_INFO_FLAGS.DEBUGPROP_INFO_ATTRIB;
            }
            info.dwFields = (uint) infoFields;
            infoArray[0] = info;
            return COM.S_OK;
        }
    }

//----------------------------------------------------------------------------

    internal class Field
    {
        internal static Type GetType(IDebugField field, out uint size)
        {
            size = 0;

            IDebugField fieldType = null;
            field.GetType(out fieldType);
            if (fieldType == null)  return null;

            // Get field size.
            fieldType.GetSize(out size);

            // Get approximate type name.
            FIELD_INFO[] fieldTypeInfo = new FIELD_INFO[1];
            fieldType.GetInfo((uint) FIELD_INFO_FIELDS.FIF_NAME,
                fieldTypeInfo);

            // Map approximate name to type name.
            switch (fieldTypeInfo[0].bstrName)
            {
                case "whole":
                switch (size)
                {
                    case 1: return typeof(sbyte);
                    case 2: return typeof(short);
                    case 4: return typeof(int);
                    case 8: return typeof(long);
                }
                    break;
                case "uwhole":
                switch (size)
                {
                    case 1: return typeof(byte);
                    case 2: return typeof(char);
                    case 4: return typeof(uint);
                    case 8: return typeof(ulong);
                }
                    break;
                case "real":
                switch (size)
                {
                    case 4: return typeof(float);
                    case 8: return typeof(double);
                }
                    break;
                case "bool": return typeof(bool);
                case "string": return typeof(string);
            }
            return null;
        }
}
```

## <a name="unmanaged-code"></a>アンマネージコード
 この例は、アンマネージコード内のメソッドのローカルのの実装を示し `IDebugProperty2::GetPropertyInfo` ています。 また、2つのヘルパー関数 `FieldGetType` と、 `FieldGetValue` フィールドの型と値を取得するために使用されるを示します。 は、 `VARIANT` フィールドの値および型として使用され、さまざまな `VARIANT` 値型を処理できます。 この実装では、は後での `FieldGetValue` 呼び出しの値に変換される [IDebugField](../../extensibility/debugger/reference/idebugfield.md) オブジェクトを返し `FieldGetPrimitiveValue` ます (「 [ローカルの評価](../../extensibility/debugger/evaluating-locals.md)」を参照)。

```cpp
STDMETHODIMP CFieldProperty::GetPropertyInfo(
    in  DEBUGPROP_INFO_FLAGS infoFlags,
    in  DWORD                radix,
    in  DWORD                timeout,
    in  IDebugReference2**   ppargs,
    in  DWORD                argCount,
    out DEBUG_PROPERTY_INFO* ppropertyInfo
    )
{
    if (!ppropertyInfo)
        return E_INVALIDARG;
    else
        memset(ppropertyInfo,0,sizeof(*ppropertyInfo));

    if (infoFlags & DEBUGPROP_INFO_FULLNAME)
    {
        ppropertyInfo->dwFields |= DEBUGPROP_INFO_FULLNAME;
        ppropertyInfo->bstrFullName = SysAllocString( m_fieldInfo.bstrFullName );
    }

    if (infoFlags & DEBUGPROP_INFO_NAME)
    {
        ppropertyInfo->dwFields |= DEBUGPROP_INFO_NAME;
        ppropertyInfo->bstrName  = SysAllocString( m_fieldInfo.bstrName );
    }

    if (infoFlags & DEBUGPROP_INFO_TYPE)
    {
        ppropertyInfo->dwFields |= DEBUGPROP_INFO_TYPE;

        VARIANT type;
        if (SUCCEEDED(FieldGetType( m_field, &type )))
        {
            // Convert the variant's type to a string
            VariantTypeToString( type, &(ppropertyInfo->bstrType) );
            VariantClear(&type);

        }
        if (ppropertyInfo->bstrType == NULL)
            ppropertyInfo->bstrType = SysAllocString( GetString(IDS_MSG_UNKNOWNTYPE) );
    }

    if (infoFlags & DEBUGPROP_INFO_PROP)
    {
        ppropertyInfo->dwFields |= DEBUGPROP_INFO_PROP;
        QueryInterface( IID_IDebugProperty2,
                        reinterpret_cast<void**>(&(ppropertyInfo->pProperty)) );
    }

    if (infoFlags & DEBUGPROP_INFO_VALUE)
    {
        ppropertyInfo->dwFields |= DEBUGPROP_INFO_VALUE;

        //only show primitive values
        VARIANT value;
        if (SUCCEEDED(FieldGetValue(m_field, &value)))
        {
            VariantValueToString( radix, m_binder, value,
                                  &(ppropertyInfo->bstrValue) );
            VariantClear(&value);
        }

        if (ppropertyInfo->bstrValue == NULL)
            ppropertyInfo->bstrValue = SysAllocString( GetString(IDS_MSG_UNKNOWNVALUE) );
    }

    if (infoFlags & DEBUGPROP_INFO_VALUE_AUTOEXPAND)
    {
    // AUTOEXPAND is ignored in this example
    }

    if (infoFlags & DEBUGPROP_INFO_ATTRIB)
    {
        ppropertyInfo->dwFields |= DEBUGPROP_INFO_ATTRIB;

        FIELD_MODIFIERS   modifiers = m_fieldInfo.dwModifiers;
        DBG_ATTRIB_FLAGS  attrib    = DBG_ATTRIB_NONE;

        //access
        if (modifiers & FIELD_MOD_ACCESS_PUBLIC)
            attrib |= DBG_ATTRIB_ACCESS_PUBLIC;
        if (modifiers & FIELD_MOD_ACCESS_PRIVATE)
            attrib |= DBG_ATTRIB_ACCESS_PRIVATE;
        if (modifiers & FIELD_MOD_ACCESS_PROTECTED)
            attrib |= DBG_ATTRIB_ACCESS_PROTECTED;
        if (modifiers & FIELD_MOD_FINAL)
            attrib |= DBG_ATTRIB_ACCESS_FINAL;

        //constant
        if (modifiers & FIELD_MOD_CONSTANT)
            attrib |= DBG_ATTRIB_VALUE_READONLY;

        //storage
        if (m_fieldKind & FIELD_SYM_GLOBAL)
            attrib |= DBG_ATTRIB_STORAGE_GLOBAL;
        if (modifiers & FIELD_MOD_STATIC)
            attrib |= DBG_ATTRIB_STORAGE_STATIC;

        //type modifier
        if (modifiers & FIELD_MOD_VIRTUAL)
            attrib |= DBG_ATTRIB_TYPE_VIRTUAL;
        if (modifiers & FIELD_MOD_CONSTANT)
            attrib |= DBG_ATTRIB_TYPE_CONSTANT;
        if (modifiers & FIELD_MOD_SYNCHRONIZED)
            attrib |= DBG_ATTRIB_TYPE_SYNCHRONIZED;
        if (modifiers & FIELD_MOD_VOLATILE)
            attrib |= DBG_ATTRIB_TYPE_VOLATILE;

        //type
        if (m_fieldKind & FIELD_TYPE_METHOD)
            attrib |= DBG_ATTRIB_METHOD;
        if (m_fieldKind & FIELD_TYPE_PROP)
            attrib |= DBG_ATTRIB_PROPERTY;
        if (m_fieldKind & FIELD_TYPE_CLASS)
            attrib |= DBG_ATTRIB_CLASS;
        if (m_fieldKind & FIELD_TYPE_INTERFACE)
            attrib |= DBG_ATTRIB_INTERFACE;
        if (m_fieldKind & FIELD_TYPE_INNERCLASS)
            attrib |= DBG_ATTRIB_INNERCLASS;
        if (m_fieldKind & FIELD_KIND_SYMBOL)
            attrib |= DBG_ATTRIB_DATA;

        //set the debug attributes
        ppropertyInfo->dwAttrib = attrib;
    }

    return S_OK;
}

//////////////////////////////////////////////////////////////////////
// Helper functions

struct PrimitiveTypeInfo
{
    LPCOLESTR  pszName;
    UINT       size;
    VARTYPE    vt;
};

PrimitiveTypeInfo primitiveTypeTable[] =
{
    { OLE("string"),    0,    VT_BSTR },
    { OLE("whole"),     1,    VT_I1   },
    { OLE("whole"),     2,    VT_I2   },
    { OLE("whole"),     4,    VT_I4   },
    { OLE("whole"),     8,    VT_I8   },
    { OLE("uwhole"),    1,    VT_UI1  },
    { OLE("uwhole"),    2,    VT_UI2  },
    { OLE("uwhole"),    4,    VT_UI4  },
    { OLE("uwhole"),    8,    VT_UI8  },
    { OLE("real"),      4,    VT_R4   },
    { OLE("real"),      8,    VT_R8   },
    { OLE("bool"),      1,    VT_BOOL },
    { OLE("bool"),      2,    VT_BOOL },
    { OLE("bool"),      4,    VT_BOOL },

    { OLE("System.String"),   0,  VT_BSTR },
    { OLE("System.SByte"),    1,  VT_I1   },
    { OLE("System.Int16"),    2,  VT_I2   },
    { OLE("System.Int32"),    4,  VT_I4   },
    { OLE("System.Int64"),    8,  VT_I8   },
    { OLE("System.Byte"),     1,  VT_UI1  },
    { OLE("System.Char"),     1,  VT_UI2  },
    { OLE("System.UInt16"),   2,  VT_UI2  },
    { OLE("System.UInt32"),   4,  VT_UI4  },
    { OLE("System.UInt64"),   8,  VT_UI8  },
    { OLE("System.Single"),   4,  VT_R4   },
    { OLE("System.Double"),   8,  VT_R8   },
    { OLE("System.Boolean"),  1,  VT_BOOL },
    { OLE("System.Boolean"),  2,  VT_BOOL },
    { OLE("System.Boolean"),  4,  VT_BOOL },

    { NULL, 0, VT_EMPTY }
};

HRESULT FieldGetType( in IDebugField* pfield, out VARIANT* pvarType )
{
    HRESULT hr;

    if (pfield == NULL)
        return E_INVALIDARG;
    if (pvarType == NULL)
        return E_INVALIDARG;
    else
        *pvarType = 0;

    //get type size and name
    DWORD        fieldTypeSize;
    FIELD_INFO   fieldTypeInfo;
    IDebugField* pfieldType = NULL;

    hr = pfield->GetType( &pfieldType );
    if (FAILED(hr))
        return hr;

    hr = pfieldType->GetSize( &fieldTypeSize );
    if (FAILED(hr))
    {
        pfieldType->Release();
        return hr;
    }

    hr = pfieldType->GetInfo( FIF_NAME, &fieldTypeInfo );
    if (FAILED(hr))
    {
        pfieldType->Release();
        return hr;
    }

    //check for primitive types
    memset( pvarType, 0, sizeof(*pvarType) );
    VariantInit(pvarType);

    for (PrimitiveTypeInfo* pprimTypeInfo = primitiveTypeTable;
         pprimTypeInfo->pszName != NULL;
         pprimTypeInfo++)
    {
        if (pprimTypeInfo->size == fieldTypeSize &&
           (wcscmp(pprimTypeInfo->pszName,fieldTypeInfo.bstrName) == 0))
        {
            pvarType->vt = pprimTypeInfo->vt;
            break;
        }
    }

    //VT_UNKNOWN is used for all other (structured) types
    if (pvarType->vt == VT_EMPTY)
    {
        pvarType->vt      = VT_UNKNOWN;
        pvarType->punkVal = pfieldType;
        pvarType->punkVal->AddRef();
    }

    if (fieldTypeInfo.bstrName != NULL)
        SysFreeString(fieldTypeInfo.bstrName);
    pfieldType->Release();
    return S_OK;
}

//----------------------------------------------------------------------------

HRESULT FieldGetValue( in IDebugField* pfield, out VARIANT* pvarValue )
{
    if (pvarValue == NULL)
        return E_INVALIDARG;
    else
        *pvarValue = 0;
    if (pfield == NULL)
        return E_INVALIDARG;

    //we delay getting the primitive value by just setting VT_UNKNOWN
    pvarValue->vt      = VT_UNKNOWN;
    pvarValue->punkVal = pfield;
    pvarValue->punkVal->AddRef();

    return S_OK;
}
```

## <a name="see-also"></a>関連項目
- [ローカルの実装のサンプル](../../extensibility/debugger/sample-implementation-of-locals.md)
- [ローカルプロパティの取得](../../extensibility/debugger/getting-local-properties.md)
- [評価コンテキスト](../../extensibility/debugger/evaluation-context.md)
