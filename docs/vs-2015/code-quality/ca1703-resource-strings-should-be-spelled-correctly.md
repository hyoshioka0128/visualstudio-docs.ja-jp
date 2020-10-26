---
title: 'CA1703: リソース文字列は正しく入力されている必要があります |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- ResourceStringsShouldBeSpelledCorrectly
- CA1703
helpviewer_keywords:
- CA1703
- ResourceStringsShouldBeSpelledCorrectly
ms.assetid: 693f4970-f512-40cb-ae3b-a0f3a5c6d6f1
caps.latest.revision: 18
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 2e720c1c491e88b6d89fb4b1f0175e8bc8a56e27
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85544054"
---
# <a name="ca1703-resource-strings-should-be-spelled-correctly"></a>CA1703:リソース文字列は正しく入力されなければなりません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|ResourceStringsShouldBeSpelledCorrectly|
|CheckId|CA1703|
|カテゴリ|Microsoft.Naming|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因
 リソース文字列に Microsoft スペル チェック ライブラリで認識されない語が 1 つ以上含まれています。

## <a name="rule-description"></a>ルールの説明
 この規則では、リソース文字列を単語 (トークン化複合単語) に解析し、各単語/トークンのスペルをチェックします。 解析アルゴリズムの詳細については、「 [CA1704: 識別子は正しく入力されている必要があり](../code-quality/ca1704-identifiers-should-be-spelled-correctly.md)ます。

 既定では、スペルチェックの英語 (en) バージョンが使用されます。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、正しくスペルが正しい単語を入力するか、カスタム辞書に単語を追加します。 カスタム辞書の使用方法の詳細については、「 [CA1704: identifier のスペルを正しく](../code-quality/ca1704-identifiers-should-be-spelled-correctly.md)する」を参照してください。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。 正しい綴りの単語を指定すると、新しいソフトウェアライブラリの学習に必要な時間が短縮されます。

## <a name="related-rules"></a>関連規則
 [CA1701:リソース文字列の複合語は、大文字と小文字を正しく区別しなければなりません](../code-quality/ca1701-resource-string-compound-words-should-be-cased-correctly.md)

 [CA1704:識別子は正しく入力されなければなりません](../code-quality/ca1704-identifiers-should-be-spelled-correctly.md)

 [CA2204:リテラルに正しいスペルを要求](../code-quality/ca2204-literals-should-be-spelled-correctly.md)
