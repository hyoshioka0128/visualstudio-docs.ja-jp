---
title: 'CA1007: 適切な場所にジェネリックを使用します。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1007
- UseGenericsWhereAppropriate
helpviewer_keywords:
- CA1007
- UseGenericsWhereAppropriate
ms.assetid: eab780ea-3b1f-4d32-b15a-5d48da2df46b
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 4ee33305c1ae0f15e5d8f390a4b65d62c87b6904
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547941"
---
# <a name="ca1007-use-generics-where-appropriate"></a>CA1007:適切な場所にジェネリックを使用します
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|UseGenericsWhereAppropriate|
|CheckId|CA1007|
|カテゴリ|Microsoft Design|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 外部から参照できるメソッドには、型の参照パラメーター <xref:System.Object?displayProperty=fullName> と、それを含むアセンブリターゲットが含まれてい [!INCLUDE[dnprdnlong](../includes/dnprdnlong-md.md)] ます。

## <a name="rule-description"></a>ルールの説明
 参照パラメーターは、 `ref` ( `ByRef` in) キーワードを使用して変更されたパラメーターです [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 。 参照パラメーターに指定する引数の型は、参照パラメーターの型と正確に一致している必要があります。 参照パラメーター型から派生した型を使用するには、最初に型をキャストし、参照パラメーター型の変数に代入する必要があります。 ジェネリックメソッドを使用すると、制約の対象となるすべての型を、最初に型を参照パラメーター型にキャストせずに、メソッドに渡すことができます。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、メソッドをジェネリックにして、 <xref:System.Object> 型パラメーターを使用してパラメーターを置き換えます。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。

## <a name="example"></a>例
 次の例は、非ジェネリックメソッドとジェネリックメソッドの両方として実装されている汎用スワップルーチンを示しています。 ジェネリックメソッドを使用して、非ジェネリックメソッドと比較して、文字列がどの程度効率的に交換されるかに注意してください。

 [!code-csharp[FxCop.Design.UseGenerics#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.UseGenerics/cs/FxCop.Design.UseGenerics.cs#1)]
 [!code-vb[FxCop.Design.UseGenerics#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.UseGenerics/vb/FxCop.Design.UseGenerics.vb#1)]

## <a name="related-rules"></a>関連規則
 [CA1005:ジェネリック型でパラメーターを使用しすぎないでください](../code-quality/ca1005-avoid-excessive-parameters-on-generic-types.md)

 [CA1010:コレクションは、ジェネリック インターフェイスを実装しなければなりません](../code-quality/ca1010-collections-should-implement-generic-interface.md)

 [CA1000:ジェネリック型の静的メンバーを宣言しません](../code-quality/ca1000-do-not-declare-static-members-on-generic-types.md)

 [CA1002:ジェネリック リストを公開しません](../code-quality/ca1002-do-not-expose-generic-lists.md)

 [CA1006:ジェネリック型をメンバー シグネチャ内で入れ子にしません](../code-quality/ca1006-do-not-nest-generic-types-in-member-signatures.md)

 [CA1004:ジェネリック メソッドは型パラメーターを指定しなければなりません](../code-quality/ca1004-generic-methods-should-provide-type-parameter.md)

 [CA1003:汎用イベント ハンドラーのインスタンスを使用します](../code-quality/ca1003-use-generic-event-handler-instances.md)

## <a name="see-also"></a>関連項目
 [ジェネリック](https://msdn.microsoft.com/library/75ea8509-a4ea-4e7a-a2b3-cf72482e9282)
