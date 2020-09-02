---
title: 'CA1027: FlagsAttribute | で列挙をマークします。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- MarkEnumsWithFlags
- CA1027
helpviewer_keywords:
- CA1027
- MarkEnumsWithFlags
ms.assetid: 249e882c-8cd1-4c00-a2de-7b6bdc1849ff
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 774279dd05bd14c34df7f1d450f00599812d6a5b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85544509"
---
# <a name="ca1027-mark-enums-with-flagsattribute"></a>CA1027:列挙型を FlagsAttribute に設定します
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|MarkEnumsWithFlags|
|CheckId|CA1027|
|カテゴリ|Microsoft Design|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因
 パブリック列挙型の値は、2の累乗であるか、列挙体に定義されている他の値の組み合わせであり、 <xref:System.FlagsAttribute?displayProperty=fullName> 属性が存在しません。 誤検知を減らすために、このルールは連続した値を持つ列挙に対する違反を報告しません。

## <a name="rule-description"></a>ルールの説明
 列挙型は、関連する名前付き定数が複数定義された値型です。 <xref:System.FlagsAttribute>名前付き定数を明確に結合できる場合は、列挙体に適用します。 たとえば、アプリケーションの曜日を列挙して、使用可能なリソースを追跡する場合を考えてみます。 各リソースの可用性が、存在する列挙体を使用してエンコードされている場合は <xref:System.FlagsAttribute> 、日付の任意の組み合わせを表すことができます。 属性を指定しない場合は、1週間の曜日のみを表すことができます。

 組み合わせ可能な列挙体を格納するフィールドの場合、個々の列挙値はフィールド内のビットのグループとして扱われます。 そのため、このようなフィールドは、 *ビットフィールド*と呼ばれることもあります。 ビットフィールドに格納する列挙値を結合するには、ブール条件演算子を使用します。 ビットフィールドをテストして特定の列挙値が存在するかどうかを判断するには、ブール型の論理演算子を使用します。 ビットフィールドで結合された列挙値を正しく格納および取得するには、列挙体に定義されている各値が2の累乗である必要があります。 そうでない限り、ブール型の論理演算子は、フィールドに格納されている個々の列挙値を抽出できません。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、を <xref:System.FlagsAttribute> 列挙体に追加します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 列挙値を組み合わせ可能にしない場合は、この規則からの警告を非表示にします。

## <a name="example"></a>例
 次の例では、は、を `DaysEnumNeedsFlags` 使用するための要件を満たしていますが、それを持たない列挙体です <xref:System.FlagsAttribute> 。 `ColorEnumShouldNotHaveFlag`列挙体の値が2の累乗ではなく、誤って指定されてい <xref:System.FlagsAttribute> ます。 これは rule [CA2217 に違反します: FlagsAttribute で列挙をマークしません](../code-quality/ca2217-do-not-mark-enums-with-flagsattribute.md)。

 [!code-csharp[FxCop.Design.EnumFlags#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.EnumFlags/cs/FxCop.Design.EnumFlags.cs#1)]

## <a name="related-rules"></a>関連規則
 [CA2217:列挙型を FlagsAttribute に設定しません](../code-quality/ca2217-do-not-mark-enums-with-flagsattribute.md)

## <a name="see-also"></a>参照
 <xref:System.FlagsAttribute?displayProperty=fullName>
