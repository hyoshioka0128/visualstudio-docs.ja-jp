---
description: このドキュメントコンテキストに関連付けられている言語を取得します。
title: 'IDebugDocumentContext2:: Get言語 Info |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocumentContext2::GetLanguageInfo
helpviewer_keywords:
- IDebugDocumentContext2::GetLanguageInfo
ms.assetid: 6a212ee5-414c-4eb5-ab11-19db1786943d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a621ca5f23af52d81e14dba6b737ca31a2525727
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105066673"
---
# <a name="idebugdocumentcontext2getlanguageinfo"></a>IDebugDocumentContext2::GetLanguageInfo
このドキュメントコンテキストに関連付けられている言語を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetLanguageInfo(
    BSTR* pbstrLanguage,
    GUID* pguidLanguage
);
```

```csharp
int GetLanguageInfo(
    out string pbstrLanguage,
    out Guid   pguidLanguage
);
```

## <a name="parameters"></a>パラメーター
`pbstrLanguage`\
入出力このドキュメントコンテキストでコードを実装する言語の名前を返します。

`pguidLanguage`\
入出力このドキュメントコンテキストでコードを実装する言語の GUID を返します。 たとえば、`guidVBScriptLang` または `guidCPPLang` です。 この GUID は、によって提供される言語に限定されません [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] 。

## <a name="return-value"></a>戻り値
成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="example"></a>例
次の例は、IDebugDocumentContext2 インターフェイスを公開する単純なオブジェクトに対してこのメソッドを実装する方法を示して `CDebugContext` います。 [](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)

```cpp
HRESULT CDebugContext::GetLanguageInfo(BSTR* pbstrLanguage, GUID* pguidLanguage)
{
    HRESULT hr;

    // Check for a valid language argument pointers.
    if (pbstrLanguage && pguidLanguage)
    {
        *pguidLanguage = GUID_NULL;
        *pbstrLanguage = SysAllocString(L"Batch File");
        if (*pbstrLanguage)
        {
            *pguidLanguage = guidBatLang;
            hr = S_OK;
        }
        else
        {
            hr = E_OUTOFMEMORY;
        }
    }
    else
    {
        hr = E_INVALIDARG;
    }

    return hr;
}
```

## <a name="see-also"></a>こちらもご覧ください
- [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)
