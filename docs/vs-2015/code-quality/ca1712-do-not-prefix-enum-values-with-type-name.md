---
title: 'CA1712: 型 name | の列挙値にプレフィックスを付けることはできませんMicrosoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1712
- DoNotPrefixEnumValuesWithTypeName
helpviewer_keywords:
- CA1712
- DoNotPrefixEnumValuesWithTypeName
ms.assetid: df0e3a12-67bf-48f1-a10b-2ef60484a5c7
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 4773a34ab7112434813990b4d25cbeeb865f3a08
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85543898"
---
# <a name="ca1712-do-not-prefix-enum-values-with-type-name"></a>CA1712:列挙型値を型名のプレフィックスにしません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|DoNotPrefixEnumValuesWithTypeName|
|CheckId|CA1712|
|カテゴリ|Microsoft.Naming|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 列挙体には、列挙体の型名で始まる名前を持つメンバーが含まれています。

## <a name="rule-description"></a>ルールの説明
 型情報は開発ツールによって提供されることが予想されるため、列挙型メンバーの名前の前には型名が付けられません。

 名前付け規則では、共通言語ランタイムをターゲットとするライブラリの統一的な名前の付け方が規定されています。 これにより、で新しいソフトウェアライブラリを学習するために必要な時間が短縮され、マネージコードの開発に関する専門知識を持つユーザーがライブラリを開発したことによる信頼度が向上します。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、列挙体メンバーから型名のプレフィックスを削除します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。

## <a name="example"></a>例
 次の例では、間違った名前を付けた列挙型の後に修正後のバージョンを示します。

 [!code-cpp[FxCop.Naming.EnumValues#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Naming.EnumValues/cpp/FxCop.Naming.EnumValues.cpp#1)]
 [!code-csharp[FxCop.Naming.EnumValues#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Naming.EnumValues/cs/FxCop.Naming.EnumValues.cs#1)]
 [!code-vb[FxCop.Naming.EnumValues#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Naming.EnumValues/vb/FxCop.Naming.EnumValues.vb#1)]

## <a name="related-rules"></a>関連規則
 [CA1711:識別子は、不適切なサフィックスを含むことはできません](../code-quality/ca1711-identifiers-should-not-have-incorrect-suffix.md)

 [CA1027:列挙型を FlagsAttribute に設定します](../code-quality/ca1027-mark-enums-with-flagsattribute.md)

 [CA2217:列挙型を FlagsAttribute に設定しません](../code-quality/ca2217-do-not-mark-enums-with-flagsattribute.md)

## <a name="see-also"></a>関連項目
 <xref:System.Enum?displayProperty=fullName>
