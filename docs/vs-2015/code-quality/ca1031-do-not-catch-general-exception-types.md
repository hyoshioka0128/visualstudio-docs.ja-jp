---
title: 'CA1031: 一般的な例外の種類をキャッチしない |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1031
- DoNotCatchGeneralExceptionTypes
helpviewer_keywords:
- CA1031
- DoNotCatchGeneralExceptionTypes
ms.assetid: cbc283ae-2a46-4ec0-940e-85aa189b118f
caps.latest.revision: 22
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 520c9a066a4a902d5e9243baf1a8d8dec1b78e29
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85542403"
---
# <a name="ca1031-do-not-catch-general-exception-types"></a>CA1031:一般的な例外の種類はキャッチしません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|DoNotCatchGeneralExceptionTypes|
|CheckId|CA1031|
|カテゴリ|Microsoft Design|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因
 やなどの一般的な例外は、 <xref:System.Exception?displayProperty=fullName> <xref:System.SystemException?displayProperty=fullName> ステートメントでキャッチされ `catch` ます。または、のような一般的な catch 句が `catch()` 使用されます。

## <a name="rule-description"></a>ルールの説明
 汎用的な例外はキャッチしないでください。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、より具体的な例外をキャッチするか、ブロック内の最後のステートメントとして一般的な例外を再スローし `catch` ます。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。 一般的な例外の種類をキャッチすると、ライブラリユーザーの実行時の問題が隠蔽されるため、デバッグが困難になる可能性があります。

> [!NOTE]
> 以降では、 [!INCLUDE[net_v40_long](../includes/net-v40-long-md.md)] 共通言語ランタイム (CLR) によって、オペレーティングシステムで発生した破損状態の例外や、のアクセス違反などのマネージコードが [!INCLUDE[TLA#tla_mswin](../includes/tlasharptla-mswin-md.md)] マネージコードによって処理されるようになりました。 またはそれ以降のバージョンでアプリケーションをコンパイルし、破損状態例外の処理を維持する場合は、 [!INCLUDE[net_v40_short](../includes/net-v40-short-md.md)] <xref:System.Runtime.ExceptionServices.HandleProcessCorruptedStateExceptionsAttribute> 破損状態例外を処理するメソッドに属性を適用できます。

## <a name="example"></a>例
 次の例は、この規則に違反する型と、ブロックを正しく実装する型を示して `catch` います。

 [!code-cpp[FxCop.Design.ExceptionAndSystemException#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Design.ExceptionAndSystemException/cpp/FxCop.Design.ExceptionAndSystemException.cpp#1)]
 [!code-csharp[FxCop.Design.ExceptionAndSystemException#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.ExceptionAndSystemException/cs/FxCop.Design.ExceptionAndSystemException.cs#1)]
 [!code-vb[FxCop.Design.ExceptionAndSystemException#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.ExceptionAndSystemException/vb/FxCop.Design.ExceptionAndSystemException.vb#1)]

## <a name="related-rules"></a>関連規則
 [CA2200:スタック詳細を保持するために再度スローします](../code-quality/ca2200-rethrow-to-preserve-stack-details.md)
