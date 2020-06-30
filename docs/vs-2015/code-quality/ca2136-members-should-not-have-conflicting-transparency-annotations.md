---
title: 'CA2136: メンバーは、競合する透過性注釈を持つことはできません |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2127
- SecurityTransparentAssembliesShouldNotContainSecurityCriticalCode
- CA2136
helpviewer_keywords:
- SecurityTransparentAssembliesShouldNotContainSecurityCriticalCode
- CA2127
ms.assetid: ff5a1d18-7c52-4da5-8990-60be83a8ea81
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: a3a17a0db7dd4ad1c57d23104a313a78cd1289ed
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547694"
---
# <a name="ca2136-members-should-not-have-conflicting-transparency-annotations"></a>CA2136:メンバーには、透過性注釈の競合があってはならない
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|TransparencyAnnotationsShouldNotConflict|
|CheckId|CA2136|
|カテゴリ|Microsoft.Security|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 この規則は、型のメンバーが、 <xref:System.Security> メンバーのコンテナーのセキュリティ属性とは異なる透過性を持つセキュリティ属性でマークされている場合に適用されます。

## <a name="rule-description"></a>ルールの説明
 透過性属性は、大きいスコープのコード要素から小さいスコープの要素に適用されます。 大きいスコープのコード要素の透過性属性は、最初の要素に含まれているコード要素の透過性属性よりも優先されます。 たとえば、属性でマークされたクラスには、 <xref:System.Security.SecurityCriticalAttribute> 属性でマークされたメソッドを含めることはできません <xref:System.Security.SecuritySafeCriticalAttribute> 。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この違反を修正するには、スコープが低いコード要素からセキュリティ属性を削除するか、属性を、含んでいるコード要素と同じになるように変更します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則からの警告を抑制しないでください。

## <a name="example"></a>例
 次の例では、メソッドが属性でマークされ、 <xref:System.Security.SecuritySafeCriticalAttribute> 属性でマークされたクラスのメンバーになってい <xref:System.Security.SecurityCriticalAttribute> ます。 セキュリティセーフ属性を削除する必要があります。

 [!code-csharp[FxCop.Security.CA2136.TransparencyAnnotationsShouldNotConflict#1](../snippets/csharp/VS_Snippets_CodeAnalysis/fxcop.security.ca2136.transparencyannotationsshouldnotconflict/cs/ca2136 - transparencyannotationsshouldnotconflict.cs#1)]
