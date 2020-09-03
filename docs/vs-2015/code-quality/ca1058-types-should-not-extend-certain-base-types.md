---
title: 'CA1058: 型は、特定の基本型を拡張することはできません |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- TypesShouldNotExtendCertainBaseTypes
- CA1058
helpviewer_keywords:
- CA1058
- TypesShouldNotExtendCertainBaseTypes
ms.assetid: 8446ee40-beb1-49fa-8733-4d8e813471c0
caps.latest.revision: 26
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: d8e267b1e6203759efc91936a3b13059368a3862
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85545393"
---
# <a name="ca1058-types-should-not-extend-certain-base-types"></a>CA1058:型は、一定の基本型を拡張することはできません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|TypesShouldNotExtendCertainBaseTypes|
|CheckId|CA1058|
|カテゴリ|Microsoft Design|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 外部から参照可能な型では、特定の基本型が拡張されます。 現在、このルールは、次の型から派生した型を報告します。

- <xref:System.ApplicationException?displayProperty=fullName>

- <xref:System.Xml.XmlDocument?displayProperty=fullName>

- <xref:System.Collections.CollectionBase?displayProperty=fullName>

- <xref:System.Collections.DictionaryBase?displayProperty=fullName>

- <xref:System.Collections.Queue?displayProperty=fullName>

- <xref:System.Collections.ReadOnlyCollectionBase?displayProperty=fullName>

- <xref:System.Collections.SortedList?displayProperty=fullName>

- <xref:System.Collections.Stack?displayProperty=fullName>

## <a name="rule-description"></a>ルールの説明
 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]バージョン1では、から新しい例外を派生させることをお勧めしました <xref:System.ApplicationException> 。 推奨事項が変更され、新しい例外は <xref:System.Exception?displayProperty=fullName> 、名前空間のまたはそのサブクラスの1つから派生する必要があり <xref:System> ます。

 <xref:System.Xml.XmlDocument>基になるオブジェクトモデルまたはデータソースの XML ビューを作成する場合は、のサブクラスを作成しないでください。

### <a name="non-generic-collections"></a>非ジェネリックコレクション
 可能な限り、ジェネリックコレクションを使用するか、拡張します。 以前に配布していない限り、コード内の非ジェネリックコレクションは拡張しないでください。

 **不適切な使用例**

```csharp
public class MyCollection : CollectionBase
{
}

public class MyReadOnlyCollection : ReadOnlyCollectionBase
{
}
```

 **正しい使用例**

```csharp
public class MyCollection : Collection<T>
{
}

public class MyReadOnlyCollection : ReadOnlyCollection<T>
{
}
```

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、別の基本データ型またはジェネリックコレクションから型を派生させます。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 の違反については、この規則による警告を抑制しないで <xref:System.ApplicationException> ください。 の違反については、この規則による警告を抑制することが安全です <xref:System.Xml.XmlDocument> 。 以前にコードがリリースされた場合、非ジェネリックコレクションに関する警告を抑制するのは安全です。
