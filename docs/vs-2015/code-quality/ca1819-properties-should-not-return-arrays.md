---
title: 'CA1819: プロパティは配列を返すことはできません |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- PropertiesShouldNotReturnArrays
- CA1819
helpviewer_keywords:
- PropertiesShouldNotReturnArrays
- CA1819
ms.assetid: 85fcf312-57f8-438a-8b10-34441fe0bdeb
caps.latest.revision: 24
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: a96d2164cbd6c03cb0d191b2d0c3c4607468209c
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545328"
---
# <a name="ca1819-properties-should-not-return-arrays"></a>CA1819:プロパティは、配列を返すことはできません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|アイテム|値|
|-|-|
|TypeName|PropertiesShouldNotReturnArrays|
|CheckId|CA1819|
|カテゴリ|Microsoft. パフォーマンス|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 パブリック型またはプロテクトプロパティは、配列を返します。

## <a name="rule-description"></a>ルールの説明
 プロパティが読み取り専用の場合でも、プロパティによって返される配列は書き込み禁止されません。 配列の改ざんを防ぐには、プロパティで配列のコピーを返す必要があります。 一般に、このようなプロパティを呼び出すときのパフォーマンス低下は理解されません。 具体的には、プロパティをインデックス付きプロパティとして使用することがあります。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、プロパティをメソッドに設定するか、コレクションを返すようにプロパティを変更します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 属性には、配列を返すプロパティを含めることができますが、コレクションを返すプロパティを含めることはできません。 [System.string] から派生した属性のプロパティに対して発生する警告を抑制できます (<!-- TODO: review code entity reference <xref:assetId:///System.Attribute?qualifyHint=False&amp;autoUpgrade=True>  -->講義. それ以外の場合は、このルールからの警告を抑制しないでください。

## <a name="example-violation"></a>違反の例

### <a name="description"></a>説明
 次の例は、この規則に違反するプロパティを示しています。

### <a name="code"></a>コード
 [!code-csharp[FxCop.Performance.PropertyArrayViolation#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Performance.PropertyArrayViolation/cs/FxCop.Performance.PropertyArrayViolation.cs#1)]
 [!code-vb[FxCop.Performance.PropertyArrayViolation#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Performance.PropertyArrayViolation/vb/FxCop.Performance.PropertyArrayViolation.vb#1)]

### <a name="comments"></a>コメント
 この規則違反を修正するには、プロパティをメソッドに設定するか、配列ではなくコレクションを返すようにプロパティを変更します。

## <a name="change-the-property-to-a-method-example"></a>プロパティをメソッドの例に変更する

### <a name="description"></a>説明
 次の例では、プロパティをメソッドに変更することによって、違反を修正します。

### <a name="code"></a>コード
 [!code-csharp[FxCop.Performance.PropertyArrayFixedMethod#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Performance.PropertyArrayFixedMethod/cs/FxCop.Performance.PropertyArrayFixedMethod.cs#1)]
 [!code-vb[FxCop.Performance.PropertyArrayFixedMethod#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Performance.PropertyArrayFixedMethod/vb/FxCop.Performance.PropertyArrayFixedMethod.vb#1)]

## <a name="return-a-collection-example"></a>コレクションの例を返す

### <a name="description"></a>説明
 次の例では、プロパティを変更してを返すことによって、違反を修正します。

 <xref:System.Collections.ObjectModel.ReadOnlyCollection%601?displayProperty=fullName>.

### <a name="code"></a>コード
 [!code-csharp[FxCop.Performance.PropertyArrayFixedCollection#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Performance.PropertyArrayFixedCollection/cs/FxCop.Performance.PropertyArrayFixedCollection.cs#1)]
 [!code-vb[FxCop.Performance.PropertyArrayFixedCollection#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Performance.PropertyArrayFixedCollection/vb/FxCop.Performance.PropertyArrayFixedCollection.vb#1)]

## <a name="allowing-users-to-modify-a-property"></a>ユーザーがプロパティを変更できるようにする

### <a name="description"></a>説明
 クラスのコンシューマーがプロパティを変更できるようにすることができます。 次の例は、この規則に違反する読み取り/書き込みプロパティを示しています。

### <a name="code"></a>コード
 [!code-csharp[FxCop.Performance.PropertyModifyViolation#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Performance.PropertyModifyViolation/cs/FxCop.Performance.PropertyModifyViolation.cs#1)]
 [!code-vb[FxCop.Performance.PropertyModifyViolation#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Performance.PropertyModifyViolation/vb/FxCop.Performance.PropertyModifyViolation.vb#1)]

### <a name="comments"></a>コメント
 次の例では、プロパティを変更してを返すことによって、違反を修正し <xref:System.Collections.ObjectModel.Collection%601?displayProperty=fullName> ます。

### <a name="code"></a>コード
 [!code-csharp[FxCop.Performance.PropertyModifyFixed#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Performance.PropertyModifyFixed/cs/FxCop.Performance.PropertyModifyFixed.cs#1)]
 [!code-vb[FxCop.Performance.PropertyModifyFixed#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Performance.PropertyModifyFixed/vb/FxCop.Performance.PropertyModifyFixed.vb#1)]

## <a name="related-rules"></a>関連規則
 [CA1024:適切な場所にプロパティを使用します](../code-quality/ca1024-use-properties-where-appropriate.md)
