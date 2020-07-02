---
title: 'CA2242: NaN に対して正しくテストします |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- TestForNaNCorrectly
- CA2242
helpviewer_keywords:
- CA2242
ms.assetid: e12dcffc-e255-4e1e-8fdf-3c6054d44abe
caps.latest.revision: 13
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: a0c832b7eb4a94506c5e15dfa5858bb9f6753912
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546264"
---
# <a name="ca2242-test-for-nan-correctly"></a>CA2242:NaN に対して正しくテストします
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|アイテム|値|
|-|-|
|TypeName|TestForNaNCorrectly|
|CheckId|CA2242|
|カテゴリ|Microsoft. 使用方法|
|互換性に影響する変更点|中断なし|

## <a name="cause"></a>原因
 式は、またはに対して値をテスト <xref:System.Single.NaN?displayProperty=fullName> <xref:System.Double.NaN?displayProperty=fullName> します。

## <a name="rule-description"></a>ルールの説明
 <xref:System.Double.NaN?displayProperty=fullName>は、算術演算が定義されていない場合に、数値以外の結果を表します。 値の間の等価性をテストし、 <xref:System.Double.NaN?displayProperty=fullName> 常にを返す式 `false` 。 値が等しくないかどうかをテストし、 <xref:System.Double.NaN?displayProperty=fullName> 常にを返す式 `true` 。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正し、値がを表すかどうかを正確に判断するに <xref:System.Double.NaN?displayProperty=fullName> <xref:System.Single.IsNaN%2A?displayProperty=fullName> は、またはを使用し <xref:System.Double.IsNaN%2A?displayProperty=fullName> て値をテストします。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。

## <a name="example"></a>例
 次の例では、値を誤ってテストする2つの式 <xref:System.Double.NaN?displayProperty=fullName> と、 <xref:System.Double.IsNaN%2A?displayProperty=fullName> 値をテストするために正しく使用する式を示します。

 [!code-csharp[FxCop.Usage.TestForNaN#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.TestForNaN/cs/FxCop.Usage.TestForNaN.cs#1)]
 [!code-vb[FxCop.Usage.TestForNaN#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.TestForNaN/vb/FxCop.Usage.TestForNaN.vb#1)]
