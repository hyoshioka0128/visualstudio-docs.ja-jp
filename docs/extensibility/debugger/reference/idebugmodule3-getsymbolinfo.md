---
title: 'IDebugModule3:: Getシンボル Info |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugModule3::GetSymbolInfo
helpviewer_keywords:
- GetSymbolInfo method
- IDebugModule3::GetSymbolInfo method
ms.assetid: dda5e8e1-6878-4aa9-9ee4-e7d0dcc11210
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3aafb28715f58eaba4499b47a2e1dee15b82ed14
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80726890"
---
# <a name="idebugmodule3getsymbolinfo"></a>IDebugModule3::GetSymbolInfo
シンボルを検索するパスの一覧と、各パスを検索した結果を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetSymbolInfo(
    SYMBOL_SEARCH_INFO_FIELDS  dwFields,
    MODULE_SYMBOL_SEARCH_INFO* pInfo
);
```

```csharp
int GetSymbolInfo(
    enum_SYMBOL_SEARCH_INFO_FIELDS dwFields,
    MODULE_SYMBOL_SEARCH_INFO[]    pinfo
);
```

## <a name="parameters"></a>パラメーター
`dwFields`\
からどのフィールドを入力するかを指定する、 [SYMBOL_SEARCH_INFO_FIELDS](../../../extensibility/debugger/reference/symbol-search-info-fields.md) 列挙のフラグの組み合わせ `pInfo` 。

`pInfo`\
入出力指定された情報を格納するメンバーを持つ [MODULE_SYMBOL_SEARCH_INFO](../../../extensibility/debugger/reference/module-symbol-search-info.md) 構造体。 Null 値の場合、このメソッドはを返し `E_INVALIDARG` ます。

## <a name="return-value"></a>戻り値
メソッドが成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

> [!NOTE]
> が返された場合でも、返された文字列 ( `MODULE_SYMBOL_SEARCH_INFO` 構造体内) は空になる可能性があり `S_OK` ます。 この場合、返される検索情報がありませんでした。

## <a name="remarks"></a>解説
`bstrVerboseSearchInfo` `MODULE_SYMBOL_SEARCH_INFO` 構造体のフィールドが空でない場合は、検索対象のパスと検索結果の一覧が含まれています。 リストはパスで書式設定され、その後に省略記号 ("...") が続き、その後に結果が続きます。 複数のパスの結果のペアがある場合、各ペアは "\r\n" (キャリッジリターン/ラインフィード) ペアで区切られます。 パターンは次のようになります。

\<path>...\<result>\r\n \<path> . \<result> .\r\n \<path> ..\<result>

最後のエントリには \r\n シーケンスがないことに注意してください。

## <a name="example"></a>例
この例では、このメソッドは3つの異なる検索結果を持つ3つのパスを返します。 各行は、復帰とラインフィードのペアで終了します。 この例では、単に検索結果を1つの文字列として出力します。

> [!NOTE]
> 状態の結果は、"..." の直後に続くものです。行の最後まで。

```cpp
void ShowSymbolSearchResults(IDebugModule3 *pIDebugModule3)
{
    MODULE_SYMBOL_SEARCH_INFO ssi = { 0 };
    HRESULT hr;
    hr = pIDebugModule3->GetSymbolInfo(SSIF_VERBOSE_SEARCH_INFO,&ssi);
    if (SUCCEEDED(hr)) {
        CComBSTR searchInfo = ssi.bstrVerboseSearchInfo;
        if (searchInfo.Length() != 0) {
            std::wcout << (wchar_t *)(BSTR)searchInfo;
            std::wcout << std::endl;
        }
    }
}
```

**c:\symbols\user32.pdb...ファイルが見つかりません。** 
**c:\winnt\symbols\user32.pdb...バージョンが一致しません。** 
** \\\symbols\symbols\user32.dll \0a8sd0ad8ad\user32.pdb...シンボルが読み込まれ**ました。

## <a name="see-also"></a>関連項目

- [SYMBOL_SEARCH_INFO_FIELDS](../../../extensibility/debugger/reference/symbol-search-info-fields.md)
- [MODULE_SYMBOL_SEARCH_INFO](../../../extensibility/debugger/reference/module-symbol-search-info.md)
- [IDebugModule3](../../../extensibility/debugger/reference/idebugmodule3.md)
