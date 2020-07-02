---
title: 'CA1709: 識別子は大文字と小文字が正しく使用されます。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- IdentifiersShouldBeCasedCorrectly
- CA1709
helpviewer_keywords:
- CA1709
- IdentifiersShouldBeCasedCorrectly
ms.assetid: f633d1a7-4ca4-40ae-b207-ec571c5fb083
caps.latest.revision: 30
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 14c50ed94f05401cc5575af9f8b98472c35b261d
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544002"
---
# <a name="ca1709-identifiers-should-be-cased-correctly"></a>CA1709:識別子では、大文字と小文字が正しく区別されなければなりません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio の最新のドキュメントについては、「 [CA1709: identifier は大文字にする必要があり](/visualstudio/code-quality/ca1709-identifiers-should-be-cased-correctly)ます」を参照してください。

|アイテム|値|
|-|-|
|TypeName|IdentifiersShouldBeCasedCorrectly|
|CheckId|CA1709|
|カテゴリ|Microsoft.Naming|
|互換性に影響する変更点|中断-アセンブリ、名前空間、型、メンバー、およびパラメーターで発生した場合。<br /><br /> 非ブレーク-ジェネリック型パラメーターで発生した場合。|

## <a name="cause"></a>原因
 識別子の名前の大文字と小文字が正しくありません。

 \- または

 識別子の名前に2文字の頭字語が含まれ、2番目の文字が小文字になっています。

 \- または

 識別子の名前には、3文字以上の大文字の頭字語が含まれています。

## <a name="rule-description"></a>ルールの説明
 名前付け規則では、共通言語ランタイムをターゲットとするライブラリの統一的な名前の付け方が規定されています。 これにより、新しいソフトウェア ライブラリを習得するまでの時間を短縮でき、マネージド コード開発の専門家によってライブラリが開発されたという信頼を顧客に与えることができます。

 慣例として、パラメーター名には camel 形式の文字を使用します。名前空間、型、およびメンバーの名前は、Pascal 形式を使用します。 Camel 形式の名前では、最初の文字は小文字で、名前に含まれる残りの単語の最初の文字は大文字になります。 Camel 形式の名前の例としては、"packetSniffer"、"ioFile"、"Fat Alerrorcode" などがあります。 Pascal 形式の名前では、最初の文字は大文字になり、名前の残りの単語の最初の文字は大文字になります。 Pascal 形式の名前の例としては、"PacketSniffer"、"IOFile"、"Fat Alerrorcode" などがあります。

 このルールでは、大文字小文字に基づいて名前が単語に分割され、2文字の単語が、"In" や "My" などの一般的な2文字の単語の一覧と照合されます。 一致するものが見つからない場合、単語は頭字語であると見なされます。 さらに、この規則では、名前の先頭に4文字の大文字が含まれている場合に、名前の末尾に3つの大文字が含まれていることを前提としています。

 慣例として、2文字の頭字語ではすべて大文字が使用され、3文字以上の頭字語では Pascal 形式が使用されます。 次の例では、' DB '、' CR '、' Cpa '、および ' Ecma ' という名前付け規則を使用します。 次の例では、' Io '、' XML '、' DoD ' の規則に違反しています。また、パラメーター名が ' xp '、' cpl ' 以外の場合は、この規則に違反します。

 "ID" は特殊なケースで、この規則に違反する原因になります。 ' Id ' は頭字語ではありませんが、' id ' の省略形です。

## <a name="how-to-fix-violations"></a>違反の修正方法
 大文字と小文字が正しくなるように名前を変更します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 独自の名前付け規則がある場合、または識別子が会社またはテクノロジの名前などの適切な名前を表す場合は、この警告を抑制することが安全です。

 また、コード分析カスタム辞書に特定の用語、略語、および頭字語を追加することもできます。 カスタム辞書に指定された用語は、このルールの違反を引き起こすことはありません。 詳細については、「[方法: コード分析辞書をカスタマイズする](../code-quality/how-to-customize-the-code-analysis-dictionary.md)」を参照してください。

## <a name="related-rules"></a>関連規則
 [CA1708:識別子は、大文字と小文字の区別以外にも相違していなければなりません](../code-quality/ca1708-identifiers-should-differ-by-more-than-case.md)
