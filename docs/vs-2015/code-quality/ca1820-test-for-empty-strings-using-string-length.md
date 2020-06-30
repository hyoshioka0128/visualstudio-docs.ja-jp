---
title: 'CA1820: 文字列 length | を使用して空の文字列をテストします。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- TestForEmptyStringsUsingStringLength
- CA1820
helpviewer_keywords:
- TestForEmptyStringsUsingStringLength
- CA1820
ms.assetid: da1e70c8-b1dc-46b9-8b8f-4e6e48339681
caps.latest.revision: 23
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 296eb6407e3ce63b0eb28ff86c215c12ec724ce9
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545315"
---
# <a name="ca1820-test-for-empty-strings-using-string-length"></a>CA1820:文字列の長さを使用して空の文字列をテストします
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|TestForEmptyStringsUsingStringLength|
|CheckId|CA1820|
|カテゴリ|Microsoft. パフォーマンス|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因
 文字列は、を使用して空の文字列と比較され <xref:System.Object.Equals%2A?displayProperty=fullName> ます。

## <a name="rule-description"></a>ルールの説明
 プロパティまたはメソッドを使用した文字列の比較 <xref:System.String.Length%2A?displayProperty=fullName> <xref:System.String.IsNullOrEmpty%2A?displayProperty=fullName> は、を使用するよりもはるかに高速です <xref:System.Object.Equals%2A> 。 これは、が、 <xref:System.Object.Equals%2A> <xref:System.String.IsNullOrEmpty%2A> <xref:System.String.Length%2A> プロパティ値を取得して0と比較するために実行された命令のいずれかまたはの数よりもはるかに多くの MSIL 命令を実行するためです。

 <xref:System.Object.Equals%2A> <xref:System.String.Length%2A> Null 文字列ではと = = 0 の動作が異なることに注意してください。 Null 文字列のプロパティの値を取得しようとすると、 <xref:System.String.Length%2A> 共通言語ランタイムはをスローし <xref:System.NullReferenceException?displayProperty=fullName> ます。 Null 文字列と空の文字列の比較を実行しても、共通言語ランタイムは例外をスローしません。この比較はを返し `false` ます。 Null のテストは、これらの2つの方法の相対的なパフォーマンスに大きな影響を与えません。 ターゲットを設定する場合は [!INCLUDE[dnprdnlong](../includes/dnprdnlong-md.md)] 、メソッドを使用し <xref:System.String.IsNullOrEmpty%2A> ます。 それ以外の場合は、 <xref:System.String.Length%2A> 可能な限り = = 比較を使用します。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、プロパティを使用するように比較を変更し、 <xref:System.String.Length%2A> null 文字列をテストします。 ターゲット設定 [!INCLUDE[dnprdnlong](../includes/dnprdnlong-md.md)] する場合は、メソッドを使用し <xref:System.String.IsNullOrEmpty%2A> ます。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 パフォーマンスが問題にならない場合は、このルールからの警告を抑制することが安全です。

## <a name="example"></a>例
 次の例は、空の文字列を検索するために使用されるさまざまな手法を示しています。

 [!code-csharp[FxCop.Performance.StringTest#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Performance.StringTest/cs/FxCop.Performance.StringTest.cs#1)]
