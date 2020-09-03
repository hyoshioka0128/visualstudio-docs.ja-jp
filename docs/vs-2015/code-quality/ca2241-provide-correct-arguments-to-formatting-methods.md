---
title: 'CA2241: 書式設定メソッドに正しい引数を指定してください |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2241
- Provide correct arguments to formatting methods
- ProvideCorrectArgumentsToFormattingMethods
helpviewer_keywords:
- ProvideCorrectArgumentsToFormattingMethods
- CA2241
ms.assetid: 83639bc4-4c91-4a07-a40e-dc5e49a84494
caps.latest.revision: 14
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 1dfd770efd4d690930155d2486b8ff1859065272
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85543651"
---
# <a name="ca2241-provide-correct-arguments-to-formatting-methods"></a>CA2241:書式設定メソッドに正しい引数を提供
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|ProvideCorrectArgumentsToFormattingMethods|
|CheckId|CA2241|
|カテゴリ|Microsoft. 使用方法|
|互換性に影響する変更点|中断なし|

## <a name="cause"></a>原因
 `format`、、などのメソッドに渡された文字列引数に、 <xref:System.Console.WriteLine%2A> <xref:System.Console.Write%2A> <xref:System.String.Format%2A?displayProperty=fullName> 各オブジェクト引数に対応する書式項目が含まれていません。また、その逆も同様です。

## <a name="rule-description"></a>ルールの説明
 、、などのメソッドへの引数は、 <xref:System.Console.WriteLine%2A> <xref:System.Console.Write%2A> <xref:System.String.Format%2A> 書式指定文字列の後に複数のインスタンスが続く形式で構成さ <xref:System.Object?displayProperty=fullName> れます。 書式指定文字列は、{index [, alignment] [: formatString]} という形式のテキストと埋め込み書式項目で構成されます。 ' index ' は、どのオブジェクトを書式設定するかを示す、0から始まる整数です。 オブジェクトの書式指定文字列に対応するインデックスがない場合、オブジェクトは無視されます。 ' Index ' によって指定されたオブジェクトが存在しない場合は、 <xref:System.FormatException?displayProperty=fullName> 実行時にがスローされます。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、各オブジェクト引数に書式項目を指定し、各書式指定項目にオブジェクト引数を指定します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。

## <a name="example"></a>例
 次の例は、規則の2つの違反を示しています。

 [!code-csharp[FxCop.Usage.FormattingArguments#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.FormattingArguments/cs/FxCop.Usage.FormattingArguments.cs#1)]
 [!code-vb[FxCop.Usage.FormattingArguments#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.FormattingArguments/vb/FxCop.Usage.FormattingArguments.vb#1)]
