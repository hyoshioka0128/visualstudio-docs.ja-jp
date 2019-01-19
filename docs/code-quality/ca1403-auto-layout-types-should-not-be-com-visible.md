---
title: CA1403:Auto 配置の型を COM 参照可能にすることはできません
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.topic: reference
f1_keywords:
- AutoLayoutTypesShouldNotBeComVisible
- CA1403
helpviewer_keywords:
- CA1403
- AutoLayoutTypesShouldNotBeComVisible
ms.assetid: a7007714-f9b4-4730-94e0-67d3dc68991f
author: gewarren
ms.author: gewarren
manager: douge
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 1f713ac012509dd36d483ca354630e125066360b
ms.sourcegitcommit: 37fb7075b0a65d2add3b137a5230767aa3266c74
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/02/2019
ms.locfileid: "53954540"
---
# <a name="ca1403-auto-layout-types-should-not-be-com-visible"></a>CA1403:Auto 配置の型を COM 参照可能にすることはできません

|||
|-|-|
|TypeName|AutoLayoutTypesShouldNotBeComVisible|
|CheckId|CA1403|
|カテゴリ|Microsoft.Interoperability|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因

コンポーネント オブジェクト モデル (COM) 参照可能な値の型が付いて、<xref:System.Runtime.InteropServices.StructLayoutAttribute?displayProperty=fullName>属性に設定<xref:System.Runtime.InteropServices.LayoutKind.Auto?displayProperty=fullName>します。

## <a name="rule-description"></a>規則の説明

<xref:System.Runtime.InteropServices.LayoutKind> レイアウトの種類は、共通言語ランタイムによって管理されます。 これらの型のレイアウトは、特定のレイアウトを期待する COM クライアントを中断する .NET Framework のバージョン間で変更できます。 場合、 <xref:System.Runtime.InteropServices.StructLayoutAttribute> 、C#、Visual Basic、および C++ コンパイラの指定の属性が指定されていない[参照](<xref:System.Runtime.InteropServices.LayoutKind.Auto>)値の型。

すべてのパブリックな非ジェネリックの型が、COM から参照できる他のマークがない限り、すべてのパブリックでないとジェネリック型が COM に表示されません。 ただし、偽陽性を減らすためには、この規則を明示的に指定する型の COM の参照範囲が必要です。 格納しているアセンブリをマークする必要があります、<xref:System.Runtime.InteropServices.ComVisibleAttribute?displayProperty=fullName>に設定`false`で型をマークする必要があり、<xref:System.Runtime.InteropServices.ComVisibleAttribute>に設定`true`します。

## <a name="how-to-fix-violations"></a>違反の修正方法

この規則違反を解決するには、値を変更、<xref:System.Runtime.InteropServices.StructLayoutAttribute>属性を[LayoutKind.Explicit](<xref:System.Runtime.InteropServices.LayoutKind.Explicit>)または[LayoutKind.Sequential](<xref:System.Runtime.InteropServices.LayoutKind.Sequential>)、か、COM 型を非表示

## <a name="when-to-suppress-warnings"></a>警告を抑制します。

この規則による警告は抑制しないでください。

## <a name="example"></a>例

次の例では、規則に違反する型と、規則に適合する型を示します。

[!code-csharp[FxCop.Interoperability.AutoLayout#1](../code-quality/codesnippet/CSharp/ca1403-auto-layout-types-should-not-be-com-visible_1.cs)]
[!code-vb[FxCop.Interoperability.AutoLayout#1](../code-quality/codesnippet/VisualBasic/ca1403-auto-layout-types-should-not-be-com-visible_1.vb)]

## <a name="related-rules"></a>関連するルール

[CA 1408:AutoDual ClassInterfaceType を使用します。](../code-quality/ca1408-do-not-use-autodual-classinterfacetype.md)

## <a name="see-also"></a>関連項目

- [相互運用のための .NET 型を修飾します。](/dotnet/framework/interop/qualifying-net-types-for-interoperation)
- [アンマネージ コードと相互運用します。](/dotnet/framework/interop/index)
