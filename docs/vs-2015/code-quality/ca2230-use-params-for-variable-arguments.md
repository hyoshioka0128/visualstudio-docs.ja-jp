---
title: 'CA2230: 可変個の引数に対して params を使用します。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- UseParamsForVariableArguments
- CA2230
helpviewer_keywords:
- CA2230
- UseParamsForVariableArguments
ms.assetid: bf98b733-4855-4110-9f16-eba5a9e79421
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: ce66e04272618b9df2ab1957af305bb9bf40ee9c
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85540362"
---
# <a name="ca2230-use-params-for-variable-arguments"></a>CA2230:可変引数に対して param を使用します
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|アイテム|値|
|-|-|
|TypeName|UseParamsForVariableArguments|
|CheckId|CA2230|
|カテゴリ|Microsoft. 使用方法|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 パブリックまたはプロテクト型に、呼び出し規約を使用するパブリックメソッドまたはプロテクトメソッドが含まれてい `VarArgs` ます。

## <a name="rule-description"></a>ルールの説明
 `VarArgs`呼び出し規約は、可変個のパラメーターを受け取る特定のメソッド定義で使用されます。 呼び出し規約を使用するメソッド `VarArgs` は、共通言語仕様 (CLS) に準拠していないため、プログラミング言語間でアクセスできない可能性があります。

 C# では、 `VarArgs` メソッドのパラメーターリストがキーワードで終了するときに、呼び出し規約が使用され `__arglist` ます。 Visual Basic は呼び出し規則をサポートしていないため、Visual C++ では、 `VarArgs` 楕円表記法を使用するアンマネージコードでのみ使用でき `...` ます。

## <a name="how-to-fix-violations"></a>違反の修正方法
 C# でのこの規則違反を修正するには、の代わりに[params](https://msdn.microsoft.com/library/1690815e-b52b-4967-8380-5780aff08012)キーワードを使用し `__arglist` ます。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。

## <a name="example"></a>例
 次の例は、2つのメソッドを示しています。1つは規則に違反し、もう1つは規則を満たしています。

 [!code-csharp[FxCop.Usage.UseParams#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.UseParams/cs/FxCop.Usage.UseParams.cs#1)]

## <a name="see-also"></a>関連項目
 <xref:System.Reflection.CallingConventions?displayProperty=fullName>[言語への非依存性、および言語非依存コンポーネント](https://msdn.microsoft.com/library/4f0b77d0-4844-464f-af73-6e06bedeafc6)
