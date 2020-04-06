---
title: をクリックします。マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80726890"
---
# <a name="idebugmodule3getsymbolinfo"></a>IDebugModule3::GetSymbolInfo
シンボルを検索するパスのリストと、各パスの検索結果を取得します。

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
[in]SYMBOL_SEARCH_INFO_FIELDS[列挙体](../../../extensibility/debugger/reference/symbol-search-info-fields.md)のフラグの組み合わせで、入力`pInfo`するフィールドを指定します。

`pInfo`\
[アウト]指定された情報をメンバに入力する[MODULE_SYMBOL_SEARCH_INFO](../../../extensibility/debugger/reference/module-symbol-search-info.md)構造体。 これが null 値の場合、このメソッド`E_INVALIDARG`は を返します。

## <a name="return-value"></a>戻り値
メソッドが成功すると、返されます`S_OK`。それ以外の場合は、エラー コードを返します。

> [!NOTE]
> (構造体内の)`MODULE_SYMBOL_SEARCH_INFO`返される文字列は、返された`S_OK`場合でも空になる可能性があります。 この場合、返す検索情報はありませんでした。

## <a name="remarks"></a>Remarks
`MODULE_SYMBOL_SEARCH_INFO`構造体の`bstrVerboseSearchInfo`フィールドが空でない場合は、検索されたパスのリストとその検索結果が含まれます。 リストはパスで書式設定され、その後に省略記号 ("...") が続き、その後に結果が続きます。 複数のパス結果ペアがある場合、各ペアは"\r\n"(復帰/改行)ペアで区切られます。 パターンは次のようになります。

\<パス>.\<>\r\n\<パス>.\<結果>\r\n\<パス>.\<結果>

最後のエントリには \r\n シーケンスがありません。

## <a name="example"></a>例
この例では、このメソッドは 3 つの異なる検索結果を持つ 3 つのパスを返します。 各行は、復帰/改行のペアで終了します。 出力例では、検索結果を単一の文字列として出力します。

> [!NOTE]
> ステータスの結果は、"..行の最後まで。

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

**c:\シンボル\ユーザー32.pdb..ファイルが見つかりません。**
 **c:\winnt\シンボル\ユーザー32.pdb..バージョンが一致しません。**
\シンボル**\シンボル\ユーザー32.dll\0a8sd0ad\user32.pdb.. \\シンボルが読み込まれました。**

## <a name="see-also"></a>関連項目

- [SYMBOL_SEARCH_INFO_FIELDS](../../../extensibility/debugger/reference/symbol-search-info-fields.md)
- [MODULE_SYMBOL_SEARCH_INFO](../../../extensibility/debugger/reference/module-symbol-search-info.md)
- [IDebugModule3](../../../extensibility/debugger/reference/idebugmodule3.md)
