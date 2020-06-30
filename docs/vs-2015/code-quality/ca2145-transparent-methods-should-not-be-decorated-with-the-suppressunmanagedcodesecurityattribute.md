---
title: 'CA2145: Transparent メソッドは、SuppressUnmanagedCodeSecurityAttribute | で修飾することはできません。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2145
ms.assetid: 81970700-b438-4b3b-9239-16887e16f7b7
caps.latest.revision: 13
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: d5eb16130aef42abcf9fddf533d0253864a75114
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546407"
---
# <a name="ca2145-transparent-methods-should-not-be-decorated-with-the-suppressunmanagedcodesecurityattribute"></a>CA2145:透過的メソッドを SuppressUnmanagedCodeSecurityAttribute で修飾してはならない
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|TransparentMethodsShouldNotUseSuppressUnmanagedCodeSecurity|
|CheckId|CA2145|
|カテゴリ|Microsoft.Security|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 透過的メソッド、メソッドでマークされたメソッド、 <xref:System.Security.SecuritySafeCriticalAttribute> またはメソッドを含む型は、属性でマークされ <xref:System.Security.SuppressUnmanagedCodeSecurityAttribute> ます。

## <a name="rule-description"></a>ルールの説明
 属性で修飾されたメソッドには、 <xref:System.Security.SuppressUnmanagedCodeSecurityAttribute> それを呼び出すメソッドに配置される暗黙的な LinkDemand があります。 この LinkDemand では、呼び出し元のコードがセキュリティ クリティカルなコードである必要があります。 SuppressUnmanagedCodeSecurity を使用するメソッドに属性をマークすると、 <xref:System.Security.SecurityCriticalAttribute> メソッドの呼び出し元に対してこの要件がより明確になります。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、メソッドまたは型を属性でマークし <xref:System.Security.SecurityCriticalAttribute> ます。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。

### <a name="code"></a>コード
 [!code-csharp[FxCop.Security.CA2145.TransparentMethodsShouldNotUseSuppressUnmanagedCodeSecurity#1](../snippets/csharp/VS_Snippets_CodeAnalysis/fxcop.security.ca2145.transparentmethodsshouldnotusesuppressunmanagedcodesecurity/cs/ca2145.cs#1)]

### <a name="comments"></a>コメント
