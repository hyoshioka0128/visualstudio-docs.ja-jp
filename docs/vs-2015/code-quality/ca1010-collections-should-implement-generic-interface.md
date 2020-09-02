---
title: 'CA1010: コレクションは、ジェネリックインターフェイス | を実装する必要があります。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1010
- CollectionsShouldImplementGenericInterface
helpviewer_keywords:
- CA1010
- CollectionsShouldImplementGenericInterface
ms.assetid: c7d7126f-fa70-40be-8f93-3243e1760dc5
caps.latest.revision: 26
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: b141d755c717ad6650d2a49c98c2b26547066b7a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85545523"
---
# <a name="ca1010-collections-should-implement-generic-interface"></a>CA1010:コレクションは、ジェネリック インターフェイスを実装しなければなりません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|CollectionsShouldImplementGenericInterface|
|CheckId|CA1010|
|カテゴリ|Microsoft Design|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因
 外部から参照できる型は、インターフェイスを実装し <xref:System.Collections.IEnumerable?displayProperty=fullName> ますが、インターフェイスを実装するのではなく、 <xref:System.Collections.Generic.IEnumerable%601?displayProperty=fullName> コンテナーを対象とするアセンブリをターゲットとし [!INCLUDE[dnprdnlong](../includes/dnprdnlong-md.md)] ます。 このルールは、を実装する型を無視 <xref:System.Collections.IDictionary?displayProperty=fullName> します。

## <a name="rule-description"></a>ルールの説明
 コレクションの操作性を拡充するために、ジェネリック コレクション インターフェイスの 1 つを実装します。 次に、コレクションを使用して、次のようなジェネリックコレクション型を設定できます。

- <xref:System.Collections.Generic.List%601?displayProperty=fullName>

- <xref:System.Collections.Generic.Queue%601?displayProperty=fullName>

- <xref:System.Collections.Generic.Stack%601?displayProperty=fullName>

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、次のジェネリックコレクションインターフェイスのいずれかを実装します。

- <xref:System.Collections.Generic.IEnumerable%601?displayProperty=fullName>

- <xref:System.Collections.Generic.ICollection%601?displayProperty=fullName>

- <xref:System.Collections.Generic.IList%601?displayProperty=fullName>

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 このルールからの警告を抑制するのは安全です。ただし、コレクションの使用は制限されます。

## <a name="example-violation"></a>違反の例

### <a name="description"></a>説明
 次の例は、非ジェネリッククラスから派生したクラス (参照型) を示して `CollectionBase` います。このクラスは、この規則に違反します。

### <a name="code"></a>コード
 [!code-csharp[FxCop.Design.CollectionsGenericViolation#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.CollectionsGenericViolation/cs/FxCop.Design.CollectionsGenericViolation.cs#1)]

### <a name="comments"></a>コメント
 この違反の違反を修正するには、ジェネリックインターフェイスを実装するか、ジェネリックインターフェイスと非ジェネリックインターフェイス (クラスなど) の両方を既に実装している型に基本クラスを変更する必要があり `Collection<T>` ます。

## <a name="fix-by-base-class-change"></a>基本クラスの変更による修正

### <a name="description"></a>説明
 次の例では、非ジェネリック `CollectionBase` クラスからジェネリック (では) クラスにコレクションの基底クラスを変更することによって、違反を修正し `Collection<T>` `Collection(Of T)` [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] ます。

### <a name="code"></a>コード
 [!code-csharp[FxCop.Design.CollectionsGenericBase#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.CollectionsGenericBase/cs/FxCop.Design.CollectionsGenericBase.cs#1)]

### <a name="comments"></a>コメント
 既に解放されているクラスの基底クラスの変更は、既存のコンシューマーに対する重大な変更と見なされます。

## <a name="fix-by-interface-implementation"></a>インターフェイスの実装による修正

### <a name="description"></a>説明
 次の例では、これらのジェネリックインターフェイス (、、および) を実装することによって、違反を修正して `IEnumerable<T>` `ICollection<T>` `IList<T>` `IEnumerable(Of T)` `ICollection(Of T)` `IList(Of T)` [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] います。

### <a name="code"></a>コード
 [!code-csharp[FxCop.Design.CollectionsGenericInterface#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.CollectionsGenericInterface/cs/FxCop.Design.CollectionsGenericInterface.cs#1)]

## <a name="related-rules"></a>関連規則
 [CA1005:ジェネリック型でパラメーターを使用しすぎないでください](../code-quality/ca1005-avoid-excessive-parameters-on-generic-types.md)

 [CA1000:ジェネリック型の静的メンバーを宣言しません](../code-quality/ca1000-do-not-declare-static-members-on-generic-types.md)

 [CA1002:ジェネリック リストを公開しません](../code-quality/ca1002-do-not-expose-generic-lists.md)

 [CA1006:ジェネリック型をメンバー シグネチャ内で入れ子にしません](../code-quality/ca1006-do-not-nest-generic-types-in-member-signatures.md)

 [CA1004:ジェネリック メソッドは型パラメーターを指定しなければなりません](../code-quality/ca1004-generic-methods-should-provide-type-parameter.md)

 [CA1003:汎用イベント ハンドラーのインスタンスを使用します](../code-quality/ca1003-use-generic-event-handler-instances.md)

 [CA1007:適切な場所にジェネリックを使用します](../code-quality/ca1007-use-generics-where-appropriate.md)

## <a name="see-also"></a>参照
 [ジェネリック](https://msdn.microsoft.com/library/75ea8509-a4ea-4e7a-a2b3-cf72482e9282)
