---
title: 'CA2218: オーバーライドする Equals | で GetHashCode をオーバーライドします。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2218
- OverrideGetHashCodeOnOverridingEquals
helpviewer_keywords:
- OverrideGetHashCodeOnOverridingEquals
- CA2218
ms.assetid: 69b020cd-29e8-45a6-952e-32cf3ce2e21d
caps.latest.revision: 22
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 8083edf04aa799c8031fbcd1b53a2e17104dd4a6
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85538802"
---
# <a name="ca2218-override-gethashcode-on-overriding-equals"></a>CA2218:オーバーライドする Equals で GetHashCode をオーバーライドします
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|アイテム|値|
|-|-|
|TypeName|OverrideGetHashCodeOnOverridingEquals|
|CheckId|CA2218|
|カテゴリ|Microsoft. 使用方法|
|互換性に影響する変更点|中断なし|

## <a name="cause"></a>原因
 パブリック型はを <xref:System.Object.Equals%2A?displayProperty=fullName> オーバーライドしますが、をオーバーライドしません <xref:System.Object.GetHashCode%2A?displayProperty=fullName> 。

## <a name="rule-description"></a>ルールの説明
 <xref:System.Object.GetHashCode%2A>現在のインスタンスに基づいて値を返します。これは、ハッシュアルゴリズムや、ハッシュテーブルなどのデータ構造に適しています。 2つのオブジェクトが同じ型で等しい場合は、次の型のインスタンスが正しく動作することを確認するために、同じハッシュコードを返す必要があります。

- <xref:System.Collections.Hashtable?displayProperty=fullName>

- <xref:System.Collections.SortedList?displayProperty=fullName>

- <xref:System.Collections.Generic.Dictionary%602?displayProperty=fullName>

- <xref:System.Collections.Generic.SortedDictionary%602?displayProperty=fullName>

- <xref:System.Collections.Generic.SortedList%602?displayProperty=fullName>

- <xref:System.Collections.Specialized.HybridDictionary?displayProperty=fullName>

- <xref:System.Collections.Specialized.ListDictionary?displayProperty=fullName>

- <xref:System.Collections.Specialized.OrderedDictionary?displayProperty=fullName>

- を実装する型<xref:System.Collections.Generic.IEqualityComparer%601?displayProperty=fullName>

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、の実装を提供 <xref:System.Object.GetHashCode%2A> します。 同じ型のオブジェクトのペアについては、の実装が <xref:System.Object.Equals%2A> ペアに対してを返す場合は、実装が同じ値を返すことを確認する必要があり `true` ます。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。

## <a name="class-example"></a>クラスの例

### <a name="description"></a>説明
 次の例は、この規則に違反するクラス (参照型) を示しています。

### <a name="code"></a>コード
 [!code-csharp[FxCop.Usage.GetHashCodeErrorClass#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.GetHashCodeErrorClass/cs/FxCop.Usage.GetHashCodeErrorClass.cs#1)]

### <a name="comments"></a>コメント
 次の例では、をオーバーライドすることによって違反を修正し <xref:System.Object.GetHashCode> ます。

### <a name="code"></a>コード
 [!code-csharp[FxCop.Usage.GetHashCodeFixedClass#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.GetHashCodeFixedClass/cs/FxCop.Usage.GetHashCodeFixedClass.cs#1)]

## <a name="structure-example"></a>構造体の例

### <a name="description"></a>説明
 次の例は、この規則に違反する構造体 (値型) を示しています。

### <a name="code"></a>コード
 [!code-csharp[FxCop.Usage.GetHashCodeErrorStruct#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.GetHashCodeErrorStruct/cs/FxCop.Usage.GetHashCodeErrorStruct.cs#1)]

### <a name="comments"></a>コメント
 次の例では、をオーバーライドすることによって違反を修正し <xref:System.Object.GetHashCode> ます。

### <a name="code"></a>コード
 [!code-csharp[FxCop.Usage.GetHashCodeFixedStruct#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.GetHashCodeFixedStruct/cs/FxCop.Usage.GetHashCodeFixedStruct.cs#1)]

## <a name="related-rules"></a>関連規則
 [CA1046:参照型で、演算子 equals をオーバーロードしないでください](../code-quality/ca1046-do-not-overload-operator-equals-on-reference-types.md)

 [CA2225:演算子オーバーロードには名前付けされた代替が存在します](../code-quality/ca2225-operator-overloads-have-named-alternates.md)

 [CA2226:演算子は対称型オーバーロードを含まなければなりません](../code-quality/ca2226-operators-should-have-symmetrical-overloads.md)

 [CA2224:オーバーロードする演算子 equals で Equals をオーバーライドします](../code-quality/ca2224-override-equals-on-overloading-operator-equals.md)

 [CA2231:ValueType.Equals のオーバーライドで、演算子 equals をオーバーロードします](../code-quality/ca2231-overload-operator-equals-on-overriding-valuetype-equals.md)

## <a name="see-also"></a>関連項目

- <xref:System.Object.Equals%2A?displayProperty=fullName>
- <xref:System.Object.GetHashCode%2A?displayProperty=fullName>
- <xref:System.Collections.Hashtable?displayProperty=fullName>
- [等値演算子](https://msdn.microsoft.com/library/bc496a91-fefb-4ce0-ab4c-61f09964119a)