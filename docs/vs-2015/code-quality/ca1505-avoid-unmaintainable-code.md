---
title: 'CA1505: メンテナンスできないコードを回避する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- AvoidUnmaintainableCode
- CA1505
helpviewer_keywords:
- AvoidUnmaintainableCode
- CA1505
ms.assetid: 8292b268-5929-4221-b699-f9c414bcec5d
caps.latest.revision: 16
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 0f2f731b1ac0d87b59c7690d0cf57ade3570ed5f
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547824"
---
# <a name="ca1505-avoid-unmaintainable-code"></a>CA1505:メンテナンスできないコードを使用しないでください
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|アイテム|値|
|-|-|
|TypeName|AvoidUnmantainableCode|
|CheckId|CA1505|
|カテゴリ|Microsoft の保守容易性|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因
 型またはメソッドの保守容易性指数が低い値です。

## <a name="rule-description"></a>ルールの説明
 保守容易性のインデックスは、コード行、プログラムボリューム、およびサイクロマティック複雑性の各メトリックを使用して計算されます。 プログラムボリュームは、コード内の演算子とオペランドの数に基づいて、型またはメソッドを理解しづらいことを示す尺度です。 サイクロマティック複雑度は、型またはメソッドの構造上の複雑さの尺度です。 コードメトリックスの詳細については[、「マネージコードの複雑さと保守性の測定](../code-quality/measuring-complexity-and-maintainability-of-managed-code.md)」を参照してください。

 保守性の低いインデックスは、型またはメソッドの保守が困難であり、再設計するのが適切であることを示しています。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この違反を修正するには、型またはメソッドを再設計し、それをより小さな、フォーカスのある型またはメソッドに分割します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この警告は、型またはメソッドが、大きなサイズの場合や、型またはメソッドを分割できない場合でも保守が容易であると見なされる場合には除外されます。

## <a name="see-also"></a>関連項目
 [マネージコードの複雑さと保守性を測定する、](../code-quality/measuring-complexity-and-maintainability-of-managed-code.md) [保守性](../code-quality/maintainability-warnings.md)に関する警告
