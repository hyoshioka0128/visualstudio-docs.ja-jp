---
title: 'CA1710: 識別子は正しいサフィックス | を持つ必要がありますMicrosoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1710
- IdentifiersShouldHaveCorrectSuffix
helpviewer_keywords:
- IdentifiersShouldHaveCorrectSuffix
- CA1710
ms.assetid: 2b8e6dce-b4e8-4a66-ba9a-6b79be5bfe8c
caps.latest.revision: 22
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 0ee7ce7c4e9edad9d941b4a70b2a199a37130e43
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85543989"
---
# <a name="ca1710-identifiers-should-have-correct-suffix"></a>CA1710:識別子は、正しいサフィックスを含んでいなければなりません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|IdentifiersShouldHaveCorrectSuffix|
|CheckId|CA1710|
|カテゴリ|Microsoft.Naming|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 識別子のサフィックスが正しくありません。

## <a name="rule-description"></a>ルールの説明
 慣例として、特定の基本型を拡張する型、特定のインターフェイスを実装する型、またはこれらの型から派生した型の名前には、基本型またはインターフェイスに関連付けられたサフィックスがあります。

 名前付け規則では、共通言語ランタイムをターゲットとするライブラリの統一的な名前の付け方が規定されています。 これにより、新しいソフトウェア ライブラリを習得するまでの時間を短縮でき、マネージド コード開発の専門家によってライブラリが開発されたという信頼を顧客に与えることができます。

 次の表に、サフィックスが関連付けられている基本型とインターフェイスの一覧を示します。

|基本型/インターフェイス|サフィックス|
|--------------------------|------------|
|<xref:System.Attribute?displayProperty=fullName>|属性|
|<xref:System.EventArgs?displayProperty=fullName>|EventArgs|
|<xref:System.Exception?displayProperty=fullName>|例外|
|<xref:System.Collections.ICollection?displayProperty=fullName>|コレクション|
|<xref:System.Collections.IDictionary?displayProperty=fullName>|Dictionary|
|<xref:System.Collections.IEnumerable?displayProperty=fullName>|コレクション|
|<xref:System.Collections.Queue?displayProperty=fullName>|コレクションまたはキュー|
|<xref:System.Collections.Stack?displayProperty=fullName>|コレクションまたはスタック|
|<xref:System.Collections.Generic.ICollection%601?displayProperty=fullName>|コレクション|
|<xref:System.Collections.Generic.IDictionary%602?displayProperty=fullName>|Dictionary|
|<xref:System.Data.DataSet?displayProperty=fullName>|DataSet|
|<xref:System.Data.DataTable?displayProperty=fullName>|Collection または DataTable|
|<xref:System.IO.Stream?displayProperty=fullName>|ストリーム|
|<xref:System.Security.IPermission?displayProperty=fullName>|権限|
|<xref:System.Security.Policy.IMembershipCondition?displayProperty=fullName>|条件|
|イベントハンドラーデリゲート。|EventHandler|

 およびを実装する型は、 <xref:System.Collections.ICollection> ディクショナリ、スタック、キューなどの一般化された型のデータ構造体であり、その型の使用目的に関する意味のある情報を提供する名前を使用できます。

 およびを実装する型 <xref:System.Collections.ICollection> は、特定の項目のコレクションであり、"collection" という語で終わる名前を持ちます。 たとえば、オブジェクトのコレクションには <xref:System.Collections.Queue> ' QueueCollection ' という名前が付いています。 ' Collection ' サフィックスは、(の) ステートメントを使用してコレクションのメンバーを列挙できることを `foreach` `For Each` [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 示します。

 <xref:System.Collections.IDictionary>型がまたはを実装している場合でも、を実装する型の名前は、"Dictionary" で終わる名前になり <xref:System.Collections.IEnumerable> <xref:System.Collections.ICollection> ます。 ' Collection ' および ' Dictionary ' サフィックスの名前付け規則を使用すると、ユーザーは次の2つの列挙パターンを区別できます。

 ' Collection ' サフィックスを持つ型は、この列挙パターンに従います。

```
foreach(SomeType x in SomeCollection) { }
```

 ' Dictionary ' サフィックスを持つ型は、この列挙パターンに従います。

```
foreach(SomeType x in SomeDictionary.Values) { }
```

 オブジェクトは、オブジェクト <xref:System.Data.DataSet> とオブジェクトのコレクションで構成されるオブジェクトのコレクションで構成さ <xref:System.Data.DataTable> <xref:System.Data.DataColumn?displayProperty=fullName> <xref:System.Data.DataRow?displayProperty=fullName> れます。 これらのコレクション <xref:System.Collections.ICollection> は、基本クラスを介して実装さ <xref:System.Data.InternalDataCollectionBase?displayProperty=fullName> れます。

## <a name="how-to-fix-violations"></a>違反の修正方法
 型の名前を変更して、正しい語句がサフィックスとして付けられるようにします。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 型が拡張される可能性がある一般化されたデータ構造であるか、または任意の多様な項目のセットを保持する場合は、' Collection ' サフィックスを使用するように警告を抑制するのが安全です。 この場合、データ構造の実装、パフォーマンス、またはその他の特性に関する意味のある情報を提供する名前が意味を持ちます (BinaryTree など)。 型が特定の型 (たとえば、StringCollection) のコレクションを表す場合、この規則からの警告を抑制しないでください。これは、ステートメントを使用して型を列挙できることをサフィックスが示しているため `foreach` です。

 他のサフィックスについては、このルールからの警告を抑制しないでください。 サフィックスによって、型名から意図された使用法を明確にすることができます。

## <a name="related-rules"></a>関連規則
 [CA1711:識別子は、不適切なサフィックスを含むことはできません](../code-quality/ca1711-identifiers-should-not-have-incorrect-suffix.md)

## <a name="see-also"></a>参照
 [属性](https://msdn.microsoft.com/library/ee0038ef-b247-4747-a650-3c5c5cd58d8b) [NIB: イベントとデリゲート](https://msdn.microsoft.com/d98fd58b-fa4f-4598-8378-addf4355a115)
