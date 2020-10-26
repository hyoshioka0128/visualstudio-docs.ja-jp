---
title: 'CA2227: コレクションプロパティは読み取り専用でなければなりません |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2227
- CollectionPropertiesShouldBeReadOnly
helpviewer_keywords:
- CA2227
- CollectionPropertiesShouldBeReadOnly
ms.assetid: 26967aaf-6fbe-438a-b4d3-ac579b5dc0f9
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 17c4e2336a5c8bd8905d857dc8189a11f9fb6181
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85540531"
---
# <a name="ca2227-collection-properties-should-be-read-only"></a>CA2227:Collection プロパティは読み取り専用でなければなりません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|CollectionPropertiesShouldBeReadOnly|
|CheckId|CA2227|
|カテゴリ|Microsoft. 使用方法|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 外部から参照できる書き込み可能プロパティは、を実装する型です <xref:System.Collections.ICollection?displayProperty=fullName> 。 配列、インデクサー (' Item ' という名前のプロパティ)、およびアクセス許可セットは、規則によって無視されます。

## <a name="rule-description"></a>ルールの説明
 書き込み可能なコレクションプロパティを使用すると、ユーザーはコレクションをまったく別のコレクションに置き換えることができます。 読み取り専用プロパティは、コレクションを置換できないようにしますが、個別のメンバーが設定されることは回避できません。 コレクションを置き換えることが目標である場合、推奨されるデザインパターンは、コレクションからすべての要素を削除するメソッドと、コレクションを再設定するメソッドを含めることです。 <xref:System.Collections.ArrayList.Clear%2A> <xref:System.Collections.ArrayList.AddRange%2A> <xref:System.Collections.ArrayList?displayProperty=fullName> このパターンの例については、クラスのメソッドとメソッドを参照してください。

 バイナリシリアル化と XML シリアル化の両方で、コレクションである読み取り専用プロパティがサポートされます。 <xref:System.Xml.Serialization.XmlSerializer?displayProperty=fullName>クラスには <xref:System.Collections.ICollection> 、 <xref:System.Collections.IEnumerable?displayProperty=fullName> シリアル化可能にするためにとを実装する型に対する特定の要件があります。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、プロパティを読み取り専用にします。デザインで必要な場合は、コレクションを消去して再設定するメソッドを追加します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。

## <a name="example"></a>例
 次の例は、書き込み可能なコレクションプロパティを持つ型を示し、コレクションを直接置換する方法を示しています。 また、メソッドとメソッドを使用して読み取り専用コレクションプロパティを置き換えることをお勧めし `Clear` `AddRange` ます。

 [!code-cpp[FxCop.Usage.PropertiesReturningCollections#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Usage.PropertiesReturningCollections/cpp/FxCop.Usage.PropertiesReturningCollections.cpp#1)]
 [!code-csharp[FxCop.Usage.PropertiesReturningCollections#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.PropertiesReturningCollections/cs/FxCop.Usage.PropertiesReturningCollections.cs#1)]
 [!code-vb[FxCop.Usage.PropertiesReturningCollections#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.PropertiesReturningCollections/vb/FxCop.Usage.PropertiesReturningCollections.vb#1)]

## <a name="related-rules"></a>関連規則
 [CA1819:プロパティは、配列を返すことはできません](../code-quality/ca1819-properties-should-not-return-arrays.md)
