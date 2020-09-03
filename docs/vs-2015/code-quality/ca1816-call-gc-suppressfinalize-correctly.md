---
title: 'CA1816: GC を呼び出します。Gc.suppressfinalize を正しく |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1816
- DisposeMethodsShouldCallSuppressFinalize
helpviewer_keywords:
- DisposeMethodsShouldCallSuppressFinalize
- CA1816
ms.assetid: 47915fbb-103f-4333-b157-1da16bf49660
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 532478a8d6ed6b88347d196b4a74b6f19a38ef85
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85546771"
---
# <a name="ca1816-call-gcsuppressfinalize-correctly"></a>CA1816:GC.SuppressFinalize を正しく呼び出します
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|CallGCSuppressFinalizeCorrectly|
|CheckId|CA1816|
|カテゴリ|Microsoft. 使用法|
|互換性に影響する変更点|中断なし|

## <a name="cause"></a>原因

- の実装であるメソッドは、を <xref:System.IDisposable.Dispose%2A?displayProperty=fullName> 呼び出しません <xref:System.GC.SuppressFinalize%2A?displayProperty=fullName> 。

- 呼び出しの実装ではないメソッド <xref:System.IDisposable.Dispose%2A?displayProperty=fullName> <xref:System.GC.SuppressFinalize%2A?displayProperty=fullName> 。

- メソッドが <xref:System.GC.SuppressFinalize%2A?displayProperty=fullName> を呼び出し、この以外のものを渡しています (Visual Basic)。

## <a name="rule-description"></a>ルールの説明
 メソッドは、 <xref:System.IDisposable.Dispose%2A?displayProperty=fullName> オブジェクトがガベージコレクションに使用できるようになる前に、いつでもユーザーがリソースを解放できるようにします。 <xref:System.IDisposable.Dispose%2A?displayProperty=fullName>メソッドが呼び出されると、オブジェクトのリソースが解放されます。 これにより、終了処理は不要になります。 <xref:System.IDisposable.Dispose%2A?displayProperty=fullName><xref:System.GC.SuppressFinalize%2A?displayProperty=fullName>ガベージコレクターがオブジェクトのファイナライザーを呼び出さないように、を呼び出す必要があります。

 ファイナライザーの派生型が [system.object] を再実装しないようにするには (<!-- TODO: review code entity reference <xref:assetId:///System.IDisposable?qualifyHint=True&amp;autoUpgrade=False>  -->) とを呼び出すために、ファイナライザーのないシールされていない型は引き続きを呼び出す必要があり <xref:System.GC.SuppressFinalize%2A?displayProperty=fullName> ます。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、次のようにします。

 メソッドがの実装である場合は <xref:System.IDisposable.Dispose%2A> 、への呼び出しを追加 <xref:System.GC.SuppressFinalize%2A?displayProperty=fullName> します。

 メソッドがの実装でない場合は <xref:System.IDisposable.Dispose%2A> 、の呼び出しを削除するか、 <xref:System.GC.SuppressFinalize%2A?displayProperty=fullName> 型の実装に移動し <xref:System.IDisposable.Dispose%2A> ます。

 に対するすべての呼び出しを変更して、 <xref:System.GC.SuppressFinalize%2A?displayProperty=fullName> この (Visual Basic で) を渡します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 Deliberating を使用して <xref:System.GC.SuppressFinalize%2A?displayProperty=fullName> 他のオブジェクトの有効期間を制御している場合にのみ、このルールの警告を非表示にします。 の実装でが呼び出されない場合は、この規則からの警告を抑制しないでください <xref:System.IDisposable.Dispose%2A> <xref:System.GC.SuppressFinalize%2A?displayProperty=fullName> 。 このような状況では、終了処理を抑制しないとパフォーマンスが低下し、利点は得られません。

## <a name="example"></a>例
 次の例は、を誤って呼び出すメソッドを示して <xref:System.GC.SuppressFinalize%2A?displayProperty=fullName> います。

 [!code-csharp[FxCop.Usage.CallGCSuppressFinalizeCorrectly#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.CallGCSuppressFinalizeCorrectly/CS/FxCop.Usage.CallGCSuppressFinalizeCorrectly.cs#1)]
 [!code-vb[FxCop.Usage.CallGCSuppressFinalizeCorrectly#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.CallGCSuppressFinalizeCorrectly/VB/FxCop.Usage.CallGCSuppressFinalizeCorrectly.vb#1)]

## <a name="example"></a>例
 次の例は、を正しく呼び出すメソッドを示して <xref:System.GC.SuppressFinalize%2A?displayProperty=fullName> います。

 [!code-csharp[FxCop.Usage.CallGCSuppressFinalizeCorrectly2#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.CallGCSuppressFinalizeCorrectly2/CS/FxCop.Usage.CallGCSuppressFinalizeCorrectly2.cs#1)]
 [!code-vb[FxCop.Usage.CallGCSuppressFinalizeCorrectly2#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.CallGCSuppressFinalizeCorrectly2/VB/FxCop.Usage.CallGCSuppressFinalizeCorrectly2.vb#1)]

## <a name="related-rules"></a>関連規則
 [CA2215:Dispose メソッドが基底クラスの Dispose を呼び出す必要があります](../code-quality/ca2215-dispose-methods-should-call-base-class-dispose.md)

 [CA2216:破棄可能な型はファイナライザーを宣言しなければなりません](../code-quality/ca2216-disposable-types-should-declare-finalizer.md)

## <a name="see-also"></a>参照
 [Dispose パターン](https://msdn.microsoft.com/library/31a6c13b-d6a2-492b-9a9f-e5238c983bcb)
