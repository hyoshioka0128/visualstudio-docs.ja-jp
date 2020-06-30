---
title: 'CA1405: COM 参照可能な型の基本型は COM 参照可能でなければなりません |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1405
- ComVisibleTypeBaseTypesShouldBeComVisible
helpviewer_keywords:
- CA1405
- ComVisibleTypeBaseTypesShouldBeComVisible
ms.assetid: a762ea2f-5285-4f73-bfb9-9eb10aea4290
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 779d3ec1ed520d5d48043f90e7cb6272553012a6
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85535045"
---
# <a name="ca1405-com-visible-type-base-types-should-be-com-visible"></a>CA1405:COM 参照可能な型の基本型は COM 参照可能でなければなりません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|ComVisibleTypeBaseTypesShouldBeComVisible|
|CheckId|CA1405|
|カテゴリ|Microsoft. 相互運用性|
|互換性に影響する変更点|依存関係 Sonfix|

## <a name="cause"></a>原因
 コンポーネントオブジェクトモデル (COM) で参照できる型が COM 参照可能ではない型から派生しています。

## <a name="rule-description"></a>ルールの説明
 COM 参照可能な型が新しいバージョンのメンバーを追加する場合、現在のバージョンにバインドされている COM クライアントの互換性を回避するために、厳密なガイドラインに従う必要があります。 COM で参照できない型は、新しいメンバーを追加するときに、これらの COM バージョン管理規則に従う必要がないということを前提としています。 ただし、com 参照可能な型が COM に表示されない型から派生し、または (既定値) のクラスインターフェイスを公開する場合、 <xref:System.Runtime.InteropServices.ClassInterfaceType?displayProperty=fullName> <xref:System.Runtime.InteropServices.ClassInterfaceType> 基本型のすべてのパブリックメンバーが com に公開されます (つまり、明示的に com 不可視としてマークされていない場合)。 基本型が後続のバージョンで新しいメンバーを追加する場合、派生型のクラスインターフェイスにバインドされているすべての COM クライアントが破損する可能性があります。 Com 参照可能な型は、com クライアントを中断する可能性を減らすために、com 参照可能な型からのみ派生しなければなりません。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、基本型 COM を参照できるようにするか、派生型 COM を非表示にします。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。

## <a name="example"></a>例
 次の例は、規則に違反する型を示しています。

 [!code-csharp[FxCop.Interoperability.ComBaseTypes#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Interoperability.ComBaseTypes/cs/FxCop.Interoperability.ComBaseTypes.cs#1)]
 [!code-vb[FxCop.Interoperability.ComBaseTypes#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Interoperability.ComBaseTypes/vb/FxCop.Interoperability.ComBaseTypes.vb#1)]

## <a name="see-also"></a>関連項目
 <xref:System.Runtime.InteropServices.ClassInterfaceAttribute?displayProperty=fullName>[クラスインターフェイスの概要](https://msdn.microsoft.com/733c0dd2-12e5-46e6-8de1-39d5b25df024)[アンマネージコードとの相互運用](https://msdn.microsoft.com/library/ccb68ce7-b0e9-4ffb-839d-03b1cd2c1258)
