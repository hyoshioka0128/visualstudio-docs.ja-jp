---
title: MODULE_SYMBOL_SEARCH_INFO |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- MODULE_SYMBOL_SEARCH_INFO
helpviewer_keywords:
- MODULE_SYMBOL_SEARCH_INFO structure
ms.assetid: 432aff03-08a5-4c5a-b2d5-e212090fc70a
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: e2cfbaf8c3756bf758956d1f1e5964d8e9f8f0c8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68205185"
---
# <a name="module_symbol_search_info"></a>MODULE_SYMBOL_SEARCH_INFO
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

検索されたシンボル検索パスに関する状態情報が含まれます。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
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
  
#### <a name="parameters"></a>パラメーター  
 `dwValidFields`  
 この構造体で記述されている検索情報の種類を指定する、 [SYMBOL_SEARCH_INFO_FIELDS](../../../extensibility/debugger/reference/symbol-search-info-fields.md) 列挙のフラグの組み合わせ。  
  
 `bstrVerboseSearchInfo`  
 検索パスと結果が1つの文字列に連結されます。  
  
## <a name="remarks"></a>注釈  
 この構造体は、 [Getシンボル情報](../../../extensibility/debugger/reference/idebugmodule3-getsymbolinfo.md) メソッドの呼び出しから返されます。  
  
 `bstrVerboseSearchInfo`フィールドが空でない場合は、検索したパスとその検索結果の一覧が含まれています。 リストはパスで書式設定され、その後に省略記号 ("...") が続き、その後に結果が続きます。 複数のパスの結果のペアがある場合、各ペアは "\r\n" (キャリッジリターン/ラインフィード) ペアで区切られます。 パターンは次のようになります。  
  
 \<path>...\<result>\r\n \<path> . \<result> .\r\n \<path> ..\<result>  
  
 最後のエントリには \r\n シーケンスがないことに注意してください。  
  
 次に示すのは、 `bstrVerboseSearchInfo` 標準出力に送信された文字列です。  
  
 `c:\symbols\user32.pdb... File not found.`  
  
 `c:\winnt\symbols\user32.pdb... Version does not match.`  
  
 `\\symbols\symbols\user32.dll\0a8sd0ad8ad\user32.pdb... Symbols loaded.`  
  
## <a name="requirements"></a>要件  
 ヘッダー: msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)   
 [GetSymbolInfo](../../../extensibility/debugger/reference/idebugmodule3-getsymbolinfo.md)
