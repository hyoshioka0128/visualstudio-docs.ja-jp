---
title: 'CA1028: 列挙ストレージは Int32 | である必要がありますMicrosoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1028
- EnumStorageShouldBeInt32
helpviewer_keywords:
- EnumStorageShouldBeInt32
- CA1028
ms.assetid: 87160825-9f39-4142-8d7f-a31fe7ac7b84
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 0b2e8ebcc7720f5cd9dc6c700bcc08b68f89e275
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85542494"
---
# <a name="ca1028-enum-storage-should-be-int32"></a>CA1028:列挙ストレージは Int32 でなければなりません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|EnumStorageShouldBeInt32|
|CheckId|CA1028|
|カテゴリ|Microsoft Design|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 パブリック列挙型の基になる型がではありません <xref:System.Int32?displayProperty=fullName> 。

## <a name="rule-description"></a>ルールの説明
 列挙型は、関連する名前付き定数が複数定義された値型です。 既定では、 <xref:System.Int32?displayProperty=fullName> データ型は定数値を格納するために使用されます。 この基になる型を変更することはできますが、ほとんどのシナリオでは必須ではなく、推奨もされません。 より小さいデータ型を使用しても、パフォーマンスが大幅に向上するわけではないことに注意 <xref:System.Int32> してください。 既定のデータ型を使用できない場合は、共通言語システム (cls) に準拠している整数型、、、、またはのいずれかを使用し <xref:System.Byte> て、 <xref:System.Int16> <xref:System.Int32> <xref:System.Int64> 列挙型のすべての値を CLS 準拠のプログラミング言語で表すことができるようにする必要があります。

## <a name="how-to-fix-violations"></a>違反の修正方法
 サイズや互換性の問題が存在する場合を除き、この規則違反を修正するには、を使用 <xref:System.Int32> します。 <xref:System.Int32>が値を保持するのに十分な大きさでない場合は、を使用 <xref:System.Int64> します。 旧バージョンとの互換性のためにより小さいデータ型が必要な場合 <xref:System.Byte> は、またはを使用 <xref:System.Int16> します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 旧バージョンとの互換性の問題に必要な場合にのみ、この規則の警告を非表示にします。 アプリケーションでは、この規則に準拠していないと、通常、問題は発生しません。 言語の相互運用性が必要なライブラリでは、この規則に準拠していないと、ユーザーに悪影響を及ぼす可能性があります。

## <a name="example-of-a-violation"></a>違反の例

### <a name="description"></a>説明
 次の例は、推奨される基になるデータ型を使用しない2つの列挙を示しています。

### <a name="code"></a>コード
 [!code-csharp[FxCop.Design.EnumIntegralType#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.EnumIntegralType/cs/FxCop.Design.EnumIntegralType.cs#1)]
 [!code-vb[FxCop.Design.EnumIntegralType#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.EnumIntegralType/vb/FxCop.Design.EnumIntegralType.vb#1)]

## <a name="example-of-how-to-fix"></a>修正方法の例

### <a name="description"></a>説明
 次の例では、基になるデータ型をに変更することで、以前の違反を修正し <xref:System.Int32> ます。

### <a name="code"></a>コード
 [!code-csharp[FxCop.Design.EnumIntegralTypeFixed#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.EnumIntegralTypeFixed/cs/FxCop.Design.EnumIntegralTypeFixed.cs#1)]
 [!code-vb[FxCop.Design.EnumIntegralTypeFixed#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.EnumIntegralTypeFixed/vb/FxCop.Design.EnumIntegralTypeFixed.vb#1)]

## <a name="related-rules"></a>関連規則
 [CA1008:Enums は 0 値を含んでいなければなりません](../code-quality/ca1008-enums-should-have-zero-value.md)

 [CA1027:列挙型を FlagsAttribute に設定します](../code-quality/ca1027-mark-enums-with-flagsattribute.md)

 [CA2217:列挙型を FlagsAttribute に設定しません](../code-quality/ca2217-do-not-mark-enums-with-flagsattribute.md)

 [CA1700:列挙型値に 'Reserved' という名前を指定しません](../code-quality/ca1700-do-not-name-enum-values-reserved.md)

 [CA1712:列挙型値を型名のプレフィックスにしません](../code-quality/ca1712-do-not-prefix-enum-values-with-type-name.md)

## <a name="see-also"></a>参照
 <xref:System.Byte?displayProperty=fullName> <xref:System.Int16?displayProperty=fullName>
 <xref:System.Int32?displayProperty=fullName>
 <xref:System.Int64?displayProperty=fullName>
