---
title: ローカルの評価 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], evaluating locals
- expression evaluation, evaluating locals
ms.assetid: 7d1ed528-4e7a-4d8f-87b4-162440644a75
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: aaf140a9ddbc7733da4d05450a024c0f0a713712
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738821"
---
# <a name="evaluate-locals"></a>ローカルを評価する
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターのこの実装方法は非推奨になりました。 CLR 式エバリュエーターの実装については[、「CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) 」および「[マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

[GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md)ローカルの値、およびローカルの名前と型を取得するために呼び出されます。 ローカルの値はプログラムの現在の状態に依存するため、ローカルの値はメモリから取得する必要があります。 オブジェクト[は](../../extensibility/debugger/reference/idebugbinder.md)、ローカルを表す[IDebugField](../../extensibility/debugger/reference/idebugfield.md)オブジェクトを、値を含むメモリ内の適切な場所にバインドするために使用されます。 メモリ内のこの位置は[、IDebugObject](../../extensibility/debugger/reference/idebugobject.md)オブジェクトによって表されます。

ローカルの値を取得するこの機能は、次のタスクを実行するヘルパー関数にカプセル化されます。

1. オブジェクトを`IDebugField`メモリにバインドしてオブジェクトを`IDebugObject`取得します。

2. メモリから値を取得します。 この値は、一連のバイトとして表されます。

3. ローカルの型に基づいて値を書式設定します。

4. ローカルの値を格納するジェネリック オブジェクトを返します。 C# では、これは`object`です。 `VARIANT`

## <a name="managed-code"></a>マネージド コード
 これは、マネージ コード内のローカルの値を取得する関数の実装です。

```csharp
namespace EEMC
{
    internal class Field
    {
        internal static object GetValue(
            IDebugBinder binder,
            IDebugField field,
            Type t,
            uint size)
        {
            if (t == null || size == 0)  return null;

            IDebugObject debugObject = null;
            binder.Bind(null, field, out debugObject);

            byte[] buffer = new byte[size];
            for (int i = 0; i < size; i++)  buffer[i] = 0;

            debugObject.GetValue(buffer, size);

            if (t == typeof(sbyte)) return (sbyte) buffer[0];
            if (t == typeof(short)) return BitConverter.ToInt16(buffer, 0);
            if (t == typeof(int))   return BitConverter.ToInt32(buffer, 0);
            if (t == typeof(long))  return BitConverter.ToInt64(buffer, 0);
            if (t == typeof(byte))  return buffer[0];
            if (t == typeof(char))  return BitConverter.ToChar(buffer, 0);
            if (t == typeof(uint))  return BitConverter.ToUInt32(buffer, 0);
            if (t == typeof(ulong)) return BitConverter.ToUInt64(buffer, 0);
            if (t == typeof(float)) return BitConverter.ToSingle(buffer, 0);
            if (t == typeof(double))  return BitConverter.ToDouble(buffer, 0);
            if (t == typeof(bool))  return BitConverter.ToBoolean(buffer, 0);
            if (t == typeof(string))  return BitConverter.ToString(buffer, 0);
            return null;
        }
    }
}
```

## <a name="unmanaged-code"></a>アンマネージ コード
 これは、アンマネージ コード内のローカルの値を取得する関数の実装です。 `FieldGetType`は、[ローカル値の取得 に](../../extensibility/debugger/getting-local-values.md)示されています。

```cpp
HRESULT FieldGetPrimitiveValue(
    in  IDebugBinder* pbinder,
    in  IDebugField*  pfield,
    out VARIANT*      pvarValue
    )
{
    if (pvarValue == NULL)
        return E_INVALIDARG;
    else
        *pvarValue = 0;

    if (pfield == NULL)
        return E_INVALIDARG;

    if (pbinder == NULL)
        return E_INVALIDARG;

    HRESULT hr;
    UINT          valueSize = 0;
    BYTE*         pvalueBits = NULL;
    IDebugObject* pobject    = NULL;

    //get the value as bits
    hr = pbinder->Bind( NULL, pfield, &pobject );
    if (FAILED(hr))
        return hr;

    hr = pobject->GetSize( &valueSize );
    if (FAILED(hr))
    {
        pobject->Release();
        return hr;
    }

    pvalueBits = reinterpret_cast<BYTE *>(malloc(valueSize * sizeof(BYTE)));
    if (!pvalueBits)
    {
        pobject->Release();
        return E_OUTOFMEMORY;
    }

    hr = pobject->GetValue( pvalueBits, valueSize );
    pobject->Release();
    if (FAILED(hr))
    {
        free(pvalueBits);
        return hr;
    }

    //get the type
    VARIANT     valueType;

    hr = FieldGetType( pfield, &valueType );
    if (FAILED(hr))
    {
        free(pvalueBits);
        return hr;
    }

    //copy a primitive value
    switch (valueType.vt)
    {
    case VT_BSTR:
        {
            pvarValue->vt = VT_BSTR;
            if (valueSize == 0)
                pvarValue->bstrVal = SysAllocString( OLE("") );
            else
                pvarValue->bstrVal =
                    SysAllocStringByteLen( reinterpret_cast<char*>(pvalueBits),
                                           valueSize );
        }

    case VT_BOOL:
    case VT_I1:
    case VT_I2:
    case VT_I4:
    case VT_I8:
    case VT_UI1:
    case VT_UI2:
    case VT_UI4:
    case VT_UI8:
    case VT_R4:
    case VT_R8:
        pvarValue->vt = valueType.vt;

        if (valueSize > 8)
            valueSize = 8;
        memcpy( &(pvarValue->iVal), pvalueBits, valueSize );
        break;

    case VT_VOID:
    case VT_EMPTY:
        pvarValue->vt = valueType.vt;
        break;

    default:
        //not a primitive type
        VariantClear(&valueType);
        free(pvalueBits);
        return E_FAIL;
    }

    free(pvalueBits);
    VariantClear(&valueType);
    return S_OK;
}
```

## <a name="see-also"></a>関連項目
- [ローカルのサンプル実装](../../extensibility/debugger/sample-implementation-of-locals.md)
- [ローカル値を取得する](../../extensibility/debugger/getting-local-values.md)
- [評価コンテキスト](../../extensibility/debugger/evaluation-context.md)
