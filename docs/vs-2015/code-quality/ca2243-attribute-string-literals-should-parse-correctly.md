---
title: 'CA2243: 属性文字列リテラルは正しく解析する必要があります |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2243
- AttributeStringLiteralsShouldParseCorrectly
helpviewer_keywords:
- AttributeStringLiteralsShouldParseCorrectly
- CA2243
ms.assetid: bfadb366-379d-4ee4-b17b-c4a09bf1106b
caps.latest.revision: 12
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 09e932651576f9b6d595657ad024b8f2697ad016
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85535747"
---
# <a name="ca2243-attribute-string-literals-should-parse-correctly"></a>CA2243:属性文字列リテラルは、正しく解析する必要があります
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|アイテム|値|
|-|-|
|TypeName|AttributeStringLiteralsShouldParseCorrectly|
|CheckId|CA2243|
|カテゴリ|Microsoft. 使用方法|
|互換性に影響する変更点|中断なし|

## <a name="cause"></a>原因
 属性の文字列リテラルパラメーターは、URL、GUID、またはバージョンに対して正しく解析されません。

## <a name="rule-description"></a>ルールの説明
 属性はから派生 <xref:System.Attribute?displayProperty=fullName> しており、属性はコンパイル時に使用されるため、定数値のみをコンストラクターに渡すことができます。 Url、Guid、およびバージョンを表す必要がある属性パラメーターを、、およびとして型指定することはできません <xref:System.Uri?displayProperty=fullName> <xref:System.Guid?displayProperty=fullName> <xref:System.Version?displayProperty=fullName> 。これらの型は定数として表すことができないためです。 代わりに、文字列で表現する必要があります。

 パラメーターは文字列として型指定されるため、コンパイル時に正しく書式設定されていないパラメーターが渡される可能性があります。

 このルールでは、名前付けヒューリスティックを使用して、uniform resource identifier (URI)、グローバル一意識別子 (GUID)、またはバージョンを表すパラメーターを検索し、渡された値が正しいことを確認します。

## <a name="how-to-fix-violations"></a>違反の修正方法
 パラメーター文字列を正しい形式の URL、GUID、またはバージョンに変更してください。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 パラメーターが URL、GUID、またはバージョンを表していない場合は、この規則による警告を抑制しても安全です。

## <a name="example"></a>例
 次の例は、この規則に違反する AssemblyFileVersionAttribute のコードを示しています。

 [!code-csharp[FxCop.Usage.AttributeStringLiteralsShouldParseCorrectly#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.AttributeStringLiteralsShouldParseCorrectly/cs/FxCop.Usage.AttributeStringLiteralsShouldParseCorrectly.cs#1)]

 このルールは、次のようにトリガーされます。

- ' Version ' を含むパラメーターは、system.string に解析できません。

- ' Guid ' を含むパラメーターは、System.guid に解析できません。

- ' Uri '、' urn '、または ' url ' を含むパラメーターは、system.string に解析できません。

## <a name="see-also"></a>関連項目
 [CA1054:URI パラメーターを文字列にすることはできません](../code-quality/ca1054-uri-parameters-should-not-be-strings.md)
