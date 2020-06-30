---
title: 'CA2119: プライベートインターフェイスを満たすメソッドをシールします。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- SealMethodsThatSatisfyPrivateInterfaces
- CA2119
helpviewer_keywords:
- CA2119
- SealMethodsThatSatisfyPrivateInterfaces
ms.assetid: 483d02e1-cfaf-4754-a98f-4116df0f3509
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 0afa6950a6ad876cdcfdcc1a56dd143422b9d44f
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544353"
---
# <a name="ca2119-seal-methods-that-satisfy-private-interfaces"></a>CA2119:プライベート インターフェイスを満たすメソッドをシールします
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|SealMethodsThatSatisfyPrivateInterfaces|
|CheckId|CA2119|
|カテゴリ|Microsoft.Security|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 継承可能なパブリック型は、(Visual Basic) インターフェイスのオーバーライド可能なメソッドの実装を提供 `internal` `Friend` します。

## <a name="rule-description"></a>ルールの説明
 インターフェイスメソッドはパブリックアクセシビリティを持っていますが、これは実装する型では変更できません。 内部インターフェイスは、インターフェイスを定義するアセンブリの外部で実装するためのものではないコントラクトを作成します。 (Visual Basic) 修飾子を使用して内部インターフェイスのメソッドを実装するパブリック型では、 `virtual` `Overridable` アセンブリ外部の派生型によってメソッドをオーバーライドできます。 定義アセンブリの2番目の型がメソッドを呼び出し、内部専用のコントラクトを要求した場合、外部アセンブリのオーバーライドされたメソッドが実行されると、動作が損なわれる可能性があります。 これにより、セキュリティの脆弱性が生じます。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、次のいずれかを使用して、メソッドがアセンブリの外部でオーバーライドされないようにします。

- 宣言する型を `sealed` ( `NotInheritable` Visual Basic) に設定します。

- 宣言する型のアクセシビリティを `internal` (Visual Basic) に変更し `Friend` ます。

- 宣言する型からすべてのパブリックコンストラクターを削除します。

- 修飾子を使用せずにメソッドを実装し `virtual` ます。

- メソッドを明示的に実装します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 慎重に確認した後に、メソッドがアセンブリの外部でオーバーライドされた場合に悪用される可能性があるセキュリティ上の問題が存在しない場合は、この規則による警告を抑制することが安全です。

## <a name="example"></a>例
 次の例は、この規則に違反する型を示して `BaseImplementation` います。

 [!code-cpp[FxCop.Security.SealMethods1#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Security.SealMethods1/cpp/FxCop.Security.SealMethods1.cpp#1)]
 [!code-csharp[FxCop.Security.SealMethods1#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.SealMethods1/cs/FxCop.Security.SealMethods1.cs#1)]
 [!code-vb[FxCop.Security.SealMethods1#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Security.SealMethods1/vb/FxCop.Security.SealMethods1.vb#1)]

## <a name="example"></a>例
 次の例では、前の例の仮想メソッドの実装を悪用しています。

 [!code-cpp[FxCop.Security.SealMethods2#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Security.SealMethods2/cpp/FxCop.Security.SealMethods2.cpp#1)]
 [!code-csharp[FxCop.Security.SealMethods2#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.SealMethods2/cs/FxCop.Security.SealMethods2.cs#1)]
 [!code-vb[FxCop.Security.SealMethods2#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Security.SealMethods2/vb/FxCop.Security.SealMethods2.vb#1)]

## <a name="see-also"></a>関連項目
 [インターフェイス](https://msdn.microsoft.com/library/2feda177-ce11-432d-81b4-d50f5f35fd37)[インターフェイス](https://msdn.microsoft.com/library/61b06674-12c9-430b-be68-cc67ecee1f5b)
