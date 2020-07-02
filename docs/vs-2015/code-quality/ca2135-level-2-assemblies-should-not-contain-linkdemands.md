---
title: 'CA2135: レベル2のアセンブリは Linkdemand | を含むことはできませんMicrosoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2135
ms.assetid: 7a775285-42d2-4f13-8434-3fdb0deeebe6
caps.latest.revision: 12
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: cbb68855832e84150b81c8a8a6fde47bf9433edc
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547707"
---
# <a name="ca2135-level-2-assemblies-should-not-contain-linkdemands"></a>CA2135:レベル 2 のアセンブリは LinkDemand を含んではならない
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|アイテム|値|
|-|-|
|TypeName|SecurityRuleSetLevel2MethodsShouldNotBeProtectedWithLinkDemands|
|CheckId|CA2135|
|カテゴリ|Microsoft.Security|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 クラスまたはクラスメンバーが、 <xref:System.Security.Permissions.SecurityAction> レベル2のセキュリティを使用しているアプリケーションでを使用しています。

## <a name="rule-description"></a>ルールの説明
 LinkDemands は、レベル 2 のセキュリティ規則セットでは使用が非推奨とされます。 Linkdemand を使用して just-in-time (JIT) コンパイル時にセキュリティを適用するのではなく、メソッド、型、およびフィールドを属性でマークし <xref:System.Security.SecurityCriticalAttribute> ます。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、を削除 <xref:System.Security.Permissions.SecurityAction> し、属性を使用して型またはメンバーをマークし <xref:System.Security.SecurityCriticalAttribute> ます。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。

## <a name="example"></a>例
 次の例では、を <xref:System.Security.Permissions.SecurityAction> 削除し、メソッドを属性でマークし <xref:System.Security.SecurityCriticalAttribute> ます。

 [!code-csharp[FxCop.Security.CA2135.SecurityRuleSetLevel2MethodsShouldNotBeProtectedWithLinkDemands#1](../snippets/csharp/VS_Snippets_CodeAnalysis/fxcop.security.ca2135.securityrulesetlevel2methodsshouldnotbeprotectedwithlinkdemands/cs/ca2135.cs#1)]
