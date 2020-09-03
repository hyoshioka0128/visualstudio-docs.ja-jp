---
title: 'CA2141: Transparent メソッドは Linkdemand | を満たすことはできません。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2141
ms.assetid: 2957f5f7-c511-4180-ba80-752034f10a77
caps.latest.revision: 16
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: bee810ed938d316e92095ad47062ed5ad9cd456f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85546446"
---
# <a name="ca2141transparent-methods-must-not-satisfy-linkdemands"></a>CA2141: 透過的メソッドは、LinkDemand を満たしてはならない
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|TransparentMethodsMustNotSatisfyLinkDemands|
|CheckId|CA2141|
|カテゴリ|Microsoft.Security|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 透過的セキュリティメソッドは、(APTCA) 属性でマークされていないアセンブリ内のメソッドを呼び出し <xref:System.Security.AllowPartiallyTrustedCallersAttribute> ます。または、透過的セキュリティメソッドは、 <xref:System.Security.Permissions.SecurityAction> `.LinkDemand` 型またはメソッドに対してを満たします。

## <a name="rule-description"></a>ルールの説明
 LinkDemand を満たすことは、セキュリティ上重要な操作であり、意図しない特権の昇格を引き起こす可能性があります。 透過的セキュリティコードは、セキュリティクリティカルなコードと同じセキュリティ監査要件の対象にならないため、Linkdemand を満たしてはなりません。 セキュリティ規則セットレベル1のアセンブリの透過的メソッドによって、対応するすべての Linkdemand が実行時に完全な要求に変換され、パフォーマンスの問題が発生する可能性があります。 セキュリティ規則セットレベル2のアセンブリでは、LinkDemand を満たす場合、transparent メソッドはジャストインタイム (JIT) コンパイラでのコンパイルに失敗します。

 E レベル2のセキュリティを有効にしたアセンブリでは、セキュリティ transparent メソッドが LinkDemand を満たすか、非 APTCA アセンブリのメソッドを呼び出すと、が発生し <xref:System.MethodAccessException> ます。レベル1のアセンブリでは、LinkDemand は完全な要求になります。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、アクセスメソッドを <xref:System.Security.SecurityCriticalAttribute> 属性または属性でマークするか、アクセスされ <xref:System.Security.SecuritySafeCriticalAttribute> たメソッドから LinkDemand を削除します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。

## <a name="example"></a>例
 この例では、transparent メソッドは LinkDemand を持つメソッドを呼び出そうとします。 このルールは、このコードで発生します。

 [!code-csharp[FxCop.Security.CA2141.TransparentMethodsMustNotSatisfyLinkDemands#1](../snippets/csharp/VS_Snippets_CodeAnalysis/fxcop.security.ca2141.transparentmethodsmustnotsatisfylinkdemands/cs/ca2141 - transparentmethodsmustnotsatisfylinkdemands.cs#1)]
