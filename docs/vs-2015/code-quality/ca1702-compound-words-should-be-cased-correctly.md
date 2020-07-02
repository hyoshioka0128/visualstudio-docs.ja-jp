---
title: 'CA1702: 複合語は大文字にする必要があります。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1702
- CompoundWordsShouldBeCasedCorrectly
helpviewer_keywords:
- CA1702
- CompoundWordsShouldBeCasedCorrectly
ms.assetid: 05481245-7ad8-48c3-a456-3aa44b6160a6
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: f9dc15cec4012d2b63eb5f21c25bd709961c95c8
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544080"
---
# <a name="ca1702-compound-words-should-be-cased-correctly"></a>CA1702:複合語では、大文字と小文字が正しく区別されなければなりません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio の最新のドキュメントについては、「 [CA1702: 複合単語の大文字と小文字](/visualstudio/code-quality/ca1702-compound-words-should-be-cased-correctly)の区別」を参照してください。

|アイテム|値|
|-|-|
|TypeName|CompoundWordsShouldBeCasedCorrectly|
|CheckId|CA1702|
|カテゴリ|Microsoft.Naming|
|互換性に影響する変更点|中断-アセンブリで発生した場合。<br /><br /> 中断なし-型パラメーターで発生した場合。|

## <a name="cause"></a>原因
 識別子の名前に複数の単語が含まれており、少なくとも1つの単語が大文字と小文字が正しくない複合語であることが示されています。

## <a name="rule-description"></a>ルールの説明
 識別子の名前は、大文字小文字に基づく単語に分割されます。 それぞれの連続する2単語の組み合わせは、Microsoft スペルチェックライブラリによってチェックされます。 認識されている場合は、識別子によってルールの違反が生成されます。 違反の原因となる複合語の例としては、"CheckSum" と "マルチパート" があります。これは、それぞれ "Checksum" と "マルチパート" として使用する必要があります。 これまでの一般的な使用により、いくつかの例外がルールに組み込まれています。また、"Toolbar" や "Filename" など、複数の単語にフラグが設定されている場合は、2つの単語 (この場合は "ToolBar" と "FileName") として大文字と小文字が区別されます。

 名前付け規則では、共通言語ランタイムをターゲットとするライブラリの統一的な名前の付け方が規定されています。 これにより、新しいソフトウェア ライブラリを習得するまでの時間を短縮でき、マネージド コード開発の専門家によってライブラリが開発されたという信頼を顧客に与えることができます。

## <a name="how-to-fix-violations"></a>違反の修正方法
 大文字と小文字が正しくなるように名前を変更します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 複合語の両方の部分がスペル辞書によって認識され、目的が2つの単語を使用する場合は、この規則による警告を抑制しても安全です。

## <a name="related-rules"></a>関連規則
 [CA1701:リソース文字列の複合語は、大文字と小文字を正しく区別しなければなりません](../code-quality/ca1701-resource-string-compound-words-should-be-cased-correctly.md)

 [CA1709:識別子では、大文字と小文字が正しく区別されなければなりません](../code-quality/ca1709-identifiers-should-be-cased-correctly.md)

 [CA1708:識別子は、大文字と小文字の区別以外にも相違していなければなりません](../code-quality/ca1708-identifiers-should-differ-by-more-than-case.md)

## <a name="see-also"></a>関連項目
 [名前付けガイドライン](https://msdn.microsoft.com/library/fc076d66-9b5f-42d3-aa65-61d970c794a3)の[大文字小文字の表記規則](https://msdn.microsoft.com/library/4c4ea526-9203-486f-b72d-29d61c5b3c6d)
