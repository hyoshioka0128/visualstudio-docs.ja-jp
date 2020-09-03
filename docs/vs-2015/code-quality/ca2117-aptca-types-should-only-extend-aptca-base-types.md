---
title: 'CA2117: APTCA 型は APTCA 基本型を拡張する必要があります |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2117
- AptcaTypesShouldOnlyExtendAptcaBaseTypes
helpviewer_keywords:
- AptcaTypesShouldOnlyExtendAptcaBaseTypes
- CA2117
ms.assetid: c505b586-2f1e-47cb-98ee-a5afcbeda70f
caps.latest.revision: 18
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 90c1f66f36fc689ee077ec66f154487d65ee13a1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85543612"
---
# <a name="ca2117-aptca-types-should-only-extend-aptca-base-types"></a>CA2117:APTCA 型は APTCA 基本型のみを拡張することができます
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|AptcaTypesShouldOnlyExtendAptcaBaseTypes|
|CheckId|CA2117|
|カテゴリ|Microsoft.Security|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 属性を持つアセンブリ内のパブリック型またはプロテクト型が、 <xref:System.Security.AllowPartiallyTrustedCallersAttribute?displayProperty=fullName> 属性を持たないアセンブリで宣言されている型から継承されています。

## <a name="rule-description"></a>ルールの説明
 既定では、厳密な名前を持つアセンブリ内のパブリック型またはプロテクト型は、完全信頼の [継承要求](https://msdn.microsoft.com/28b9adbb-8f08-4f10-b856-dbf59eb932d9) によって暗黙的に保護されます。 (APTCA) 属性でマークされた厳密な名前付きのアセンブリには、 <xref:System.Security.AllowPartiallyTrustedCallersAttribute> この保護はありません。 属性は、継承の要求を無効にします。 これにより、完全に信頼されていない型によって継承可能なアセンブリ内で宣言された型が作成されます。

 APTCA 属性が完全に信頼されたアセンブリに存在し、アセンブリ内の型が部分的に信頼された呼び出し元を許可しない型から継承する場合、セキュリティ上の脆弱性が発生する可能性があります。 2つの型が `T1` `T2` あり、次の条件を満たす場合、悪意のある呼び出し元は型を使用して、を `T1` 保護する暗黙的な完全信頼の継承要求をバイパスでき `T2` ます。

- `T1` は、APTCA 属性を持つ、完全に信頼されたアセンブリで宣言されたパブリック型です。

- `T1` アセンブリ外の型から継承 `T2` します。

- `T2`のアセンブリには APTCA 属性がないため、部分的に信頼されたアセンブリの型によって継承できません。

  部分的に信頼された型は `X` 、から継承できます。これに `T1` より、で宣言された継承されたメンバーにアクセスできるようになり `T2` ます。 に `T2` は APTCA 属性がないため、その直接の派生型 () は、 `T1` 完全な信頼の継承要求を満たす必要があります。 `T1` 完全な信頼があるため、このチェックが満たされます。 セキュリティ上のリスクは、が信頼されていないサブ `X` クラスから保護する継承要求の満たさに関与しないためです `T2` 。 このため、APTCA 属性を持つ型では、属性を持たない型を拡張することはできません。

  もう1つのセキュリティの問題として、一般的には、派生型 ( `T1` ) がプログラマのエラーによって、完全な信頼を必要とする型からプロテクトメンバーを公開する () ことがあり `T2` ます。 これが発生すると、信頼されていない呼び出し元は、完全に信頼された型にのみ使用できる情報にアクセスできます。

## <a name="how-to-fix-violations"></a>違反の修正方法
 違反によって報告された型が、APTCA 属性を必要としないアセンブリにある場合は、それを削除します。

 APTCA 属性が必要な場合は、完全信頼の継承要求を型に追加します。 これにより、信頼されていない型による継承から保護されます。

 違反によって報告された基本型のアセンブリに APTCA 属性を追加することによって、違反を修正することができます。 この操作を行わないでください。まず、アセンブリ内のすべてのコードと、アセンブリに依存するすべてのコードのセキュリティレビューを頻繁に実行する必要があります。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則からの警告を安全に抑制するには、型によって公開されているプロテクトメンバーが、信頼されていない呼び出し元に、破壊的な方法で使用できる機微な情報、操作、またはリソースへのアクセスを直接または間接的に許可しないようにする必要があります。

## <a name="example"></a>例
 次の例では、2つのアセンブリとテストアプリケーションを使用して、この規則によって検出されたセキュリティの脆弱性を示しています。 最初のアセンブリには APTCA 属性がなく、部分的に信頼された型 (前の説明ではによって表される) によって継承することはできません `T2` 。

 [!code-csharp[FxCop.Security.NoAptcaInherit#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.NoAptcaInherit/cs/FxCop.Security.NoAptcaInherit.cs#1)]

## <a name="example"></a>例
 前の説明で示されている2番目のアセンブリは完全に信頼され、部分的に信頼された `T1` 呼び出し元を許可します。

 [!code-csharp[FxCop.Security.YesAptcaInherit#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.YesAptcaInherit/cs/FxCop.Security.YesAptcaInherit.cs#1)]

## <a name="example"></a>例
 前の説明で表されたテストの種類 `X` は、部分的に信頼されたアセンブリにあります。

 [!code-csharp[FxCop.Security.TestAptcaInherit#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.TestAptcaInherit/cs/FxCop.Security.TestAptcaInherit.cs#1)]

 この例を実行すると、次の出力が生成されます。

 **いかがわしい glen 2/22/2003 12:00:00 AM** 
 での対応**テストから: 晴れ meadow** 
**晴れの meadow 2/22/2003 12:00:00 AM での対応**
## <a name="related-rules"></a>関連規則
 [CA2116:APTCA メソッドは APTCA メソッドのみを呼び出すことができます](../code-quality/ca2116-aptca-methods-should-only-call-aptca-methods.md)

## <a name="see-also"></a>参照
 部分的に信頼されたコード[継承要求](https://msdn.microsoft.com/28b9adbb-8f08-4f10-b856-dbf59eb932d9)[からライブラリを使用して](https://msdn.microsoft.com/library/dd66cd4c-b087-415f-9c3e-94e3a1835f74) [、部分的に信頼されたコードによって呼び出すことができる](https://msdn.microsoft.com/a417fcd4-d3ca-4884-a308-3a1a080eac8d)[安全なコーディングのガイドライン](https://msdn.microsoft.com/library/4f882d94-262b-4494-b0a6-ba9ba1f5f177).NET Framework
