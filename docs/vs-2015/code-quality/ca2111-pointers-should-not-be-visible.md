---
title: 'CA2111: ポインターを visible にすることはできません。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- PointersShouldNotBeVisible
- CA2111
helpviewer_keywords:
- CA2111
- PointersShouldNotBeVisible
ms.assetid: b3a8d466-895b-43bc-a2df-5d7058fe915f
caps.latest.revision: 16
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 7429251a66ce2fe22a825a153cb90248faabb9fd
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544366"
---
# <a name="ca2111-pointers-should-not-be-visible"></a>CA2111:ポインターは参照可能にすることはできません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|PointersShouldNotBeVisible|
|CheckId|CA2111|
|カテゴリ|Microsoft.Security|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 Public、protected、 <xref:System.IntPtr?displayProperty=fullName> または field は読み取り専用では <xref:System.UIntPtr?displayProperty=fullName> ありません。

## <a name="rule-description"></a>ルールの説明
 <xref:System.IntPtr>および <xref:System.UIntPtr> は、アンマネージメモリにアクセスするために使用されるポインター型です。 ポインターがプライベート、内部、または読み取り専用ではない場合、悪意のあるコードがポインターの値を変更して、メモリ内の任意の場所へのアクセスを許可したり、アプリケーションやシステムの障害を引き起こしたりする可能性があります。

 ポインターフィールドを含む型へのアクセスをセキュリティで保護する場合は、「 [CA2112: セキュリティで保護された型はフィールドを公開しない](../code-quality/ca2112-secured-types-should-not-expose-fields.md)」を参照してください。

## <a name="how-to-fix-violations"></a>違反の修正方法
 読み取り専用、内部、またはプライベートにして、ポインターをセキュリティで保護します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 ポインターの値に依存しない場合は、このルールの警告を非表示にします。

## <a name="example"></a>例
 次のコードは、規則に違反しているポインターを示しています。 非プライベートポインターもルール CA1051 に違反していることに注意してください。[表示インスタンスフィールドを宣言しません](../code-quality/ca1051-do-not-declare-visible-instance-fields.md)。

 [!code-csharp[FxCop.Security.PointersArePrivate#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.PointersArePrivate/cs/FxCop.Security.PointersArePrivate.cs#1)]

## <a name="related-rules"></a>関連規則
 [CA2112:セキュリティで保護された型はフィールドを公開してはなりません](../code-quality/ca2112-secured-types-should-not-expose-fields.md)

 [CA1051:参照可能なインスタンス フィールドを宣言しません](../code-quality/ca1051-do-not-declare-visible-instance-fields.md)

## <a name="see-also"></a>関連項目
 <xref:System.IntPtr?displayProperty=fullName> <xref:System.UIntPtr?displayProperty=fullName>
