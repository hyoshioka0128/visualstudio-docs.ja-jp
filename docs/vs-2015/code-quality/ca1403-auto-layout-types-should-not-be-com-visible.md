---
title: 'CA1403: Auto レイアウトの型を COM 参照可能にすることはできません |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- AutoLayoutTypesShouldNotBeComVisible
- CA1403
helpviewer_keywords:
- CA1403
- AutoLayoutTypesShouldNotBeComVisible
ms.assetid: a7007714-f9b4-4730-94e0-67d3dc68991f
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 1752efb5be1828f62703e1fe1a1130b37ff80503
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85534928"
---
# <a name="ca1403-auto-layout-types-should-not-be-com-visible"></a>CA1403:Auto 配置の型を COM 参照可能にすることはできません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|AutoLayoutTypesShouldNotBeComVisible|
|CheckId|CA1403|
|カテゴリ|Microsoft. 相互運用性|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 コンポーネントオブジェクトモデル (COM) に表示される値型は、属性がに設定されたマークが付けられ <xref:System.Runtime.InteropServices.StructLayoutAttribute?displayProperty=fullName> <xref:System.Runtime.InteropServices.LayoutKind?displayProperty=fullName> ます。

## <a name="rule-description"></a>ルールの説明
 <xref:System.Runtime.InteropServices.LayoutKind> レイアウトの種類は、共通言語ランタイムによって管理されます。 これらの型のレイアウトは、.NET Framework のバージョン間で変わる可能性があります。これにより、特定のレイアウトを期待する COM クライアントが中断されます。 <xref:System.Runtime.InteropServices.StructLayoutAttribute>属性が指定されていない場合、C#、 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 、および C++ コンパイラは、 <xref:System.Runtime.InteropServices.LayoutKind> 値型のレイアウトを指定することに注意してください。

 特に指定されていない限り、パブリックなすべての非ジェネリック型は COM から参照できます。非パブリック型とジェネリック型はすべて、COM から見えません。 ただし、偽陽性を減らすために、このルールでは、型の COM 参照可能範囲が明示的に指定されている必要があります。含んでいるアセンブリは、がに設定されたでマークされ、 <xref:System.Runtime.InteropServices.ComVisibleAttribute?displayProperty=fullName> `false` 型はに設定されたでマークされる必要があり <xref:System.Runtime.InteropServices.ComVisibleAttribute> `true` ます。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、属性の値 <xref:System.Runtime.InteropServices.StructLayoutAttribute> をまたはに変更する <xref:System.Runtime.InteropServices.LayoutKind> か、型が COM に対して非表示になるようにし <xref:System.Runtime.InteropServices.LayoutKind> ます。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。

## <a name="example"></a>例
 次の例は、規則に違反する型と、規則を満たす型を示しています。

 [!code-csharp[FxCop.Interoperability.AutoLayout#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Interoperability.AutoLayout/cs/FxCop.Interoperability.AutoLayout.cs#1)]
 [!code-vb[FxCop.Interoperability.AutoLayout#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Interoperability.AutoLayout/vb/FxCop.Interoperability.AutoLayout.vb#1)]

## <a name="related-rules"></a>関連規則
 [CA1408:AutoDual ClassInterfaceType を使用しないでください](../code-quality/ca1408-do-not-use-autodual-classinterfacetype.md)

## <a name="see-also"></a>参照
 [相互運用のための .Net 型を修飾する](https://msdn.microsoft.com/library/4b8afb52-fb8d-4e65-b47c-fd82956a3cdd)[クラスインターフェイスの概要](https://msdn.microsoft.com/733c0dd2-12e5-46e6-8de1-39d5b25df024)[アンマネージコードとの相互運用](https://msdn.microsoft.com/library/ccb68ce7-b0e9-4ffb-839d-03b1cd2c1258)
