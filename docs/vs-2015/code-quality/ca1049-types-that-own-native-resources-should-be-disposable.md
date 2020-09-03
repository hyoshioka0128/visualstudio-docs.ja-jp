---
title: 'CA1049: ネイティブリソースを所有する型は、破棄可能である必要があります |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1049
- TypesThatOwnNativeResourcesShouldBeDisposable
helpviewer_keywords:
- TypesThatOwnNativeResourcesShouldBeDisposable
- CA1049
ms.assetid: 084e587d-0e45-4092-b767-49eed30d6a35
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 49c56b98e3be01675c2c21cd11c2961dd75f4877
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85546810"
---
# <a name="ca1049-types-that-own-native-resources-should-be-disposable"></a>CA1049:ネイティブ リソースを所有する型は、破棄可能でなければなりません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|TypesThatOwnNativeResourcesShouldBeDisposable|
|CheckId|CA1049|
|カテゴリ|Microsoft Design|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因
 型がフィールド、 <xref:System.IntPtr?displayProperty=fullName> <xref:System.UIntPtr?displayProperty=fullName> フィールド、またはフィールドを参照し <xref:System.Runtime.InteropServices.HandleRef?displayProperty=fullName> ていますが、を実装していません <xref:System.IDisposable?displayProperty=fullName> 。

## <a name="rule-description"></a>ルールの説明
 この規則は <xref:System.IntPtr> 、、 <xref:System.UIntPtr> 、の <xref:System.Runtime.InteropServices.HandleRef> 各フィールドがアンマネージリソースへのポインターを格納していることを前提としています。 アンマネージリソースを割り当てる型は、を実装して <xref:System.IDisposable> 、呼び出し元が必要に応じてリソースを解放し、リソースを保持するオブジェクトの有効期間を短縮できるようにする必要があります。

 アンマネージリソースをクリーンアップするために推奨される設計パターンは、メソッドとメソッドを使用して、これらのリソースを解放するための暗黙的な方法と明示的な手段の両方を提供することです <xref:System.Object.Finalize%2A?displayProperty=fullName> <xref:System.IDisposable.Dispose%2A?displayProperty=fullName> 。 ガベージコレクターは、 <xref:System.Object.Finalize%2A> オブジェクトが到達できなくなったと判断した後、一定の時間内にオブジェクトのメソッドを呼び出します。 が呼び出された後 <xref:System.Object.Finalize%2A> 、オブジェクトを解放するには、追加のガベージコレクションが必要です。 <xref:System.IDisposable.Dispose%2A>メソッドを使用すると、呼び出し元は、リソースがガベージコレクターに残されている場合に解放されるより前に、リソースを明示的に解放することができます。 アンマネージリソースをクリーンアップした後、はメソッドを呼び出して、 <xref:System.IDisposable.Dispose%2A> <xref:System.GC.SuppressFinalize%2A?displayProperty=fullName> 呼び出しが不要になったことをガベージコレクターに知らせる必要があります。これにより、追加のガベージコレクションが不要になり、 <xref:System.Object.Finalize%2A> オブジェクトの有効期間が短縮されます。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、を実装 <xref:System.IDisposable> します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 型がアンマネージリソースを参照していない場合は、この規則からの警告を抑制することが安全です。 それ以外の場合は、実装に失敗する <xref:System.IDisposable> と、アンマネージリソースが使用できなくなったり、使用できなくなったりする可能性があるため、この規則による警告は抑制しないでください。

## <a name="example"></a>例
 次の例は、 <xref:System.IDisposable> アンマネージリソースをクリーンアップするためにを実装する型を示しています。

 [!code-csharp[FxCop.Design.UnmanagedResources#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.UnmanagedResources/cs/FxCop.Design.UnmanagedResources.cs#1)]
 [!code-vb[FxCop.Design.UnmanagedResources#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.UnmanagedResources/vb/FxCop.Design.UnmanagedResources.vb#1)]

## <a name="related-rules"></a>関連規則
 [CA2115:ネイティブ リソースを使用しているときには GC.KeepAlive を呼び出します](../code-quality/ca2115-call-gc-keepalive-when-using-native-resources.md)

 [CA1816:GC.SuppressFinalize を正しく呼び出します](../code-quality/ca1816-call-gc-suppressfinalize-correctly.md)

 [CA2216:破棄可能な型はファイナライザーを宣言しなければなりません](../code-quality/ca2216-disposable-types-should-declare-finalizer.md)

 [CA1001:破棄可能なフィールドを所有する型は、破棄可能でなければなりません](../code-quality/ca1001-types-that-own-disposable-fields-should-be-disposable.md)

## <a name="see-also"></a>参照
  [Dispose パターン](https://msdn.microsoft.com/library/31a6c13b-d6a2-492b-9a9f-e5238c983bcb)
