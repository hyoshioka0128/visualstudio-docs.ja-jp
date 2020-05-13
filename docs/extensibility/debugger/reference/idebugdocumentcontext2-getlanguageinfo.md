---
title: をクリックします。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocumentContext2::GetLanguageInfo
helpviewer_keywords:
- IDebugDocumentContext2::GetLanguageInfo
ms.assetid: 6a212ee5-414c-4eb5-ab11-19db1786943d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9d139029bf65149ae59fb037434f6e7d6298f1d5
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80731859"
---
# <a name="idebugdocumentcontext2getlanguageinfo"></a>IDebugDocumentContext2::GetLanguageInfo
このドキュメント コンテキストに関連付けられている言語を取得します。

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
[アウト]このドキュメント コンテキストでコードを実装する言語の名前を返します。

`pguidLanguage`\
[アウト]このドキュメント コンテキストでコードを実装する言語の GUID を返します。 たとえば、`guidVBScriptLang` または `guidCPPLang` です。 この GUID は、 によって[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]提供される言語に限定されません。

## <a name="return-value"></a>戻り値
成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="example"></a>例
次の例は[、IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)インターフェイス`CDebugContext`を公開する単純なオブジェクトに対してこのメソッドを実装する方法を示しています。

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

## <a name="see-also"></a>関連項目
- [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)
