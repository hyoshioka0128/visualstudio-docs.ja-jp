---
title: 'CA1001: 破棄可能なフィールドを所有する型は、破棄可能でなければなりません。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1001
- TypesThatOwnDisposableFieldsShouldBeDisposable
helpviewer_keywords:
- CA1001
- TypesThatOwnDisposableFieldsShouldBeDisposable
ms.assetid: c85c126c-2b16-4505-940a-b5ddf873fb22
caps.latest.revision: 23
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: dab4532f082bd81eaa7b812eb038c5957636d453
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85548318"
---
# <a name="ca1001-types-that-own-disposable-fields-should-be-disposable"></a>CA1001:破棄可能なフィールドを所有する型は、破棄可能でなければなりません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|TypesThatOwnDisposableFieldsShouldBeDisposable|
|CheckId|CA1001|
|カテゴリ|Microsoft Design|
|互換性に影響する変更点|非互換性-型がアセンブリの外部で参照できない場合。<br /><br /> 中断-型がアセンブリの外部で参照可能な場合。|

## <a name="cause"></a>原因
 クラスは、型のインスタンスフィールドを宣言して実装し <xref:System.IDisposable?displayProperty=fullName> ます。クラスはを実装しません <xref:System.IDisposable> 。

## <a name="rule-description"></a>ルールの説明
 クラスは、 <xref:System.IDisposable> 所有しているアンマネージリソースを破棄するためのインターフェイスを実装します。 型のインスタンスフィールドは <xref:System.IDisposable> 、そのフィールドがアンマネージリソースを所有していることを示します。 フィールドを宣言するクラスは、 <xref:System.IDisposable> 間接的にアンマネージリソースを所有し、インターフェイスを実装する必要があり <xref:System.IDisposable> ます。 クラスがアンマネージリソースを直接所有していない場合は、ファイナライザーを実装しないでください。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、 <xref:System.IDisposable> メソッドからを実装し、 <xref:System.IDisposable.Dispose%2A?displayProperty=fullName> <xref:System.IDisposable.Dispose%2A> フィールドのメソッドを呼び出します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。

## <a name="example"></a>例
 次の例は、規則に違反するクラスと、を実装することによって規則を満たすクラスを示して <xref:System.IDisposable> います。 クラスがアンマネージリソースを直接所有していないため、クラスはファイナライザーを実装しません。

 [!code-csharp[FxCop.Design.DisposableFields#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.DisposableFields/cs/FxCop.Design.DisposableFields.cs#1)]
 [!code-vb[FxCop.Design.DisposableFields#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.DisposableFields/vb/FxCop.Design.DisposableFields.vb#1)]

## <a name="related-rules"></a>関連規則
 [CA2213:破棄可能なフィールドは破棄されなければなりません](../code-quality/ca2213-disposable-fields-should-be-disposed.md)

 [CA2216:破棄可能な型はファイナライザーを宣言しなければなりません](../code-quality/ca2216-disposable-types-should-declare-finalizer.md)

 [CA2215:Dispose メソッドが基底クラスの Dispose を呼び出す必要があります](../code-quality/ca2215-dispose-methods-should-call-base-class-dispose.md)

 [CA1049:ネイティブ リソースを所有する型は、破棄可能でなければなりません](../code-quality/ca1049-types-that-own-native-resources-should-be-disposable.md)
