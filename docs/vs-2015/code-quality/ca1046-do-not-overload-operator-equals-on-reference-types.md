---
title: 'CA1046: 参照型 | の演算子 equals をオーバーロードしませんMicrosoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- DoNotOverloadOperatorEqualsOnReferenceTypes
- CA1046
helpviewer_keywords:
- CA1046
- DoNotOverloadOperatorEqualsOnReferenceTypes
ms.assetid: c1dfbfe3-63f9-4005-a81a-890427b77e79
caps.latest.revision: 16
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 118c29473db09d5ed0a4fa447e27e593a88f98b3
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546758"
---
# <a name="ca1046-do-not-overload-operator-equals-on-reference-types"></a>CA1046:参照型で、演算子 equals をオーバーロードしないでください
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|DoNotOverloadOperatorEqualsOnReferenceTypes|
|CheckId|CA1046|
|カテゴリ|Microsoft Design|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 パブリックまたは入れ子にされたパブリック参照型は、等値演算子をオーバーロードします。

## <a name="rule-description"></a>ルールの説明
 参照型の場合、等値演算子は既定の実装でほぼ問題がありません。 既定で、2 つの参照が等値と見なされるのは、同じオブジェクトを参照する場合のみです。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、等値演算子の実装を削除します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 参照型が組み込みの値型のように動作する場合は、この規則からの警告を抑制することが安全です。 型のインスタンスに対して加算または減算を実行するのに意味がある場合は、等値演算子を実装し、違反を抑制することが適切な場合があります。

## <a name="example"></a>例
 次の例は、2つの参照を比較する場合の既定の動作を示しています。

 [!code-csharp[FxCop.Design.RefTypesNoEqualityOp#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.RefTypesNoEqualityOp/cs/FxCop.Design.RefTypesNoEqualityOp.cs#1)]

## <a name="example"></a>例
 次のアプリケーションは、一部の参照を比較します。

 [!code-csharp[FxCop.Design.TestRefTypesNoEqualityOp#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.TestRefTypesNoEqualityOp/cs/FxCop.Design.TestRefTypesNoEqualityOp.cs#1)]

 この例を実行すると、次の出力が生成されます。

 **a = new (2, 2) と b = new (2, 2) は等しいでしょうか。** 
 **C と a は同じですか?はい** 
 **b と a は = = ですか?** 
 **C と a は = = ですか?はい**
## <a name="related-rules"></a>関連規則
 [CA1013:オーバーロードする加算および減算で、演算子 equals をオーバーロードします](../code-quality/ca1013-overload-operator-equals-on-overloading-add-and-subtract.md)

## <a name="see-also"></a>関連項目
 <xref:System.Object.Equals%2A?displayProperty=fullName>[等値演算子](https://msdn.microsoft.com/library/bc496a91-fefb-4ce0-ab4c-61f09964119a)
