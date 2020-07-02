---
title: 'CA2134: メソッドは、基本メソッドをオーバーライドするときに、一貫性のある透明度を維持する必要があります |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2134
ms.assetid: 3b17e487-0326-442e-90e1-dc0ba9cdd3f2
caps.latest.revision: 11
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: fe9a84280b0124eed6bb0cfffae9c1ec2942bddf
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547720"
---
# <a name="ca2134-methods-must-keep-consistent-transparency-when-overriding-base-methods"></a>CA2134:メソッドは、基本メソッドをオーバーライドしている場合、透過性の整合性を保つ必要がある
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|アイテム|値|
|-|-|
|TypeName|MethodsMustOverrideWithConsistentTransparency|
|CheckId|CA2134|
|カテゴリ|Microsoft.Security|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 この規則は、でマークされたメソッドが <xref:System.Security.SecurityCriticalAttribute> 透過的またはでマークされたメソッドをオーバーライドするときに適用され <xref:System.Security.SecuritySafeCriticalAttribute> ます。 この規則は、透過的またはでマークされたメソッドが <xref:System.Security.SecuritySafeCriticalAttribute> 、でマークされたメソッドをオーバーライドした場合にも発生し <xref:System.Security.SecurityCriticalAttribute> ます。

 この規則は、仮想メソッドをオーバーライドする場合やインターフェイスを実装する場合に適用されます。

## <a name="rule-description"></a>ルールの説明
 この規則は、継承チェーンのさらに上にあるメソッドのセキュリティアクセシビリティを変更しようとした場合に発生します。 たとえば、基底クラスの仮想メソッドが透過的またはセーフクリティカルである場合、派生クラスは透過的またはセーフクリティカルなメソッドでオーバーライドする必要があります。 逆に、仮想がセキュリティクリティカルである場合、派生クラスはセキュリティクリティカルなメソッドでそれをオーバーライドする必要があります。 インターフェイスメソッドの実装にも同じ規則が適用されます。

 透過性規則は、コードが実行時ではなく JIT コンパイルされる場合に適用されます。これにより、透過性の計算に動的な型情報が含まれなくなります。 したがって、透過性の計算結果は、動的な型に関係なく、JIT コンパイルされている静的な型からのみ特定できる必要があります。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、仮想メソッドをオーバーライドするメソッドの透明度を変更するか、仮想メソッドまたはインターフェイスメソッドの透過性に一致するようにインターフェイスを実装します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則からの警告を抑制しないでください。 この規則を違反すると、 <xref:System.TypeLoadException> レベル2の透過性を使用するアセンブリのランタイムが生成されます。

## <a name="examples"></a>例

### <a name="code"></a>コード
 [!code-csharp[FxCop.Security.CA2134.MethodsMustOverrideWithConsistentTransparency#1](../snippets/csharp/VS_Snippets_CodeAnalysis/fxcop.security.ca2134.methodsmustoverridewithconsistenttransparency/cs/ca2134 - methodsmustoverridewithconsistenttransparency.cs#1)]

## <a name="see-also"></a>参照
 [透過的セキュリティ コード、レベル 2](https://msdn.microsoft.com/library/4d05610a-0da6-4f08-acea-d54c9d6143c0)
