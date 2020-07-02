---
title: 'CA1506: クラスの結合が過剰にならないようにする |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- AvoidExcessiveClassCoupling
- CA1506
helpviewer_keywords:
- AvoidExcessiveClassCoupling
- CA1506
ms.assetid: 9f0943c0-e802-4e3f-8798-2ab8653ddc80
caps.latest.revision: 14
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 07f19cb9d4aa2ed118898a1816092479cbd16565
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545705"
---
# <a name="ca1506-avoid-excessive-class-coupling"></a>CA1506:クラス結合度を大きくしすぎないでください
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|アイテム|値|
|-|-|
|TypeName|AvoidExcessiveClassCoupling|
|CheckId|CA1506|
|カテゴリ|Microsoft の保守容易性|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 型またはメソッドは、他の多くの型と結合されます。

## <a name="rule-description"></a>ルールの説明
 この規則は、型またはメソッドに含まれる一意の型参照の数をカウントすることによって、クラス結合度を計測します。

 クラスの結合度が高い型およびメソッドは、保守が困難な場合があります。 結合率が低く、高い凝集度を示す型とメソッドを用意することをお勧めします。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この違反を修正するには、型またはメソッドを再設計して、結合される型の数を減らしてみてください。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 他の型に対する依存関係の数が多いにもかかわらず、型またはメソッドが保守容易と見なされる場合は、この警告を除外します。

## <a name="see-also"></a>関連項目
 [マネージコードの複雑さと保守性を測定する、](../code-quality/measuring-complexity-and-maintainability-of-managed-code.md) [保守性](../code-quality/maintainability-warnings.md)に関する警告
