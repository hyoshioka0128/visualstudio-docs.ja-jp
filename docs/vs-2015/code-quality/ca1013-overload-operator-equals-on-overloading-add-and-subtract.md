---
title: 'CA1013: オーバーロードされた加算および減算 | で、演算子 equals をオーバーロードします。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- OverrideOperatorEqualsOnOverridingAddAndSubtract
- OverrideOperatorEqualsOnOverloadingAddAndSubtract
- CA1013
- OverloadOperatorEqualsOnOverloadingAddAndSubtract
helpviewer_keywords:
- OverrideOperatorEqualsOnOverloadingAddAndSubtract
- OverrideOperatorEqualsOnOverridingAddAndSubtract
- CA1013
- OverloadOperatorEqualsOnOverloadingAddAndSubtract
ms.assetid: 5bd28d68-c179-49ff-af47-5250b8b18a10
caps.latest.revision: 24
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: dd1c144f04150e3965e2c0264b80147cbd9b8f19
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72663213"
---
# <a name="ca1013-overload-operator-equals-on-overloading-add-and-subtract"></a>CA1013: オーバーロードする加算および減算で、演算子 equals をオーバーロードします
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|OverloadOperatorEqualsOnOverloadingAddAndSubtract|
|CheckId|CA1013|
|カテゴリ|Microsoft.Design|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因
 パブリック型またはプロテクト型で、等値演算子を実装しないまま、加算演算子または減算演算子を実装しています。

## <a name="rule-description"></a>規則の説明
 加算や減算などの演算を使用して型のインスタンスを組み合わせることができる場合は、ほぼ常に等しいかどうかを定義して、同じ構成値を持つ任意の2つのインスタンスに対して `true` を返す必要があります。

 等値演算子のオーバーロードされた実装では、既定の等値演算子を使用できません。 そうすると、スタックオーバーフローが発生します。 等値演算子を実装するには、実装で Object.equals メソッドを使用します。 次の例を参照してください。

```vb
If (Object.ReferenceEquals(left, Nothing)) Then
    Return Object.ReferenceEquals(right, Nothing)
Else
    Return left.Equals(right)
End If
```

```csharp
if (Object.ReferenceEquals(left, null))
    return Object.ReferenceEquals(right, null);
return left.Equals(right);
```

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、加算および減算演算子と数学的に一致するように等値演算子を実装します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 等値演算子の既定の実装で型の正しい動作が提供されている場合は、この規則による警告を抑制しても安全です。

## <a name="example"></a>例
 次の例では、この規則に違反する型 (`BadAddableType`) を定義しています。 この型は、等値演算子を実装して、同じフィールド値を持つ2つのインスタンスが等しいかどうかをテスト `true` ようにする必要があります。 `GoodAddableType` 型は、修正された実装を示します。 この型は、非等値演算子も実装し、他の規則を満たすように <xref:System.Object.Equals%2A> をオーバーライドすることに注意してください。 完全な実装では、<xref:System.Object.GetHashCode%2A>も実装します。

 [!code-csharp[FxCop.Design.AddAndSubtract#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.AddAndSubtract/cs/FxCop.Design.AddAndSubtract.cs#1)]

## <a name="example"></a>例
 次の例では、このトピックで以前に定義した型のインスタンスを使用して、等値演算子の既定の動作と正しい動作を示すことにより、等しいかどうかをテストします。

 [!code-csharp[FxCop.Design.TestAddAndSubtract#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.TestAddAndSubtract/cs/FxCop.Design.TestAddAndSubtract.cs#1)]

 この例を実行すると、次の出力が生成されます。

 **不適切な型: {2,2} {2,2} が等しいかどうかを確認してください。** 
**適切な種類ではありません: {3,3} {3,3} は同じですか?はい**
**適切な種類: {3,3} {3,3} = =?  はい**
**無効な型です: {2,2} {9,9} が等しいかどうかを確認してください。** 
**適切な型ではありません: {3,3} {9,9} は = = ですか?  いいえ**
## <a name="see-also"></a>関連項目
 [等値演算子](https://msdn.microsoft.com/library/bc496a91-fefb-4ce0-ab4c-61f09964119a)
