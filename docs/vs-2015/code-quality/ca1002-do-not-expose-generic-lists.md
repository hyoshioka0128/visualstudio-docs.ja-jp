---
title: 'CA1002: ジェネリックリストを公開しません |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- DoNotExposeGenericLists
- CA1002
helpviewer_keywords:
- CA1002
- DoNotExposeGenericLists
ms.assetid: 5caac810-1a79-47df-a27b-c46c5040bf34
caps.latest.revision: 22
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 6fcc4ae2a07eb7b1f155d6c65020e2c1a9ddc9f2
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546849"
---
# <a name="ca1002-do-not-expose-generic-lists"></a>CA1002:ジェネリック リストを公開しません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|DoNotExposeGenericLists|
|CheckId|CA1002|
|カテゴリ|Microsoft Design|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 型に、外部から参照できるメンバーが含まれています。このメンバーは型である <xref:System.Collections.Generic.List%601?displayProperty=fullName> か、型を返し <xref:System.Collections.Generic.List%601?displayProperty=fullName> ます。または、署名にパラメーターが含まれてい <xref:System.Collections.Generic.List%601?displayProperty=fullName> ます。

## <a name="rule-description"></a>ルールの説明
 <xref:System.Collections.Generic.List%601?displayProperty=fullName>は、パフォーマンスを目的として設計され、継承されないジェネリックコレクションです。 <xref:System.Collections.Generic.List%601?displayProperty=fullName>には、継承されたクラスの動作を簡単に変更できる仮想メンバーが含まれていません。 次のジェネリックコレクションは継承用に設計されているため、ではなく公開する必要があり <xref:System.Collections.Generic.List%601?displayProperty=fullName> ます。

- <xref:System.Collections.ObjectModel.Collection%601?displayProperty=fullName>

- <xref:System.Collections.ObjectModel.ReadOnlyCollection%601?displayProperty=fullName>

- <xref:System.Collections.ObjectModel.KeyedCollection%602?displayProperty=fullName>

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、 <xref:System.Collections.Generic.List%601?displayProperty=fullName> 型を継承用に設計されたジェネリックコレクションのいずれかに変更します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この警告を発生させるアセンブリが再利用可能なライブラリではない場合を除き、この規則からの警告を抑制しないでください。 たとえば、汎用リストを使用してパフォーマンスを向上させたパフォーマンスチューニングアプリケーションでは、この警告を抑制するのが安全です。

## <a name="related-rules"></a>関連規則
 [CA1005:ジェネリック型でパラメーターを使用しすぎないでください](../code-quality/ca1005-avoid-excessive-parameters-on-generic-types.md)

 [CA1010:コレクションは、ジェネリック インターフェイスを実装しなければなりません](../code-quality/ca1010-collections-should-implement-generic-interface.md)

 [CA1000:ジェネリック型の静的メンバーを宣言しません](../code-quality/ca1000-do-not-declare-static-members-on-generic-types.md)

 [CA1006:ジェネリック型をメンバー シグネチャ内で入れ子にしません](../code-quality/ca1006-do-not-nest-generic-types-in-member-signatures.md)

 [CA1004:ジェネリック メソッドは型パラメーターを指定しなければなりません](../code-quality/ca1004-generic-methods-should-provide-type-parameter.md)

 [CA1003:汎用イベント ハンドラーのインスタンスを使用します](../code-quality/ca1003-use-generic-event-handler-instances.md)

 [CA1007:適切な場所にジェネリックを使用します](../code-quality/ca1007-use-generics-where-appropriate.md)

## <a name="see-also"></a>関連項目
 [ジェネリック](https://msdn.microsoft.com/library/75ea8509-a4ea-4e7a-a2b3-cf72482e9282)
