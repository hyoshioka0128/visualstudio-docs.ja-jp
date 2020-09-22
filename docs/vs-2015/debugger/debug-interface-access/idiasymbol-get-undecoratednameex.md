---
title: 'IDiaSymbol:: get_undecoratedNameEx |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_undecoratedNameEx method
ms.assetid: 579aed0b-c57d-41a1-a94a-3bf665fd4a9d
caps.latest.revision: 14
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: f9c50f5d352d8a52b0eb8b125992b2c325e48234
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841888"
---
# <a name="idiasymbolget_undecoratednameex"></a>IDiaSymbol::get_undecoratedNameEx
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

C++ の修飾 (リンケージ) 名の装飾のない名前の一部またはすべてを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT get_undecoratedNameEx(   
   DWORD undecorateOptions,  
   BSTR* pRetval  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `undecoratedOptions`  
 から返される内容を制御するフラグの組み合わせを指定します。 特定の値とその実行内容については、「解説」を参照してください。  
  
 `pRetVal`  
 入出力C++ の装飾名の装飾されていない名前を返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合は、を返し `S_OK` ます。それ以外の場合 `S_FALSE` は、またはエラーコードを返します。  
  
> [!NOTE]
> の戻り値は、 `S_FALSE` そのシンボルに対してプロパティを使用できないことを意味します。  
  
## <a name="remarks"></a>注釈  
 は、 `undecorateOptions` 次のフラグの組み合わせにすることができます。  
  
> [!NOTE]
> フラグ名は DIA SDK で定義されていないため、宣言をコードに追加するか、生の値を使用する必要があります。  
  
|フラグ|値|説明|  
|----------|-----------|-----------------|  
|UNDNAME_COMPLETE|0x0000|完全修飾を有効にします。|  
|UNDNAME_NO_LEADING_UNDERSCORES|0x0001|Microsoft 拡張キーワードから先頭のアンダースコアを削除します。|  
|UNDNAME_NO_MS_KEYWORDS|0x0002|Microsoft 拡張キーワードの展開を無効にします。|  
|UNDNAME_NO_FUNCTION_RETURNS|0x0004|プライマリ宣言の戻り値の型の展開を無効にします。|  
|UNDNAME_NO_ALLOCATION_MODEL|0x0008|宣言モデルの展開を無効にします。|  
|UNDNAME_NO_ALLOCATION_LANGUAGE|0x0010|宣言言語指定子の展開を無効にします。|  
|UNDNAME_RESERVED1|0x0020|予約済み。|  
|UNDNAME_RESERVED2|0x0040|予約済み。|  
|UNDNAME_NO_THISTYPE|0x0060|型のすべての修飾子を無効に `this` します。|  
|UNDNAME_NO_ACCESS_SPECIFIERS|0x0080|メンバーのアクセス指定子の展開を無効にします。|  
|UNDNAME_NO_THROW_SIGNATURES|0x0100|関数および関数へのポインターに対する "throw 署名" の展開を無効にします。|  
|UNDNAME_NO_MEMBER_TYPE|0x0200|メンバーまたはメンバーの展開を無効に `static` `virtual` します。|  
|UNDNAME_NO_RETURN_UDT_MODEL|0x0400|UDT の戻り値に対する Microsoft モデルの拡張を無効にします。|  
|UNDNAME_32_BIT_DECODE|0x0800|Undecorates 32 ビットの装飾名。|  
|UNDNAME_NAME_ONLY|0x1000|プライマリ宣言の名前のみを取得します。[scope::] の名前だけを返します。  テンプレートパラメーターを展開します。|  
|UNDNAME_TYPE_ONLY|0x2000|入力は型のエンコードにすぎません。抽象宣言子を合成します。|  
|UNDNAME_HAVE_PARAMETERS|0x4000|実際のテンプレートパラメーターを使用できます。|  
|UNDNAME_NO_ECSU|0x8000|列挙型/クラス/構造体/共用体を非表示にします。|  
|UNDNAME_NO_IDENT_CHAR_CHECK|0x10000|有効な識別子文字のチェックを抑制します。|  
|UNDNAME_NO_PTR64|0x20000|出力に ptr64 が含まれていません。|  
  
## <a name="see-also"></a>参照  
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
