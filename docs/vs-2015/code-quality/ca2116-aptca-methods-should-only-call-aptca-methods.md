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
ms.openlocfilehash: c9de5178b585275ef410ad3179ba320b663536bf
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72658679"
---
# <a name="ca2116-aptca-methods-should-only-call-aptca-methods"></a>CA2116: APTCA メソッドは APTCA メソッドのみを呼び出すことができます
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|AptcaMethodsShouldOnlyCallAptcaMethods|
|CheckId|CA2116|
|カテゴリ|Microsoft.Security|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 <xref:System.Security.AllowPartiallyTrustedCallersAttribute?displayProperty=fullName> 属性を持つアセンブリ内のメソッドは、属性を持たないアセンブリ内のメソッドを呼び出します。

## <a name="rule-description"></a>規則の説明
 既定では、厳密な名前を持つアセンブリ内のパブリックメソッドまたはプロテクトメソッドは、完全信頼の[リンク確認要求](https://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d)によって暗黙的に保護されます。完全に信頼された呼び出し元だけが、厳密な名前付きアセンブリにアクセスできます。 <xref:System.Security.AllowPartiallyTrustedCallersAttribute> (APTCA) 属性でマークされた厳密な名前付きアセンブリには、この保護はありません。 属性は、リンク確認要求を無効にし、イントラネットまたはインターネットからコードを実行するなど、完全に信頼されていない呼び出し元がアセンブリにアクセスできるようにします。

 APTCA 属性が完全に信頼されたアセンブリに存在し、部分的に信頼された呼び出し元を許可しない別のアセンブリのコードをアセンブリが実行すると、セキュリティ上の脆弱性が発生する可能性があります。 `M1` と `M2` の2つのメソッドが次の条件を満たす場合、悪意のある呼び出し元は `M1` メソッドを使用して、`M2`を保護する暗黙の完全信頼リンク要求を回避できます。

- `M1` は、APTCA 属性を持つ、完全に信頼されたアセンブリで宣言されたパブリックメソッドです。

- `M1` は `M1`のアセンブリの外部で `M2` メソッドを呼び出します。

- `M2`のアセンブリには APTCA 属性がないため、部分的に信頼されている呼び出し元の代わりにまたはによって実行することはできません。

  部分的に信頼された呼び出し元 `X` は、メソッド `M1`を呼び出して、`M1` に `M2`を呼び出すことができます。 `M2` には APTCA 属性がないため、直接の呼び出し元 (`M1`) は完全信頼のリンク確認要求を満たす必要があります。`M1` は完全に信頼されているため、このチェックを満たしています。 セキュリティ上のリスクは、信頼されていない呼び出し元からの `M2` を保護するリンク確認要求の満たさに `X` が関与しないためです。 そのため、APTCA 属性を持つメソッドは、属性を持たないメソッドを呼び出すことはできません。

## <a name="how-to-fix-violations"></a>違反の修正方法
 APCTA 属性が必要な場合は、要求を使用して、完全信頼アセンブリを呼び出すメソッドを保護します。 必要なアクセス許可は、メソッドによって公開される機能によって異なります。 可能であれば、完全信頼の要求によってメソッドを保護し、基になる機能が部分的に信頼された呼び出し元に公開されないようにします。 これが不可能な場合は、公開されている機能を効果的に保護するアクセス許可のセットを選択します。 要求の詳細については、「[要求](https://msdn.microsoft.com/e5283e28-2366-4519-b27d-ef5c1ddc1f48)」を参照してください。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則からの警告を安全に抑制するには、メソッドによって公開されている機能が、破壊的な方法で使用できる機密情報、操作、またはリソースに直接または間接的にアクセスすることを、呼び出し元に許可しないようにする必要があります。

## <a name="example"></a>例
 次の例では、2つのアセンブリとテストアプリケーションを使用して、この規則によって検出されたセキュリティの脆弱性を示しています。 最初のアセンブリには APTCA 属性がなく、部分的に信頼された呼び出し元 (前のトピックでは `M2` によって表されます) からアクセスできないようにする必要があります。

 [!code-csharp[FxCop.Security.NoAptca#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.NoAptca/cs/FxCop.Security.NoAptca.cs#1)]

## <a name="example"></a>例
 2番目のアセンブリは完全に信頼されており、部分的に信頼された呼び出し元を許可します (前の説明の `M1` で表されます)。

 [!code-csharp[FxCop.Security.YesAptca#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.YesAptca/cs/FxCop.Security.YesAptca.cs#1)]

## <a name="example"></a>例
 テストアプリケーション (前の説明の `X` で表されます) は部分的に信頼されています。

 [!code-csharp[FxCop.Security.TestAptcaMethods#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.TestAptcaMethods/cs/FxCop.Security.TestAptcaMethods.cs#1)]

 この例を実行すると、次の出力が生成されます。

 **完全信頼の要求: 要求が失敗しました。** 
**ClassRequiringFullTrust が呼び出されました。**
## <a name="related-rules"></a>関連規則
 [CA2117: APTCA 型は APTCA 基本型のみを拡張することができます](../code-quality/ca2117-aptca-types-should-only-extend-aptca-base-types.md)

## <a name="see-also"></a>関連項目
 部分的に信頼され[たコード](https://msdn.microsoft.com/e5283e28-2366-4519-b27d-ef5c1ddc1f48)[からのライブラリを使用して](https://msdn.microsoft.com/library/dd66cd4c-b087-415f-9c3e-94e3a1835f74)部分的に信頼されたコード[によって呼び出すこと](https://msdn.microsoft.com/a417fcd4-d3ca-4884-a308-3a1a080eac8d)ができる[安全なコーディングのガイドライン](https://msdn.microsoft.com/library/4f882d94-262b-4494-b0a6-ba9ba1f5f177).NET Framework リンク確認[要求](https://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d)の[データとモデリング](https://msdn.microsoft.com/library/8c37635d-e2c1-4b64-a258-61d9e87405e6)
