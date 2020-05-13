---
title: MODULE_SYMBOL_SEARCH_INFO |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- MODULE_SYMBOL_SEARCH_INFO
helpviewer_keywords:
- MODULE_SYMBOL_SEARCH_INFO structure
ms.assetid: 432aff03-08a5-4c5a-b2d5-e212090fc70a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 5f15587759c4f665d1593d1298c47459a0e64aac
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80714253"
---
# <a name="module_symbol_search_info"></a>MODULE_SYMBOL_SEARCH_INFO

検索されたシンボル検索パスに関するステータス情報を格納します。

## <a name="syntax"></a>構文

```cpp
typedef struct _tagSYMBOL_SEARCH_INFO
{
    SYMBOL_SEARCH_INFO_FIELDS dwValidFields;
    BSTR                      bstrVerboseSearchInfo;
} MODULE_SYMBOL_SEARCH_INFO;
```

```csharp
public struct MODULE_SYMBOL_SEARCH_INFO {
    public uint   dwValidFields;
    public string bstrVerboseSearchInfo;
}
```

## <a name="members"></a>メンバー

`dwValidFields`\
この構造体で説明されている検索情報の種類を指定する[SYMBOL_SEARCH_INFO_FIELDS](../../../extensibility/debugger/reference/symbol-search-info-fields.md)列挙体のフラグの組み合わせ。

`bstrVerboseSearchInfo`\
検索パスと結果を 1 つの文字列に連結します。

## <a name="remarks"></a>Remarks

この構造体は[、GetSymbolInfo](../../../extensibility/debugger/reference/idebugmodule3-getsymbolinfo.md)メソッドの呼び出しから返されます。

フィールドが`bstrVerboseSearchInfo`空でない場合は、検索されたパスとその検索の結果のリストが含まれます。 リストはパスで書式設定され、その後に省略記号 ("...") が続き、その後に結果が続きます。 複数のパス結果ペアがある場合、各ペアは"\r\n"(復帰/改行)ペアで区切られます。 パターンは次のようになります。

\<パス>.\<>\r\n\<パス>.\<結果>\r\n\<パス>.\<結果>

最後のエントリには \r\n シーケンスがありません。

標準出力に送信`bstrVerboseSearchInfo`された可能性のある文字列を次に示します。

`c:\symbols\user32.pdb... File not found.`

`c:\winnt\symbols\user32.pdb... Version does not match.`

`\\symbols\symbols\user32.dll\0a8sd0ad8ad\user32.pdb... Symbols loaded.`

## <a name="requirements"></a>必要条件

ヘッダー: msdbg.h

名前空間: を使用します。

アセンブリ:

## <a name="see-also"></a>関連項目

- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [GetSymbolInfo](../../../extensibility/debugger/reference/idebugmodule3-getsymbolinfo.md)
