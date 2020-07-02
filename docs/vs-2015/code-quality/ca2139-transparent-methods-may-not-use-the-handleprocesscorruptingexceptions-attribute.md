---
title: 'CA2139: Transparent メソッドは、HandleProcessCorruptingExceptions attribute | を使用することはできません。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2139
ms.assetid: 45a0328a-add7-40f9-8934-dff59beb02b3
caps.latest.revision: 13
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 233e4366befd2a5a0d5690b14198ac13e2fcc957
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546485"
---
# <a name="ca2139-transparent-methods-may-not-use-the-handleprocesscorruptingexceptions-attribute"></a>CA2139:透過的メソッドは、HandleProcessCorruptingExceptions 属性を使用してはならない
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|アイテム|値|
|-|-|
|TypeName|TransparentMethodsMustNotHandleProcessCorruptingExceptions|
|CheckId|CA2139|
|カテゴリ|Microsoft.Security|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 透過的メソッドは、属性でマークされ <xref:System.Runtime.ExceptionServices.HandleProcessCorruptedStateExceptionsAttribute> ます。

## <a name="rule-description"></a>ルールの説明
 この規則は、透過的なメソッドをすべて実行し、属性を使用して例外の処理を処理しようとし <xref:System.Runtime.ExceptionServices.HandleProcessCorruptedStateExceptionsAttribute> ます。 プロセスを破損させる例外は、CLR バージョン4.0 の例外の例外分類です <xref:System.AccessViolationException> 。 HandleProcessCorruptedStateExceptionsAttribute 属性はセキュリティ クリティカルなメソッドでのみ使用できる属性で、透過的メソッドに適用された場合は無視されます。 プロセス破損例外を処理するには、この方法がセキュリティクリティカルまたはセキュリティセーフクリティカルである必要があります。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、属性を削除する <xref:System.Runtime.ExceptionServices.HandleProcessCorruptedStateExceptionsAttribute> か、または属性を使用してメソッドをマークし <xref:System.Security.SecurityCriticalAttribute> <xref:System.Security.SecuritySafeCriticalAttribute> ます。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。

## <a name="example"></a>例
 この例では、透過的なメソッドは属性でマークされ、 <xref:System.Runtime.ExceptionServices.HandleProcessCorruptedStateExceptionsAttribute> ルールは失敗します。 メソッドは、または属性でもマークされている必要があり <xref:System.Security.SecurityCriticalAttribute> <xref:System.Security.SecuritySafeCriticalAttribute> ます。

 [!code-csharp[FxCop.Security.CA2139#1](../snippets/csharp/VS_Snippets_CodeAnalysis/fxcop.security.ca2139/cs/ca2139.cs#1)]
