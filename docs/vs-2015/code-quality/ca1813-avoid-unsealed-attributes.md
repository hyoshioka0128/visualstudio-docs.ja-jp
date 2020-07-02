---
title: 'CA1813: 封印されていない属性を避けます。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1813
- AvoidUnsealedAttributes
helpviewer_keywords:
- CA1813
- AvoidUnsealedAttributes
ms.assetid: f5e31b4c-9f8b-49e1-a2a8-bb5f1140729a
caps.latest.revision: 15
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 8d86f4a9ecbdfff451fed21f93c0fe6a7679d471
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85543950"
---
# <a name="ca1813-avoid-unsealed-attributes"></a>CA1813:アンシールド属性を使用しません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|アイテム|値|
|-|-|
|TypeName|AvoidUnsealedAttributes|
|CheckId|CA1813|
|カテゴリ|Microsoft. パフォーマンス|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 パブリック型がから継承されて <xref:System.Attribute?displayProperty=fullName> おり、が abstract ではなく、シールされていません ( `NotInheritable` Visual Basic)。

## <a name="rule-description"></a>ルールの説明
 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] クラス ライブラリには、カスタム属性を取得するメソッドが用意されています。 既定では、これらのメソッドは属性の継承階層を検索します。たとえば、指定された属性の型、または指定された属性の型を <xref:System.Attribute.GetCustomAttribute%2A?displayProperty=fullName> 拡張する任意の属性の型を検索します。 属性をシールすると、継承階層での検索が不要になり、パフォーマンスが向上します。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、属性の型を封印するか、抽象にします。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 このルールからの警告を抑制するのは安全です。 この操作は、属性階層を定義する場合にのみ実行してください。属性を封印したり、抽象にしたりすることはできません。

## <a name="example"></a>例
 次の例は、この規則を満たすカスタム属性を示しています。

 [!code-csharp[FxCop.Performance.AttributesSealed#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Performance.AttributesSealed/cs/FxCop.Performance.AttributesSealed.cs#1)]
 [!code-vb[FxCop.Performance.AttributesSealed#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Performance.AttributesSealed/vb/FxCop.Performance.AttributesSealed.vb#1)]

## <a name="related-rules"></a>関連規則
 [CA1019:属性引数にアクセサーを定義します](../code-quality/ca1019-define-accessors-for-attribute-arguments.md)

 [CA1018:属性を AttributeUsageAttribute に設定します](../code-quality/ca1018-mark-attributes-with-attributeusageattribute.md)

## <a name="see-also"></a>関連項目
 [属性](https://msdn.microsoft.com/library/ee0038ef-b247-4747-a650-3c5c5cd58d8b)
