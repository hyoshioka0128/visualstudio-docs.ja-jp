---
title: 'CA1038: 列挙子は厳密に型指定する必要があります |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- EnumeratorsShouldBeStronglyTyped
- CA1038
helpviewer_keywords:
- EnumeratorsShouldBeStronglyTyped
- CA1038
ms.assetid: 8919f526-d487-42a4-87dc-2b2ee25260c4
caps.latest.revision: 18
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: e660b1af58dca8d0d69ce2844076382c4a5a1f12
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85548266"
---
# <a name="ca1038-enumerators-should-be-strongly-typed"></a>CA1038:列挙子は厳密に型指定されていなければなりません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|EnumeratorsShouldBeStronglyTyped|
|CheckId|CA1038|
|カテゴリ|Microsoft Design|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 パブリック型またはプロテクト型はを実装し <xref:System.Collections.IEnumerator?displayProperty=fullName> ますが、厳密に型指定されたバージョンのプロパティは提供しません <xref:System.Collections.IEnumerator.Current%2A?displayProperty=fullName> 。 次の型から派生した型は、この規則から除外されます。

- <xref:System.Collections.CollectionBase?displayProperty=fullName>

- <xref:System.Collections.DictionaryBase?displayProperty=fullName>

- <xref:System.Collections.ReadOnlyCollectionBase?displayProperty=fullName>

## <a name="rule-description"></a>ルールの説明
 この規則 <xref:System.Collections.IEnumerator> <xref:System.Collections.IEnumerator.Current%2A> では、インターフェイスによって提供される機能を使用するときに、ユーザーが戻り値を厳密な型にキャストする必要がないように、厳密に型指定されたバージョンのプロパティも実装する必要があります。 この規則は、を実装する型に、 <xref:System.Collections.IEnumerator> よりも強力な型のインスタンスのコレクションが含まれていることを前提としてい <xref:System.Object> ます。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、インターフェイスプロパティを明示的に実装します (として宣言し `IEnumerator.Current` ます)。 として宣言されたプロパティの、厳密に型指定されたパブリックバージョンを追加 `Current` し、厳密に型指定されたオブジェクトを返すようにします。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 オブジェクトベースのコレクション (バイナリツリーなど) で使用するオブジェクトベースの列挙子を実装する場合は、この規則からの警告を非表示にします。 新しいコレクションを拡張する型は、厳密に型指定された列挙子を定義し、厳密に型指定されたプロパティを公開します。

## <a name="example"></a>例
 次の例は、厳密に型指定された型を実装する正しい方法を示して <xref:System.Collections.IEnumerator> います。

 [!code-csharp[FxCop.Design.IEnumeratorStrongTypes#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.IEnumeratorStrongTypes/cs/FxCop.Design.IEnumeratorStrongTypes.cs#1)]

## <a name="related-rules"></a>関連規則
 [CA1035:ICollection の実装は、厳密に型指定されたメンバーを含んでいます](../code-quality/ca1035-icollection-implementations-have-strongly-typed-members.md)

 [CA1039:リストは厳密に型指定されています](../code-quality/ca1039-lists-are-strongly-typed.md)

## <a name="see-also"></a>参照
 <xref:System.Collections.IEnumerator?displayProperty=fullName> <xref:System.Collections.CollectionBase?displayProperty=fullName>
 <xref:System.Collections.DictionaryBase?displayProperty=fullName>
 <xref:System.Collections.ReadOnlyCollectionBase?displayProperty=fullName>
