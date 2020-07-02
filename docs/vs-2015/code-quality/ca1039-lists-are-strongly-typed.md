---
title: 'CA1039: リストは厳密に型指定されています |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1039
- ListsAreStronglyTyped
helpviewer_keywords:
- CA1039
- ListsAreStronglyTyped
ms.assetid: 5ac366c4-fd87-4d5c-95d5-f755510c8e5c
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 4e485375c12564b5416c79bd3a41dedb1da76dc0
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85533446"
---
# <a name="ca1039-lists-are-strongly-typed"></a>CA1039:リストは厳密に型指定されています
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|アイテム|値|
|-|-|
|TypeName|ListsAreStronglyTyped|
|CheckId|CA1039|
|カテゴリ|Microsoft Design|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 パブリック型またはプロテクト型はを実装し <xref:System.Collections.IList?displayProperty=fullName> ますが、次の1つまたは複数に対して厳密に型指定されたメソッドを提供しません。

- IList。項目

- IList. 追加

- IList. Contains

- IList. IndexOf

- IList。挿入

- IList。削除

## <a name="rule-description"></a>ルールの説明
 この規則 <xref:System.Collections.IList> <xref:System.Object?displayProperty=fullName> では、インターフェイスによって提供される機能を使用するときに、ユーザーが引数を型にキャストする必要がないように、厳密に型指定されたメンバーを実装する必要があります。 インターフェイスは、 <xref:System.Collections.IList> インデックスによってアクセスできるオブジェクトのコレクションによって実装されます。 この規則は、を実装する型が、 <xref:System.Collections.IList> よりも強力な型のインスタンスのコレクションを管理するためにこれを行うことを前提としてい <xref:System.Object> ます。

 <xref:System.Collections.IList><xref:System.Collections.ICollection?displayProperty=fullName>インターフェイスおよびインターフェイスを実装し <xref:System.Collections.IEnumerable?displayProperty=fullName> ます。 を実装する場合は <xref:System.Collections.IList> 、に必要な厳密に型指定されたメンバーを指定する必要があり <xref:System.Collections.ICollection> ます。 コレクション内のオブジェクトがを拡張 <xref:System.ValueType?displayProperty=fullName> する場合、ボックス化によって発生するパフォーマンスの低下を回避するために、に厳密に型指定されたメンバーを指定する必要があります <xref:System.Collections.IEnumerable.GetEnumerator%2A> 。これは、コレクションのオブジェクトが参照型である場合には必要ありません。

 この規則に準拠するには、InterfaceName の形式の名前 (など) を使用して、インターフェイスメンバーを明示的に実装します。 <xref:System.Collections.IList.Add%2A> 明示的なインターフェイスメンバーは、インターフェイスによって宣言されたデータ型を使用します。 などのインターフェイスメンバー名を使用して、厳密に型指定されたメンバーを実装し `Add` ます。 厳密に型指定されたメンバーをパブリックとして宣言し、コレクションによって管理される厳密な型のパラメーターと戻り値を宣言します。 厳密な型は、 <xref:System.Object> <xref:System.Array> インターフェイスによって宣言されているやなどの弱い型を置き換えます。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、明示的に <xref:System.Collections.IList> メンバーを実装し、前にメモしたメンバーに対して厳密に型指定された代替手段を提供します。 インターフェイスを正しく実装し、 <xref:System.Collections.IList> 必要な厳密に型指定されたメンバーを提供するコードについては、次の例を参照してください。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 リンクリストなど、新しいオブジェクトベースのコレクションを実装する場合、この規則からの警告を抑制します。新しいコレクションを拡張する型は、厳密な型を決定します。 これらの型は、この規則に準拠し、厳密に型指定されたメンバーを公開する必要があります。

## <a name="example"></a>例
 次の例では、厳密に型指定されたすべてのコレクションについて、型が `YourType` を拡張し <xref:System.Collections.CollectionBase?displayProperty=fullName> ています。 では、 <xref:System.Collections.CollectionBase> インターフェイスの明示的な実装が提供されることに注意して <xref:System.Collections.IList> ください。 したがって、との厳密に型指定されたメンバーのみを指定する必要があり <xref:System.Collections.IList> <xref:System.Collections.ICollection> ます。

 [!code-csharp[FxCop.Design.IListStrongTypes#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.IListStrongTypes/cs/FxCop.Design.IListStrongTypes.cs#1)]

## <a name="related-rules"></a>関連規則
 [CA1035:ICollection の実装は、厳密に型指定されたメンバーを含んでいます](../code-quality/ca1035-icollection-implementations-have-strongly-typed-members.md)

 [CA1038:列挙子は厳密に型指定されていなければなりません](../code-quality/ca1038-enumerators-should-be-strongly-typed.md)

## <a name="see-also"></a>関連項目
 <xref:System.Collections.CollectionBase?displayProperty=fullName> <xref:System.Collections.ICollection?displayProperty=fullName>
 <xref:System.Collections.IEnumerable?displayProperty=fullName>
 <xref:System.Collections.IList?displayProperty=fullName>
 <xref:System.Object?displayProperty=fullName>
