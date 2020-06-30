---
title: 'CA2107: deny をレビューし、使用のみを許可する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2107
- ReviewDenyAndPermitOnlyUsage
helpviewer_keywords:
- ReviewDenyAndPermitOnlyUsage
- CA2107
ms.assetid: 366f4a56-ae93-4882-81d0-bd0a55ebbc26
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 7f273ea5f58babf7a0c04f6b0758732d43aab7db
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547772"
---
# <a name="ca2107-review-deny-and-permit-only-usage"></a>CA2107:拒否および許可のみの使用を確認します
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|ReviewDenyAndPermitOnlyUsage|
|CheckId|CA2107|
|カテゴリ|Microsoft.Security|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 メソッドには、PermitOnly または Deny セキュリティアクションを指定するセキュリティチェックが含まれています。

## <a name="rule-description"></a>ルールの説明
 [PermitOnly メソッド](https://msdn.microsoft.com/8c7bdb7f-882f-45b7-908c-6cbaa1767649)とセキュリティアクションの使用は、 <xref:System.Security.CodeAccessPermission.Deny%2A?displayProperty=fullName> セキュリティに関する高度な知識を持つユーザーのみが使用する必要があり [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] ます。 コードにこのセキュリティ アクションを使用する場合、セキュリティを再確認する必要があります。

 拒否は、セキュリティ要求に応じて発生するスタックウォークの既定の動作を変更します。 これにより、呼び出し履歴内の呼び出し元の実際のアクセス許可に関係なく、拒否するメソッドの期間中に付与されないアクセス許可を指定できます。 スタックウォークが拒否によってセキュリティ保護されたメソッドを検出し、要求されたアクセス許可が拒否されたアクセス許可に含まれている場合、スタックウォークは失敗します。 PermitOnly では、スタックウォークの既定の動作も変更されます。 これにより、呼び出し元のアクセス許可に関係なく、許可できるアクセス許可のみをコードで指定できます。 スタックウォークが PermitOnly によってセキュリティ保護されたメソッドを検出し、要求されたアクセス許可が PermitOnly によって指定されたアクセス許可に含まれていない場合、スタックウォークは失敗します。

 これらのアクションに依存するコードは、有用性と微妙な動作が制限されているため、セキュリティの脆弱性に対して慎重に評価する必要があります。 以下、具体例に沿って説明します。

- [リンク確認要求](https://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d)は、Deny または PermitOnly の影響を受けません。

- スタックウォークを発生させる要求と同じスタックフレームで Deny または PermitOnly が発生した場合、セキュリティアクションは無効です。

- パスベースのアクセス許可を構築するために使用される値は、通常、複数の方法で指定できます。 パスの1つの形式へのアクセスを拒否しても、すべてのフォームへのアクセスが拒否されるわけではありません。 たとえば、ファイル共有 \\ \ \ \ 共有がネットワークドライブ X: にマップされている場合、共有上のファイルへのアクセスを拒否するには、 \\ \Server\Share\File、X:\File、およびファイルにアクセスするその他のすべてのパスを拒否する必要があります。

- は、 <xref:System.Security.CodeAccessPermission.Assert%2A?displayProperty=fullName> Deny または PermitOnly に到達する前にスタックウォークを終了できます。

- 拒否によって何らかの影響がある場合 (つまり、呼び出し元に拒否によってブロックされるアクセス許可がある場合)、呼び出し元は保護されたリソースに直接アクセスして、拒否を回避することができます。 同様に、呼び出し元に拒否されたアクセス許可がない場合、スタックウォークは拒否されずに失敗します。

## <a name="how-to-fix-violations"></a>違反の修正方法
 これらのセキュリティアクションを使用すると、違反が発生します。 違反を修正するには、これらのセキュリティアクションを使用しないでください。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 セキュリティレビューを完了した後にのみ、この規則からの警告を非表示にします。

## <a name="example"></a>例
 次の例は、Deny のいくつかの制限を示しています。

 次のライブラリには、それらを保護するセキュリティ要求以外の2つのメソッドを持つクラスが含まれています。

 [!code-csharp[FxCop.Security.PermitAndDeny#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.PermitAndDeny/cs/FxCop.Security.PermitAndDeny.cs#1)]

## <a name="example"></a>例
 次のアプリケーションは、保護されたメソッドでの、ライブラリからの拒否の影響を示しています。

 [!code-csharp[FxCop.Security.TestPermitAndDeny#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.TestPermitAndDeny/cs/FxCop.Security.TestPermitAndDeny.cs#1)]

 この例を実行すると、次の出力が生成されます。

 **要求: 呼び出し元の拒否は、アサートされたアクセス許可で要求に影響しません。** 
**Linkdemand: 呼び出し元の Deny は、アサートされたアクセス許可を持つ LinkDemand には影響しません。** 
**Linkdemand: 呼び出し元の拒否は、LinkDemand で保護されたコードには影響しません。** 
**Linkdemand: この拒否は、linkdemand で保護されたコードには影響しません。**
## <a name="see-also"></a>関連項目
 <xref:System.Security.CodeAccessPermission.PermitOnly%2A?displayProperty=fullName> <xref:System.Security.CodeAccessPermission.Assert%2A?displayProperty=fullName>
 <xref:System.Security.CodeAccessPermission.Deny%2A?displayProperty=fullName>
 <xref:System.Security.IStackWalk.PermitOnly%2A?displayProperty=fullName>
 [安全なコーディングのガイドライン](https://msdn.microsoft.com/library/4f882d94-262b-4494-b0a6-ba9ba1f5f177) [PermitOnly メソッドを使用し](https://msdn.microsoft.com/8c7bdb7f-882f-45b7-908c-6cbaa1767649)た[セキュリティチェックのオーバーライド](https://msdn.microsoft.com/4acdeff5-fc05-41bf-8505-7387cdbfca28)
