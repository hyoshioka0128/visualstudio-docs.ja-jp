---
title: 'CA2101: P 呼び出し文字列引数のマーシャリングを指定します |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- SpecifyMarshalingForPInvokeStringArguments
- CA2101
helpviewer_keywords:
- CA2101
- SpecifyMarshalingForPInvokeStringArguments
ms.assetid: 9d1abfc3-d320-41e0-9f6e-60cefe6ffe1b
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: ae65e922d1b4946300155bbf148abac574a2ec2a
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544379"
---
# <a name="ca2101-specify-marshaling-for-pinvoke-string-arguments"></a>CA2101: P/Invoke 文字列引数に対してマーシャリングを指定します
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|SpecifyMarshalingForPInvokeStringArguments|
|CheckId|CA2101|
|カテゴリ|Microsoft のグローバリゼーション|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因
 プラットフォーム呼び出しメンバーは、部分的に信頼された呼び出し元を許可し、文字列パラメーターを持ち、文字列を明示的にマーシャリングしません。

## <a name="rule-description"></a>ルールの説明
 Unicode から ANSI に変換する場合、特定の ANSI コードページですべての Unicode 文字を表現できるとは限りません。 *最適マッピング*では、表現できない文字の文字を置き換えることで、この問題を解決しようとします。 この機能を使用すると、選択した文字を制御できなくなる可能性があるため、セキュリティ上の脆弱性が生じる可能性があります。 たとえば、悪意のあるコードでは、特定のコードページで見つからない文字を含む Unicode 文字列を意図的に作成することができます。これは、".." などのファイルシステムの特殊文字に変換されます。 または '/'。 また、文字列が ANSI に変換される前に、特殊文字のセキュリティチェックが頻繁に行われることにも注意してください。

 最も適したマッピングは、アンマネージ変換の既定値で、WChar から1M バイトまでです。 最適マッピングを明示的に無効にしない限り、コードには、この問題のために悪用可能なセキュリティ脆弱性が含まれている可能性があります。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、文字列データ型を明示的にマーシャリングします。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。

## <a name="example"></a>例
 次の例は、この規則に違反するメソッドを示し、違反の修正方法を示しています。

 [!code-csharp[FxCop.Security.PinvokeAnsiUnicode#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.PinvokeAnsiUnicode/cs/FxCop.Security.PinvokeAnsiUnicode.cs#1)]
