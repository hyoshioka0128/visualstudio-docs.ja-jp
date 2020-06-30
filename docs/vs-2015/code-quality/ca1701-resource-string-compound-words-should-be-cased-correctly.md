---
title: 'CA1701: リソース文字列の複合語は、大文字と小文字が正しく使用されている必要があります。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- ResourceStringCompoundWordsShouldBeCasedCorrectly
- CA1701
helpviewer_keywords:
- CA1701
- ResourceStringCompoundWordsShouldBeCasedCorrectly
ms.assetid: 4ddbe09f-24b8-4c47-9373-a06f4487ca0d
caps.latest.revision: 26
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 7c1c3b0fd6cf3a25d5db9e3039d4dc5d8364a18e
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544106"
---
# <a name="ca1701-resource-string-compound-words-should-be-cased-correctly"></a>CA1701:リソース文字列の複合語は、大文字と小文字を正しく区別しなければなりません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|ResourceStringCompoundWordsShouldBeCasedCorrectly|
|CheckId|CA1701|
|カテゴリ|Microsoft.Naming|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因
 リソース文字列に、大文字小文字が正しく表示されない複合語が含まれています。

## <a name="rule-description"></a>ルールの説明
 リソース文字列内の各単語は、大文字小文字に基づくトークンに分割されます。 Microsoft スペル チェック ライブラリは、隣接する 2 つのトークンの組み合わせを個別にチェックします。 それらが認識されると、その語はこの規則への違反となります。 違反の原因となる複合語の例としては、"CheckSum" と "マルチパート" があります。これは、それぞれ "Checksum" と "マルチパート" として使用する必要があります。 以前の一般的な使用により、いくつかの例外がルールに組み込まれています。また、"Toolbar" や "Filename" などの複数の単語にフラグが設定されている場合は、2つの異なる単語として大文字にする必要があります。 この例では、"ToolBar" と "FileName" にフラグが設定されています。

 名前付け規則では、共通言語ランタイムをターゲットとするライブラリの統一的な名前の付け方が規定されています。 これにより、新しいソフトウェア ライブラリを習得するまでの時間を短縮でき、マネージド コード開発の専門家によってライブラリが開発されたという信頼を顧客に与えることができます。

## <a name="how-to-fix-violations"></a>違反の修正方法
 大文字と小文字が正しくなるように単語を変更します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 複合語の両方の部分がスペル辞書によって認識され、目的が2つの単語を使用する場合は、この規則による警告を抑制しても安全です。

 また、スペルチェック用のカスタム辞書に複合単語を追加することもできます。 カスタム辞書内の単語は、違反を発生させません。 詳細については、「[方法: コード分析辞書をカスタマイズする](../code-quality/how-to-customize-the-code-analysis-dictionary.md)」を参照してください。

## <a name="related-rules"></a>関連規則
 [CA1702:複合語では、大文字と小文字が正しく区別されなければなりません](../code-quality/ca1702-compound-words-should-be-cased-correctly.md)

 [CA1709:識別子では、大文字と小文字が正しく区別されなければなりません](../code-quality/ca1709-identifiers-should-be-cased-correctly.md)

 [CA1708:識別子は、大文字と小文字の区別以外にも相違していなければなりません](../code-quality/ca1708-identifiers-should-differ-by-more-than-case.md)

## <a name="see-also"></a>関連項目
 [大文字と小文字の規則](https://msdn.microsoft.com/library/4c4ea526-9203-486f-b72d-29d61c5b3c6d)の[名前付けのガイドライン](https://msdn.microsoft.com/library/fc076d66-9b5f-42d3-aa65-61d970c794a3)
