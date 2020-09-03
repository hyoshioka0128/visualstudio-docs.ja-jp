---
title: 'CA1018: Mark 属性と AttributeUsageAttribute |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1018
- MarkAttributesWithAttributeUsage
helpviewer_keywords:
- CA1018
- MarkAttributesWithAttributeUsage
ms.assetid: 6ab70ec0-220f-4880-af31-45067703133c
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 256fc281b27c483f1dda0317f7d2695fa36c47f8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85535058"
---
# <a name="ca1018-mark-attributes-with-attributeusageattribute"></a>CA1018:属性を AttributeUsageAttribute に設定します
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|MarkAttributesWithAttributeUsage|
|CheckId|CA1018|
|カテゴリ|Microsoft Design|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 この <xref:System.AttributeUsageAttribute?displayProperty=fullName> 属性はカスタム属性に存在しません。

## <a name="rule-description"></a>ルールの説明
 カスタム属性を定義するときは、を使用して、 <xref:System.AttributeUsageAttribute> カスタム属性を適用できるソースコード内の場所を指定します。 属性の意味と用途によって、コード内の有効な位置が決まります。 たとえば、ライブラリ内の各型を管理および強化する担当者を識別する属性を定義し、その責任は常に型レベルで割り当てられます。 この場合、コンパイラはクラス、列挙、およびインターフェイスの属性を有効にする必要がありますが、メソッド、イベント、またはプロパティで有効にしないでください。 組織のポリシーと手順では、アセンブリで属性を有効にするかどうかを指定します。

 <xref:System.AttributeTargets?displayProperty=fullName>列挙体は、カスタム属性に対して指定できるターゲットを定義します。 を省略した場合 <xref:System.AttributeUsageAttribute> 、カスタム属性は、 `All` 列挙体の値で定義されているすべてのターゲットに対して有効になり <xref:System.AttributeTargets> ます。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、を使用して、属性のターゲットを指定し <xref:System.AttributeUsageAttribute> ます。 次の例を参照してください。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 メッセージを除外するのではなく、このルールの違反を修正する必要があります。 属性が継承されている場合でも <xref:System.AttributeUsageAttribute> 、コードの保守を簡素化するために属性が存在している必要があります。

## <a name="example"></a>例
 次の例では、2つの属性を定義します。 `BadCodeMaintainerAttribute` ステートメントを誤っ <xref:System.AttributeUsageAttribute> て省略し、 `GoodCodeMaintainerAttribute` このセクションの前半で説明した属性を正しく実装します。 このプロパティは、 `DeveloperName` デザイン規則 [CA1019: 属性引数に対してアクセサーを定義](../code-quality/ca1019-define-accessors-for-attribute-arguments.md) する必要があり、完全を期すために含まれています。

 [!code-csharp[FxCop.Design.AttributeUsage#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.AttributeUsage/cs/FxCop.Design.AttributeUsage.cs#1)]
 [!code-vb[FxCop.Design.AttributeUsage#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.AttributeUsage/vb/FxCop.Design.AttributeUsage.vb#1)]

## <a name="related-rules"></a>関連規則
 [CA1019:属性引数にアクセサーを定義します](../code-quality/ca1019-define-accessors-for-attribute-arguments.md)

 [CA1813:アンシールド属性を使用しません](../code-quality/ca1813-avoid-unsealed-attributes.md)

## <a name="see-also"></a>参照
 [属性](https://msdn.microsoft.com/library/ee0038ef-b247-4747-a650-3c5c5cd58d8b)
