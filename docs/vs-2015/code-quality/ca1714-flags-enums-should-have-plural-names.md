---
title: 'CA1714: Flags 列挙型には複数形の名前が必要です |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- FlagsEnumsShouldHavePluralNames
- CA1714
helpviewer_keywords:
- CA1714
- FlagsEnumsShouldHavePluralNames
ms.assetid: 95ef5b43-7681-49e9-a5a3-ac0357cf1be7
caps.latest.revision: 16
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 74e93a9644f365120117bd247d2ea8b9d43608cb
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85548188"
---
# <a name="ca1714-flags-enums-should-have-plural-names"></a>CA1714:フラグ列挙型は、複数形の名前を含んでいなければなりません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|FlagsEnumsShouldHavePluralNames|
|CheckId|CA1714|
|カテゴリ|Microsoft.Naming|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 パブリック列挙型にが含まれ <xref:System.FlagsAttribute?displayProperty=fullName> ており、その名前の末尾がの ' ではありません。

## <a name="rule-description"></a>ルールの説明
 でマークされている型に <xref:System.FlagsAttribute> は複数形の名前があります。これは、属性が複数の値を指定できることを示すためです。 たとえば、曜日を定義する列挙体は、複数の日を指定できるアプリケーションで使用することが想定されています。 この列挙体にはが含まれている必要があり、 <xref:System.FlagsAttribute> ' Days ' という名前を付けることができます。 1つの日だけを指定できるようにする同様の列挙には、属性は含まれず、"Day" と呼ばれることもあります。

 名前付け規則では、共通言語ランタイムをターゲットとするライブラリの統一的な名前の付け方が規定されています。 これにより、新しいソフトウェア ライブラリを習得するまでの時間を短縮でき、マネージド コード開発の専門家によってライブラリが開発されたという信頼を顧客に与えることができます。

## <a name="how-to-fix-violations"></a>違反の修正方法
 列挙型の名前を複数形にすることも、複数の列挙値を同時に指定しない場合は属性を削除することもでき <xref:System.FlagsAttribute> ます。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 名前が複数形の単語であっても、の末尾がではない場合、違反を抑制するのは安全です。 たとえば、前述の複数日間の列挙に ' DaysOfTheWeek ' という名前が付けられている場合、ルールのロジックに違反することになりますが、その目的は違反になります。 このような違反は suppressd にする必要があります。

## <a name="related-rules"></a>関連規則
 [CA1027:列挙型を FlagsAttribute に設定します](../code-quality/ca1027-mark-enums-with-flagsattribute.md)

 [CA2217:列挙型を FlagsAttribute に設定しません](../code-quality/ca2217-do-not-mark-enums-with-flagsattribute.md)

## <a name="see-also"></a>関連項目
 <xref:System.FlagsAttribute?displayProperty=fullName>[列挙型のデザイン](https://msdn.microsoft.com/library/dd53c952-9d9a-4736-86ff-9540e815d545)
