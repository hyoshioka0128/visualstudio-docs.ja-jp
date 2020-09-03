---
title: 'CA1023: インデクサーを多次元にすることはできません |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- IndexersShouldNotBeMultidimensional
- CA1023
helpviewer_keywords:
- CA1023
- IndexersShouldNotBeMultidimensional
ms.assetid: ae499879-97f6-434e-a61d-1fedd231d2fb
caps.latest.revision: 16
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 30eee67d54e4fc3c73b265240fff82b0729e1cfc
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85546651"
---
# <a name="ca1023-indexers-should-not-be-multidimensional"></a>CA1023:インデクサーを多次元にすることはできません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|IndexersShouldNotBeMultidimensional|
|CheckId|CA1023|
|カテゴリ|Microsoft Design|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 パブリックまたはプロテクト型に、複数のインデックスを使用するパブリックまたは保護されたインデクサーが含まれています。

## <a name="rule-description"></a>ルールの説明
 インデクサー (つまり、インデックス付きプロパティ) では、1つのインデックスを使用する必要があります。 多次元インデクサーを使用すると、ライブラリの使いやすさが大幅に低下する可能性があります。 設計に複数のインデックスが必要な場合は、型が論理データストアを表すかどうかを再検討します。 それ以外の場合は、メソッドを使用します。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、唯一の整数または文字列インデックスを使用するようにデザインを変更するか、インデクサーではなくメソッドを使用します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 非標準のインデクサーの必要性を慎重に検討した後にのみ、この規則からの警告を非表示にします。

## <a name="example"></a>例
 次の例は、 `DayOfWeek03` ルールに違反する多次元インデクサーを持つ型を示しています。 インデクサーは変換の一種と見なすことができるため、メソッドとしてより適切に公開されます。 この型は、規則を満たすためにで再設計されてい `RedesignedDayOfWeek03` ます。

 [!code-cpp[FxCop.Design.OneDimensionForIndexer#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Design.OneDimensionForIndexer/cpp/FxCop.Design.OneDimensionForIndexer.cpp#1)]
 [!code-csharp[FxCop.Design.OneDimensionForIndexer#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.OneDimensionForIndexer/cs/FxCop.Design.OneDimensionForIndexer.cs#1)]
 [!code-vb[FxCop.Design.OneDimensionForIndexer#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.OneDimensionForIndexer/vb/FxCop.Design.OneDimensionForIndexer.vb#1)]

## <a name="related-rules"></a>関連規則
 [CA1043:インデクサーには整数または文字列引数を使用します](../code-quality/ca1043-use-integral-or-string-argument-for-indexers.md)

 [CA1024:適切な場所にプロパティを使用します](../code-quality/ca1024-use-properties-where-appropriate.md)
