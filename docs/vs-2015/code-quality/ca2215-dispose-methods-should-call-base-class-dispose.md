---
title: 'CA2215: Dispose メソッドは基底クラスの dispose | を呼び出す必要がありますMicrosoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2215
- DisposeMethodsShouldCallBaseClassDispose
- Dispose methods should call base class dispose
helpviewer_keywords:
- DisposeMethodsShouldCallBaseClassDispose
- CA2215
ms.assetid: c772e7a6-a87e-425c-a70e-912664ae9042
caps.latest.revision: 18
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 4197c2faaf4aa23db930a9019538592326a84116
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85534382"
---
# <a name="ca2215-dispose-methods-should-call-base-class-dispose"></a>CA2215:Dispose メソッドが基底クラスの Dispose を呼び出す必要があります
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|アイテム|値|
|-|-|
|TypeName|DisposeMethodsShouldCallBaseClassDispose|
|CheckId|CA2215|
|カテゴリ|Microsoft. 使用方法|
|互換性に影響する変更点|中断なし|

## <a name="cause"></a>原因
 を実装する型は、 <xref:System.IDisposable?displayProperty=fullName> も実装する型から継承 <xref:System.IDisposable> します。 <xref:System.IDisposable.Dispose%2A>継承する型のメソッドは、 <xref:System.IDisposable.Dispose%2A> 親の型のメソッドを呼び出しません。

## <a name="rule-description"></a>ルールの説明
 型が破棄可能な型から継承する場合は、 <xref:System.IDisposable.Dispose%2A> 独自のメソッド内から基本型のメソッドを呼び出す必要があり <xref:System.IDisposable.Dispose%2A> ます。 基本型のメソッド Dispose を呼び出すと、基本型によって作成されたすべてのリソースが解放されます。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、を呼び出し `base` ます。<xref:System.IDisposable.Dispose%2A> メソッド内 <xref:System.IDisposable.Dispose%2A> 。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 を呼び出した場合、このルールからの警告を抑制するのは安全です `base` 。<xref:System.IDisposable.Dispose%2A> ルールチェックよりも深い呼び出しレベルで発生します。

## <a name="example"></a>例
 を実装する型の例を次に示し `TypeA` <xref:System.IDisposable> ます。

 [!code-csharp[FxCop.Usage.IDisposablePattern#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.IDisposablePattern/cs/FxCop.Usage.IDisposablePattern.cs#1)]

## <a name="example"></a>例
 次の例は、 `TypeB` 型を継承し、 `TypeA` そのメソッドを正しく呼び出す型を示して <xref:System.IDisposable.Dispose%2A> います。

 [!code-vb[FxCop.Usage.IDisposableBaseCalled#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.IDisposableBaseCalled/vb/FxCop.Usage.IDisposableBaseCalled.vb#1)]

## <a name="see-also"></a>関連項目
 <xref:System.IDisposable?displayProperty=fullName> [Dispose パターン](https://msdn.microsoft.com/library/31a6c13b-d6a2-492b-9a9f-e5238c983bcb)
