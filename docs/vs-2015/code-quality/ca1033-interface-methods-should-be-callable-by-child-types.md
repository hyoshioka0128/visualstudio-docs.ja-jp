---
title: 'CA1033: インターフェイスメソッドは、子の型によって呼び出し可能でなければなりません |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- InterfaceMethodsShouldBeCallableByChildTypes
- CA1033
helpviewer_keywords:
- CA1033
- InterfaceMethodsShouldBeCallableByChildTypes
ms.assetid: 9f171497-a5e3-4769-a77b-7aed755b2662
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 18629f8d5c63b652d6539db10c6e6dba5d621c24
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85542299"
---
# <a name="ca1033-interface-methods-should-be-callable-by-child-types"></a>CA1033:インターフェイス メソッドは、子型によって呼び出し可能でなければなりません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|InterfaceMethodsShouldBeCallableByChildTypes|
|CheckId|CA1033|
|カテゴリ|Microsoft Design|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因
 シールされていない外部から参照できる型によって、パブリック インターフェイスを持つメソッドを明示的に実装しています。また、同じ名前を持つ外部から参照できる代替のメソッドがありません。

## <a name="rule-description"></a>ルールの説明
 パブリックインターフェイスメソッドを明示的に実装する基本型について考えてみます。 基本型から派生した型は、 `this` インターフェイスにキャストされている現在のインスタンス (C# の場合) への参照によってのみ、継承されたインターフェイスメソッドにアクセスできます。 派生型が継承されたインターフェイスメソッドを再実装 (明示的に) すると、基本実装にアクセスできなくなります。 現在のインスタンス参照を使用して呼び出すと、派生した実装が呼び出されます。これにより、再帰と最終的なスタックオーバーフローが発生します。

 この規則は、 <xref:System.IDisposable.Dispose%2A?displayProperty=fullName> 外部から参照可能な `Close()` または `System.IDisposable.Dispose(Boolean)` メソッドが指定されている場合に、の明示的な実装に対する違反を報告しません。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、同じ機能を公開し、派生型から参照できるようにするか、または非明示的な実装に変更する新しいメソッドを実装します。 互換性に影響する変更が許容される場合、別の方法として、型をシールする方法があります。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 外部から参照可能なメソッドが提供されていても、明示的に実装されたメソッドとは異なる名前を持つ場合は、この規則による警告を抑制することが安全です。

## <a name="example"></a>例
 次の例は、 `ViolatingBase` 規則に違反する型と、 `FixedBase` 違反の修正を示す型を示しています。

 [!code-csharp[FxCop.Design.ExplicitMethodImplementations#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.ExplicitMethodImplementations/cs/FxCop.Design.ExplicitMethodImplementations.cs#1)]

## <a name="see-also"></a>関連項目
 [インターフェイス](https://msdn.microsoft.com/library/2feda177-ce11-432d-81b4-d50f5f35fd37)
