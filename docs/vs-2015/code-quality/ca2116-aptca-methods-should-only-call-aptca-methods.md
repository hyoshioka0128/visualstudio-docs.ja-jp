---
title: 'CA2116: APTCA メソッドは APTCA メソッドのみを呼び出すことができます。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- AptcaMethodsShouldOnlyCallAptcaMethods
- CA2116
helpviewer_keywords:
- AptcaMethodsShouldOnlyCallAptcaMethods
- CA2116
ms.assetid: 8b91637e-891f-4dde-857b-bf8012270ec4
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 115c0e733716994ba463eada938f8ff908612d0f
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547759"
---
# <a name="ca2116-aptca-methods-should-only-call-aptca-methods"></a>CA2116:APTCA メソッドは APTCA メソッドのみを呼び出すことができます
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|AptcaMethodsShouldOnlyCallAptcaMethods|
|CheckId|CA2116|
|カテゴリ|Microsoft.Security|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 属性を持つアセンブリ内のメソッドが、 <xref:System.Security.AllowPartiallyTrustedCallersAttribute?displayProperty=fullName> 属性を持たないアセンブリ内のメソッドを呼び出しています。

## <a name="rule-description"></a>ルールの説明
 既定では、厳密な名前を持つアセンブリ内のパブリックメソッドまたはプロテクトメソッドは、完全信頼の[リンク確認要求](https://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d)によって暗黙的に保護されます。完全に信頼された呼び出し元だけが、厳密な名前付きアセンブリにアクセスできます。 (APTCA) 属性でマークされた厳密な名前付きのアセンブリには、 <xref:System.Security.AllowPartiallyTrustedCallersAttribute> この保護はありません。 属性は、リンク確認要求を無効にし、イントラネットまたはインターネットからコードを実行するなど、完全に信頼されていない呼び出し元がアセンブリにアクセスできるようにします。

 APTCA 属性が完全に信頼されたアセンブリに存在し、部分的に信頼された呼び出し元を許可しない別のアセンブリのコードをアセンブリが実行すると、セキュリティ上の脆弱性が発生する可能性があります。 2つのメソッドが `M1` `M2` あり、次の条件を満たす場合、悪意のある呼び出し元はメソッドを使用して、 `M1` を保護する暗黙的な完全信頼リンク要求をバイパスできます `M2` 。

- `M1`は、APTCA 属性を持つ、完全に信頼されたアセンブリで宣言されたパブリックメソッドです。

- `M1``M2`のアセンブリの外部でメソッドを呼び出し `M1` ます。

- `M2`のアセンブリには APTCA 属性が含まれていないため、部分的に信頼されている呼び出し元の代わりにまたはによって実行することはできません。

  部分的に信頼された呼び出し元は `X` メソッドを呼び出して `M1` 、 `M1` を呼び出すことができ `M2` ます。 に `M2` は APTCA 属性がないため、その直前の呼び出し元 ( `M1` ) は完全な信頼のためのリンク確認要求を満たす必要があります。 `M1` 完全な信頼があるため、このチェックが満たされます。 セキュリティ上のリスクは、信頼されていない `X` 呼び出し元から保護されるリンク確認要求に、が関与しないためです `M2` 。 そのため、APTCA 属性を持つメソッドは、属性を持たないメソッドを呼び出すことはできません。

## <a name="how-to-fix-violations"></a>違反の修正方法
 APCTA 属性が必要な場合は、要求を使用して、完全信頼アセンブリを呼び出すメソッドを保護します。 必要なアクセス許可は、メソッドによって公開される機能によって異なります。 可能であれば、完全信頼の要求によってメソッドを保護し、基になる機能が部分的に信頼された呼び出し元に公開されないようにします。 これが不可能な場合は、公開されている機能を効果的に保護するアクセス許可のセットを選択します。 要求の詳細については、「[要求](https://msdn.microsoft.com/e5283e28-2366-4519-b27d-ef5c1ddc1f48)」を参照してください。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則からの警告を安全に抑制するには、メソッドによって公開されている機能が、破壊的な方法で使用できる機密情報、操作、またはリソースに直接または間接的にアクセスすることを、呼び出し元に許可しないようにする必要があります。

## <a name="example"></a>例
 次の例では、2つのアセンブリとテストアプリケーションを使用して、この規則によって検出されたセキュリティの脆弱性を示しています。 最初のアセンブリには APTCA 属性がなく、部分的に信頼された呼び出し元 (前の説明ではによって表されます) からアクセスできないようにする必要があり `M2` ます。

 [!code-csharp[FxCop.Security.NoAptca#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.NoAptca/cs/FxCop.Security.NoAptca.cs#1)]

## <a name="example"></a>例
 2番目のアセンブリは完全に信頼されており、部分的に信頼された呼び出し元を許可します (前の説明ではに示されて `M1` います)。

 [!code-csharp[FxCop.Security.YesAptca#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.YesAptca/cs/FxCop.Security.YesAptca.cs#1)]

## <a name="example"></a>例
 (前の説明ので示されている) テストアプリケーション `X` は、部分的に信頼されています。

 [!code-csharp[FxCop.Security.TestAptcaMethods#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.TestAptcaMethods/cs/FxCop.Security.TestAptcaMethods.cs#1)]

 この例を実行すると、次の出力が生成されます。

 **完全信頼の要求: 要求が失敗しました。** 
**ClassRequiringFullTrust が呼び出されました。**
## <a name="related-rules"></a>関連規則
 [CA2117:APTCA 型は APTCA 基本型のみを拡張することができます](../code-quality/ca2117-aptca-types-should-only-extend-aptca-base-types.md)

## <a name="see-also"></a>関連項目
 部分的に信頼され[たコード](https://msdn.microsoft.com/e5283e28-2366-4519-b27d-ef5c1ddc1f48)[からのライブラリを使用して](https://msdn.microsoft.com/library/dd66cd4c-b087-415f-9c3e-94e3a1835f74)部分的に信頼されたコード[によって呼び出すこと](https://msdn.microsoft.com/a417fcd4-d3ca-4884-a308-3a1a080eac8d)ができる[安全なコーディングのガイドライン](https://msdn.microsoft.com/library/4f882d94-262b-4494-b0a6-ba9ba1f5f177).NET Framework リンク確認[要求](https://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d)の[データとモデリング](https://msdn.microsoft.com/library/8c37635d-e2c1-4b64-a258-61d9e87405e6)
