---
description: このドキュメントコンテキストを含むドキュメントの表示可能な名前を取得します。
title: 'IDebugDocumentContext2:: GetName |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocumentContext2::GetName
helpviewer_keywords:
- IDebugDocumentContext2::GetName
ms.assetid: 546c5b2e-f166-4edb-9e61-57d797ca98a1
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b4e75cd6b963965a245055ff8fa0849e39339af1
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102146211"
---
# <a name="idebugdocumentcontext2getname"></a>IDebugDocumentContext2::GetName
このドキュメントコンテキストを含むドキュメントの表示可能な名前を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetName(
    GETNAME_TYPE gnType,
    BSTR*        pbstrFileName
);
```

```csharp
int GetName(
    enum_GETNAME_TYPE  gnType,
    out string         pbstrFileName
);
```

## <a name="parameters"></a>パラメーター
`gnType`\
から返される名前の型を指定する [GETNAME_TYPE](../../../extensibility/debugger/reference/getname-type.md) 列挙の値です。

`pbstrFileName`\
入出力ファイルの名前を返します。

## <a name="return-value"></a>戻り値
成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
このメソッドは、通常、ドキュメントの名前そのものを格納するためにドキュメントコンテキストが記述されている場合 (例のように)、 [GetName](../../../extensibility/debugger/reference/idebugdocument2-getname.md) メソッドへの呼び出しを転送します。

## <a name="example"></a>例
次の例は、IDebugDocumentContext2 インターフェイスを公開する単純なオブジェクトに対してこのメソッドを実装する方法を示して `CDebugContext` います。 [](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)

```cpp
HRESULT CDebugContext::GetName(GETNAME_TYPE gnType, BSTR* pbstrFileName)
{
    HRESULT hr;

    // Check for a valid file name argument.
    if (pbstrFileName)
    {
        *pbstrFileName = NULL;

        switch (gnType)
        {
            case GN_NAME:
            case GN_FILENAME:
            {
                // Copy the member file name into the local file name.
                *pbstrFileName = SysAllocString(m_sbstrFileName);
                // Check for successful copy.
                hr = (*pbstrFileName) ? S_OK : E_OUTOFMEMORY;
                break;
            }
            default:
            {
                hr = E_FAIL;
                break;
            }
        }
    }
    else
    {
        hr = E_INVALIDARG;
    }

    return hr;
}
```

## <a name="see-also"></a>関連項目
- [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)
- [GETNAME_TYPE](../../../extensibility/debugger/reference/getname-type.md)
