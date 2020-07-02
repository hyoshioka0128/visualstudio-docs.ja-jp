---
title: 'CA2126: 型のリンク要求には継承要求が必要です |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2126
- TypeLinkDemandsRequireInheritanceDemands
helpviewer_keywords:
- CA2126
- TypeLinkDemandsRequireInheritanceDemands
ms.assetid: 07b604e5-5579-4df9-a578-dadd0d8370a7
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 051a041c245fae55e3d4759130c145c662734aa8
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544275"
---
# <a name="ca2126-type-link-demands-require-inheritance-demands"></a>CA2126:型のリンク要求には継承要求が必要です
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|アイテム|値|
|-|-|
|TypeName|TypeLinkDemandsRequireInheritanceDemands|
|CheckId|CA2126|
|カテゴリ|Microsoft.Security|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 パブリックに封印されていない型はリンク確認要求で保護され、オーバーライド可能なメソッドを持っています。また、型もメソッドも継承要求で保護されていません。

## <a name="rule-description"></a>ルールの説明
 メソッドまたはその宣言する型に対するリンク確認要求を行うには、メソッドの直前の呼び出し元に、指定されたアクセス許可が必要です。 メソッドに対する継承要求では、指定されたアクセス許可を持つオーバーライドメソッドが必要です。 型に対する継承要求では、指定されたアクセス許可を持つ派生クラスが必要です。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、リンク確認要求と同じアクセス許可の継承要求で、型またはメソッドをセキュリティで保護します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。

## <a name="example"></a>例
 次の例は、規則に違反する型を示しています。

 [!code-cpp[FxCop.Security.TypesWithLinkDemands#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Security.TypesWithLinkDemands/cpp/FxCop.Security.TypesWithLinkDemands.cpp#1)]
 [!code-csharp[FxCop.Security.TypesWithLinkDemands#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.TypesWithLinkDemands/cs/FxCop.Security.TypesWithLinkDemands.cs#1)]
 [!code-vb[FxCop.Security.TypesWithLinkDemands#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Security.TypesWithLinkDemands/vb/FxCop.Security.TypesWithLinkDemands.vb#1)]

## <a name="related-rules"></a>関連規則
 [CA2108:値型での宣言セキュリティを確認します](../code-quality/ca2108-review-declarative-security-on-value-types.md)

 [CA2112:セキュリティで保護された型はフィールドを公開してはなりません](../code-quality/ca2112-secured-types-should-not-expose-fields.md)

 [CA2122:リンク要求を含むメソッドを間接的に公開しません](../code-quality/ca2122-do-not-indirectly-expose-methods-with-link-demands.md)

 [CA2123:オーバーライドのリンク要求はベースと同一でなければなりません](../code-quality/ca2123-override-link-demands-should-be-identical-to-base.md)

## <a name="see-also"></a>関連項目
 [セキュリティで保護されたコーディングガイドライン](https://msdn.microsoft.com/library/4f882d94-262b-4494-b0a6-ba9ba1f5f177)の[継承要求](https://msdn.microsoft.com/28b9adbb-8f08-4f10-b856-dbf59eb932d9)の[リンク](https://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d)[確認要求](https://msdn.microsoft.com/e5283e28-2366-4519-b27d-ef5c1ddc1f48)
