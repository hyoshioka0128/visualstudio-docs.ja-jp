---
title: 'CA1034: 入れ子にされた型を visible にすることはできません |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- NestedTypesShouldNotBeVisible
- CA1034
helpviewer_keywords:
- NestedTypesShouldNotBeVisible
- CA1034
ms.assetid: e9789a2c-2540-42a1-8705-ae7104011194
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 04a982c993ffbb04a3e7600dfb93a00e80727b84
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85542169"
---
# <a name="ca1034-nested-types-should-not-be-visible"></a>CA1034:入れ子にされた型を参照可能にすることはできません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|NestedTypesShouldNotBeVisible|
|CheckId|CA1034|
|カテゴリ|Microsoft Design|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 外部から参照できる型に、外部から参照できる型宣言が含まれています。 入れ子になった列挙型とプロテクト型は、この規則から除外されます。

## <a name="rule-description"></a>ルールの説明
 入れ子になった型は、別の型のスコープ内で宣言された型です。 入れ子になった型は、含んでいる型のプライベート実装の詳細をカプセル化する場合に便利です。 このような用途なので、入れ子にされた型は外部から参照できないようにします。

 論理グループまたは名前の競合を避けるために、外部から参照できる入れ子になった型を使用しないでください。代わりに、名前空間を使用します。

 入れ子になった型には、メンバーアクセシビリティの概念が含まれており、プログラマによってはわかりにくくなります。

 保護された型は、高度なカスタマイズシナリオでサブクラスおよび入れ子にされた型で使用できます。

## <a name="how-to-fix-violations"></a>違反の修正方法
 入れ子になった型を外部から参照できるようにしない場合は、型のアクセシビリティを変更します。 それ以外の場合は、入れ子になった型を親から削除します。 入れ子になった型を分類することが目的である場合は、代わりに名前空間を使用して階層を作成します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。

## <a name="example"></a>例
 次の例は、規則に違反する型を示しています。

 [!code-cpp[FxCop.Design.NestedTypes#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Design.NestedTypes/cpp/FxCop.Design.NestedTypes.cpp#1)]
 [!code-csharp[FxCop.Design.NestedTypes#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.NestedTypes/cs/FxCop.Design.NestedTypes.cs#1)]
 [!code-vb[FxCop.Design.NestedTypes#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.NestedTypes/vb/FxCop.Design.NestedTypes.vb#1)]
