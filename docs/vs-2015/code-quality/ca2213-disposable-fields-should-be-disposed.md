---
title: 'CA2213: 破棄可能なフィールドを破棄する必要があります |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- DisposableFieldsShouldBeDisposed
- CA2213
helpviewer_keywords:
- CA2213
- DisposableFieldsShouldBeDisposed
ms.assetid: e99442c9-70e2-47f3-b61a-d8ac003bc6e5
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 887600bad0c3d05ff78050aa4449cf49dc882027
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85534577"
---
# <a name="ca2213-disposable-fields-should-be-disposed"></a>CA2213:破棄可能なフィールドは破棄されなければなりません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|DisposableFieldsShouldBeDisposed|
|CheckId|CA2213|
|カテゴリ|Microsoft. 使用方法|
|互換性に影響する変更点|中断なし|

## <a name="cause"></a>原因
 を実装する型は、 <xref:System.IDisposable?displayProperty=fullName> も実装する型のフィールドを宣言 <xref:System.IDisposable> します。 <xref:System.IDisposable.Dispose%2A>フィールドのメソッドが、 <xref:System.IDisposable.Dispose%2A> 宣言する型のメソッドによって呼び出されていません。

## <a name="rule-description"></a>ルールの説明
 型は、そのすべてのアンマネージリソースを破棄します。これは、を実装することで実現され <xref:System.IDisposable> ます。 このルールは、破棄可能な型が、 `T` 破棄可能 `F` な型のインスタンスであるフィールドを宣言しているかどうかを確認し `FT` ます。 各フィールドについて、 `F` ルールはの呼び出しの検索を試み `FT.Dispose` ます。 この規則は、によって呼び出されたメソッドを検索し、 `T.Dispose` 1 レベル下 (で呼び出されたメソッドによって呼び出されたメソッド) を検索し `FT.Dispose` ます。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、 <xref:System.IDisposable.Dispose%2A> フィールドに保持され <xref:System.IDisposable> ているアンマネージリソースの割り当てと解放を担当する場合は、を実装する型のフィールドに対してを呼び出します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 フィールドに保持されているリソースを解放する責任がない場合、またはの呼び出しが <xref:System.IDisposable.Dispose%2A> 規則のチェックよりも深い呼び出しレベルで発生する場合は、この規則からの警告を抑制することが安全です。

## <a name="example"></a>例
 次の例は、 `TypeA` <xref:System.IDisposable> ( `FT` 前の説明で) を実装する型を示しています。

 [!code-csharp[FxCop.Usage.IDisposablePattern#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.IDisposablePattern/cs/FxCop.Usage.IDisposablePattern.cs#1)]

## <a name="example"></a>例
 次の例では、フィールド `TypeB` `aFieldOfADisposableType` に対してを呼び出さずに (前の説明の) フィールドを破棄可能 `F` な型 () として宣言することによって、この規則に違反する型を示して `TypeA` い <xref:System.IDisposable.Dispose%2A> ます。 `TypeB` 前の説明のに対応 `T` します。

 [!code-csharp[FxCop.Usage.IDisposableFields#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.IDisposableFields/cs/FxCop.Usage.IDisposableFields.cs#1)]

## <a name="see-also"></a>参照
 <xref:System.IDisposable?displayProperty=fullName> [Dispose パターン](https://msdn.microsoft.com/library/31a6c13b-d6a2-492b-9a9f-e5238c983bcb)
