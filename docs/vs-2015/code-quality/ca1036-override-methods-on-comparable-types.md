---
title: 'CA1036: 比較可能な型のメソッドをオーバーライドします |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1036
- OverrideMethodsOnComparableTypes
helpviewer_keywords:
- OverrideMethodsOnComparableTypes
- CA1036
ms.assetid: 2329f844-4cb8-426d-bee2-cd065d1346d0
caps.latest.revision: 23
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 52247c9175b22d3d96aa91557ee133f37c55e789
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85546602"
---
# <a name="ca1036-override-methods-on-comparable-types"></a>CA1036:比較可能な型でメソッドをオーバーライドします
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|OverrideMethodsOnComparableTypes|
|CheckId|CA1036|
|カテゴリ|Microsoft Design|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因
 パブリック型またはプロテクト型が <xref:System.IComparable?displayProperty=fullName> インターフェイスを実装していますが、オーバーライドされていないか、またはをオーバーライドしていないか、またはより大きいか、またはを超えてい <xref:System.Object.Equals%2A?displayProperty=fullName> ます。 型がインターフェイスの実装のみを継承する場合、規則は違反を報告しません。

## <a name="rule-description"></a>ルールの説明
 カスタム並べ替え順序を定義する型は、インターフェイスを実装し <xref:System.IComparable> ます。 メソッドは、 <xref:System.IComparable.CompareTo%2A> 型の2つのインスタンスの正しい並べ替え順序を示す整数値を返します。 このルールは、並べ替え順序を設定する型を識別します。これは、等値、非等値、より小さい、およびより大きいという通常の意味が適用されないことを意味します。 の実装を提供する場合は <xref:System.IComparable> 、通常、 <xref:System.Object.Equals%2A> と一致する値を返すようにをオーバーライドする必要もあり <xref:System.IComparable.CompareTo%2A> ます。 <xref:System.Object.Equals%2A>をオーバーライドし、演算子のオーバーロードをサポートする言語でコーディングする場合は、と一致する演算子も指定する必要があり <xref:System.Object.Equals%2A> ます。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、をオーバーライド <xref:System.Object.Equals%2A> します。 プログラミング言語で演算子のオーバーロードがサポートされている場合は、次の演算子を指定します。

- op_Equality

- op_Inequality

- op_LessThan

- op_GreaterThan

  C# では、これらの演算子を表すために使用されるトークンは、= =、! =、のように \<, and > なります。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 演算子が不足していることが原因で違反が発生し、プログラミング言語で演算子のオーバーロードがサポートされていない場合に、この規則からの警告を抑制するのは安全です。これは Visual Basic .NET の場合と同様です。 また、演算子の実装がアプリケーションコンテキストで意味を持たないと判断した場合、op_Equality 以外の等値演算子でこの規則を使用した場合の警告を抑制することも安全です。 ただし、Object.equals をオーバーライドする場合は、常に op_Equality と = = 演算子を使用する必要があります。

## <a name="example"></a>例
 次の例には、を正しく実装する型が含まれてい <xref:System.IComparable> ます。 コードコメントは、およびインターフェイスに関連するさまざまな規則を満たすメソッドを識別し <xref:System.Object.Equals%2A> <xref:System.IComparable> ます。

 [!code-csharp[FxCop.Design.IComparable#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.IComparable/cs/FxCop.Design.IComparable.cs#1)]

## <a name="example"></a>例
 次のアプリケーションは、 <xref:System.IComparable> 前に示した実装の動作をテストします。

 [!code-csharp[FxCop.Design.TestIComparable#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.TestIComparable/cs/FxCop.Design.TestIComparable.cs#1)]

## <a name="see-also"></a>参照
 <xref:System.IComparable?displayProperty=fullName> <xref:System.Object.Equals%2A?displayProperty=fullName>
 [等値演算子](https://msdn.microsoft.com/library/bc496a91-fefb-4ce0-ab4c-61f09964119a)
