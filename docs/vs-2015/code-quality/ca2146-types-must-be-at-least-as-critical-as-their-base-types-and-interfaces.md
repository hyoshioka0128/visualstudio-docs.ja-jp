---
title: 'CA2146: 型は、基本型およびインターフェイスと同様に、少なくとも重要である必要があります |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2146
ms.assetid: 241fb784-1f6b-46e5-8ceb-c438e341d38e
caps.latest.revision: 13
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 2316d6e555fa091d26392aee71b774489c81a379
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85546394"
---
# <a name="ca2146-types-must-be-at-least-as-critical-as-their-base-types-and-interfaces"></a>CA2146:型は、基本型およびインターフェイスと同程度以上、重要でなければならない
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|TypesMustBeAtLeastAsCriticalAsBaseTypes|
|CheckId|CA2146|
|カテゴリ|Microsoft.Security|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 透過型は、またはでマークされた型から派生し <xref:System.Security.SecuritySafeCriticalAttribute> <xref:System.Security.SecurityCriticalAttribute> ます。または、属性でマークされた型は、 <xref:System.Security.SecuritySafeCriticalAttribute> 属性でマークされた型から派生し <xref:System.Security.SecurityCriticalAttribute> ます。

## <a name="rule-description"></a>ルールの説明
 派生型に透過的セキュリティ属性が設定されていて、この属性が基本型または実装されたインターフェイスほど重要ではない場合に、この規則が適用されます。 クリティカルな基本型から派生したり、クリティカルなインターフェイスを実装したりできるのは、クリティカルなデータ型だけです。また、セーフ クリティカルな基本型から派生したり、セーフ クリティカルなインターフェイスを実装したりできるのは、クリティカルまたはセーフ クリティカルなデータ型だけです。 レベル2の透過性でこの規則を違反すると、 <xref:System.TypeLoadException> 派生型のがになります。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この違反を修正するには、基本型またはインターフェイスとして少なくとも重要な透過性属性を使用して、派生または実装する型をマークします。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。

## <a name="example"></a>例
 [!code-csharp[FxCop.Security.CA2146.TypesMustBeAtLeastAsCriticalAsBaseTypes#1](../snippets/csharp/VS_Snippets_CodeAnalysis/fxcop.security.ca2146.typesmustbeatleastascriticalasbasetypes/cs/ca2146 - typesmustbeatleastascriticalasbasetypes.cs#1)]
