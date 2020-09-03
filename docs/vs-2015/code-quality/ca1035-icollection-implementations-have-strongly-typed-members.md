---
title: 'CA1035: ICollection の実装に厳密に型指定されたメンバー |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- ICollectionImplementationsHaveStronglyTypedMembers
- CA1035
helpviewer_keywords:
- CA1035
- ICollectionImplementationsHaveStronglyTypedMembers
ms.assetid: ad404eb5-cf6a-44b7-b78a-8ebfb654bc7f
caps.latest.revision: 18
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 2e679fb3cc62ba80cfb7b56dfd7fa6590375565e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85546615"
---
# <a name="ca1035-icollection-implementations-have-strongly-typed-members"></a>CA1035:ICollection の実装は、厳密に型指定されたメンバーを含んでいます
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|ICollectionImplementationsHaveStronglyTypedMembers|
|CheckId|CA1035|
|カテゴリ|Microsoft Design|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 パブリック型またはプロテクト型は <xref:System.Collections.ICollection?displayProperty=fullName> を実装しますが、には厳密に型指定されたメソッドを提供しません <xref:System.Collections.ICollection.CopyTo%2A?displayProperty=fullName> 。 の厳密に型指定されたバージョンは、 <xref:System.Collections.ICollection.CopyTo%2A> 2 つのパラメーターを受け取る必要があり、 <xref:System.Array?displayProperty=fullName> <xref:System.Object?displayProperty=fullName> 最初のパラメーターとしてまたはの配列を持つことはできません。

## <a name="rule-description"></a>ルールの説明
 この規則 <xref:System.Collections.ICollection> <xref:System.Object> では、インターフェイスによって提供される機能を使用するときに、ユーザーが引数を型にキャストする必要がないように、厳密に型指定されたメンバーを実装する必要があります。 この規則は、を実装する型が、 <xref:System.Collections.ICollection> より強力な型のインスタンスのコレクションを管理するためにそれを行うことを前提としてい <xref:System.Object> ます。

 <xref:System.Collections.ICollection> では、<xref:System.Collections.IEnumerable?displayProperty=fullName> インターフェイスを実装します。 コレクション内のオブジェクトがを拡張 <xref:System.ValueType?displayProperty=fullName> する場合は、 <xref:System.Collections.IEnumerable.GetEnumerator%2A> ボックス化によって発生するパフォーマンスの低下を回避するために、厳密に型指定されたメンバーをに提供する必要があります。 コレクションのオブジェクトが参照型である場合、これは必要ありません。

 インターフェイスメンバーの厳密に型指定されたバージョンを実装するには、のように、形式の名前を使用してインターフェイスメンバーを明示的に実装し `InterfaceName.InterfaceMemberName` <xref:System.Collections.ICollection.CopyTo%2A> ます。 明示的なインターフェイスメンバーは、インターフェイスによって宣言されたデータ型を使用します。 などのインターフェイスメンバー名を使用して、厳密に型指定されたメンバーを実装し <xref:System.Collections.ICollection.CopyTo%2A> ます。 厳密に型指定されたメンバーをパブリックとして宣言し、コレクションによって管理される厳密な型のパラメーターと戻り値を宣言します。 厳密な型は、 <xref:System.Object> <xref:System.Array> インターフェイスによって宣言されているやなどの弱い型を置き換えます。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、インターフェイスメンバーを明示的に実装します (として宣言し <xref:System.Collections.ICollection.CopyTo%2A> ます)。 として宣言された、厳密に型指定されたパブリックメンバーを追加 `CopyTo` し、その最初のパラメーターとして厳密に型指定された配列を取得します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 バイナリツリーなどの新しいオブジェクトベースのコレクションを実装する場合、この規則からの警告を抑制します。新しいコレクションを拡張する型は、厳密な型を決定します。 これらの型は、この規則に準拠し、厳密に型指定されたメンバーを公開する必要があります。

## <a name="example"></a>例
 次の例は、を実装する正しい方法を示して <xref:System.Collections.ICollection> います。

 [!code-csharp[FxCop.Design.ICollectionStrongTypes#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.ICollectionStrongTypes/cs/FxCop.Design.ICollectionStrongTypes.cs#1)]

## <a name="related-rules"></a>関連規則
 [CA1038:列挙子は厳密に型指定されていなければなりません](../code-quality/ca1038-enumerators-should-be-strongly-typed.md)

 [CA1039:リストは厳密に型指定されています](../code-quality/ca1039-lists-are-strongly-typed.md)

## <a name="see-also"></a>参照
 <xref:System.Array?displayProperty=fullName> <xref:System.Collections.IEnumerable?displayProperty=fullName>
 <xref:System.Collections.ICollection?displayProperty=fullName>
 <xref:System.Object?displayProperty=fullName>
