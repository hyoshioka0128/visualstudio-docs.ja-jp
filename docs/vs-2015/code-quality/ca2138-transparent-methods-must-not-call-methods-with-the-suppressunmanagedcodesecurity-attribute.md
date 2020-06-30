---
title: 'CA2138: Transparent メソッドは、SuppressUnmanagedCodeSecurity attribute | を使用してメソッドを呼び出すことはできません。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2138
ms.assetid: a14c4d32-f079-4f3a-956c-a1657cde0f66
caps.latest.revision: 14
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 35cc152998b15a2fd4c4ff02e4730cdfae5366cb
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546498"
---
# <a name="ca2138-transparent-methods-must-not-call-methods-with-the-suppressunmanagedcodesecurity-attribute"></a>CA2138:透過的メソッドは、SuppressUnmanagedCodeSecurity 属性を持つメソッドを呼び出してはならない
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|TransparentMethodsMustNotCallSuppressUnmanagedCodeSecurityMethods|
|CheckId|CA2138|
|カテゴリ|Microsoft.Security|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 透過的セキュリティメソッドは、属性でマークされたメソッドを呼び出し <xref:System.Security.SuppressUnmanagedCodeSecurityAttribute> ます。

## <a name="rule-description"></a>ルールの説明
 この規則は、ネイティブコードを直接呼び出す透過的メソッド (たとえば、P/Invoke (プラットフォーム呼び出し) 呼び出しでを使用するなど) で適用されます。 属性でマークされた P/Invoke メソッドと COM 相互運用メソッドは、 <xref:System.Security.SuppressUnmanagedCodeSecurityAttribute> 呼び出し元のメソッドに対して LinkDemand を実行します。 透過的セキュリティコードは Linkdemand を満たすことができないため、コードでは、SuppressUnmanagedCodeSecurity 属性でマークされたメソッド、または SuppressUnmanagedCodeSecurity 属性でマークされたクラスのメソッドを呼び出すことはできません。 メソッドが失敗するか、要求が完全な要求に変換されます。

 この規則を違反すると、 <xref:System.MethodAccessException> レベル2のセキュリティ透過性モデルのになり、レベル1の透過性モデルのに対する完全な要求が発生し <xref:System.Security.Permissions.SecurityPermissionAttribute.UnmanagedCode%2A> ます。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、属性を削除 <xref:System.Security.SuppressUnmanagedCodeSecurityAttribute> し、メソッドを属性または属性でマークし <xref:System.Security.SecurityCriticalAttribute> <xref:System.Security.SecuritySafeCriticalAttribute> ます。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。

## <a name="example"></a>例
 [!code-csharp[FxCop.Security.CA2138.TransparentMethodsMustNotCallSuppressUnmanagedCodeSecurityMethods#1](../snippets/csharp/VS_Snippets_CodeAnalysis/fxcop.security.ca2138.transparentmethodsmustnotcallsuppressunmanagedcodesecuritymethods/cs/ca2138.cs#1)]
