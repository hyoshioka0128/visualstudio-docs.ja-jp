---
title: 'CA1721: プロパティ名は get メソッド | と一致させることはできませんMicrosoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1721
- PropertyNamesShouldNotMatchGetMethods
helpviewer_keywords:
- CA1721
- PropertyNamesShouldNotMatchGetMethods
ms.assetid: 45a0e853-1f06-4688-af1b-cc634409e295
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 77ec48a1164c7065ba5033ef51eb704b8361dc1c
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544457"
---
# <a name="ca1721-property-names-should-not-match-get-methods"></a>CA1721:プロパティ名は get メソッドと同一にすることはできません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|アイテム|値|
|-|-|
|TypeName|PropertyNamesShouldNotMatchGetMethods|
|CheckId|CA1721|
|カテゴリ|Microsoft.Naming|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 パブリックメンバーまたはプロテクトメンバーの名前は、' Get ' で始まり、それ以外の場合は、public または protected プロパティの名前と一致します。 たとえば、' GetColor ' という名前のメソッドを含む型と、' Color ' という名前のプロパティは、この規則に違反します。

## <a name="rule-description"></a>ルールの説明
 Get メソッドとプロパティには、その関数を明確に区別する名前を付ける必要があります。

 名前付け規則では、共通言語ランタイムをターゲットとするライブラリの統一的な名前の付け方が規定されています。 これにより、新しいソフトウェアライブラリを学習するために必要な時間が短縮され、マネージコードの開発に関する専門知識を持つユーザーによってライブラリが開発されたという自信が高まります。

## <a name="how-to-fix-violations"></a>違反の修正方法
 名前を変更して、先頭に ' Get ' が付いているメソッドの名前と一致しないようにします。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。

> [!NOTE]
> この警告は、Get メソッドが IExtenderProvider インターフェイスの実装によって発生した場合に除外される可能性があります。

## <a name="example"></a>例
 次の例には、この規則に違反するメソッドとプロパティが含まれています。

 [!code-csharp[FxCop.Naming.GetMethod#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Naming.GetMethod/cs/FxCop.Naming.GetMethod.cs#1)]
 [!code-vb[FxCop.Naming.GetMethod#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Naming.GetMethod/vb/FxCop.Naming.GetMethod.vb#1)]

## <a name="related-rules"></a>関連規則
 [CA1024:適切な場所にプロパティを使用します](../code-quality/ca1024-use-properties-where-appropriate.md)
