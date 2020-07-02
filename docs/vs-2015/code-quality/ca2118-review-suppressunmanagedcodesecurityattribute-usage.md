---
title: 'CA2118: SuppressUnmanagedCodeSecurityAttribute usage | を確認します。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2118
- ReviewSuppressUnmanagedCodeSecurityUsage
helpviewer_keywords:
- ReviewSuppressUnmanagedCodeSecurityUsage
- CA2118
ms.assetid: 4cb8d2fc-4e44-4dc3-9b74-7f5838827d41
caps.latest.revision: 22
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: bc0e88265245d795697d32a9e6a95909c0415259
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85538659"
---
# <a name="ca2118-review-suppressunmanagedcodesecurityattribute-usage"></a>CA2118:SuppressUnmanagedCodeSecurityAttribute の使用法を確認してください
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|アイテム|値|
|-|-|
|TypeName|ReviewSuppressUnmanagedCodeSecurityUsage|
|CheckId|CA2118|
|カテゴリ|Microsoft.Security|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 パブリックまたはプロテクトの型またはメンバーには、属性があり <xref:System.Security.SuppressUnmanagedCodeSecurityAttribute?displayProperty=fullName> ます。

## <a name="rule-description"></a>ルールの説明
 <xref:System.Security.SuppressUnmanagedCodeSecurityAttribute>COM 相互運用機能またはプラットフォーム呼び出しを使用してアンマネージコードを実行するメンバーの、セキュリティシステムの既定の動作を変更します。 一般に、システムは、アンマネージコードのアクセス許可の[データとモデリング](https://msdn.microsoft.com/library/8c37635d-e2c1-4b64-a258-61d9e87405e6)を行います。 この要求は、メンバーが呼び出されるたびに実行時に発生し、呼び出し履歴内のすべての呼び出し元に対してアクセス許可があるかどうかをチェックします。 属性が存在する場合、システムはアクセス許可の[リンク確認要求](https://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d)を行います。呼び出し元が JIT でコンパイルされると、直接の呼び出し元のアクセス許可がチェックされます。

 この属性は、主にパフォーマンスを向上するために使用されますが、パフォーマンスが向上するとセキュリティ上のリスクも高くなります。 ネイティブメソッドを呼び出すパブリックメンバーに属性を配置した場合、呼び出し履歴 (直前の呼び出し元を除く) 内の呼び出し元は、アンマネージコードを実行するためのアンマネージコードのアクセス許可を必要としません。 パブリックメンバーのアクションと入力処理によっては、信頼できない呼び出し元が、信頼できるコードに通常制限されている機能にアクセスする可能性があります。

 は、 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 呼び出し元が現在のプロセスのアドレス空間に直接アクセスできないようにするために、セキュリティチェックに依存しています。 この属性は通常のセキュリティをバイパスするため、プロセスのメモリの読み取りや書き込みに使用できる場合は、コードに重大な脅威が生じます。 リスクは、意図的にプロセスメモリへのアクセスを提供するメソッドに限定されないことに注意してください。また、この情報は、悪意のあるコードが何らかの方法でアクセスできるようなシナリオにも存在します。たとえば、驚くべき、形式が正しくない、または無効な入力を提供します。

 既定のセキュリティポリシーでは、アセンブリがローカルコンピューターから実行されているか、次のいずれかのグループのメンバーでない限り、アンマネージコードのアクセス許可がアセンブリに付与されません。

- マイコンピューターゾーンコードグループ

- Microsoft 厳密な名前のコードグループ

- ECMA 厳密名コードグループ

## <a name="how-to-fix-violations"></a>違反の修正方法
 コードを慎重に確認し、この属性が絶対に必要であることを確認します。 マネージコードセキュリティについてよく知らない場合、またはこの属性を使用した場合のセキュリティへの影響を理解していない場合は、コードから削除します。 属性が必要な場合は、呼び出し元が悪意のあるコードを使用できないようにする必要があります。 コードにアンマネージコードを実行するためのアクセス許可がない場合、この属性は無効であり、削除する必要があります。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則からの警告を安全に抑制するには、コードからネイティブの操作または破壊的な方法で使用できるリソースへのアクセスが提供されていないことを確認する必要があります。

## <a name="example"></a>例
 次の例は、規則に違反しています。

 [!code-csharp[FxCop.Security.TypesDoNotSuppress#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.TypesDoNotSuppress/cs/FxCop.Security.TypesDoNotSuppress.cs#1)]

## <a name="example"></a>例
 次の例では、メソッドによって、 `DoWork` プラットフォーム呼び出しメソッドへのパブリックにアクセスできるコードパスが提供され `FormatHardDisk` ます。

 [!code-csharp[FxCop.Security.PInvokeAndSuppress#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.PInvokeAndSuppress/cs/FxCop.Security.PInvokeAndSuppress.cs#1)]

## <a name="example"></a>例
 次の例では、public メソッドに `DoDangerousThing` よって違反が発生します。 違反を解決するには、をプライベートにする `DoDangerousThing` 必要があります。また、メソッドに示されているように、セキュリティ要求によって保護されたパブリックメソッドを使用してアクセスする必要があり `DoWork` ます。

 [!code-csharp[FxCop.Security.TypeInvokeAndSuppress#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.TypeInvokeAndSuppress/cs/FxCop.Security.TypeInvokeAndSuppress.cs#1)]

## <a name="see-also"></a>関連項目
 <xref:System.Security.SuppressUnmanagedCodeSecurityAttribute?displayProperty=fullName>[安全なコーディングのガイドライン](https://msdn.microsoft.com/library/4f882d94-262b-4494-b0a6-ba9ba1f5f177)[セキュリティの最適化](https://msdn.microsoft.com/cf255069-d85d-4de3-914a-e4625215a7c0)[データとモデリングの](https://msdn.microsoft.com/library/8c37635d-e2c1-4b64-a258-61d9e87405e6)[リンク確認要求](https://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d)
