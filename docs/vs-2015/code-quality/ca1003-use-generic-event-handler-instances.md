---
title: 'CA1003: 汎用イベントハンドラーのインスタンスを使用します。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- UseGenericEventHandlerInstances
- CA1003
helpviewer_keywords:
- CA1003
- UseGenericEventHandlerInstances
ms.assetid: 402101b6-555d-4cf7-b223-1d9fdfaaf1cd
caps.latest.revision: 24
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: ee0571e85a1d4ec9960e0235814fcb9d7adbd483
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85539907"
---
# <a name="ca1003-use-generic-event-handler-instances"></a>CA1003:汎用イベント ハンドラーのインスタンスを使用します
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|アイテム|値|
|-|-|
|TypeName|UseGenericEventHandlerInstances|
|CheckId|CA1003|
|カテゴリ|Microsoft Design|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 型には、void を返すデリゲートが含まれています。このシグネチャには、2つのパラメーター (最初のオブジェクト、もう1つは EventArgs に割り当て可能な型)、および格納しているアセンブリターゲットが含まれてい [!INCLUDE[dnprdnlong](../includes/dnprdnlong-md.md)] ます。

## <a name="rule-description"></a>ルールの説明
 より前 [!INCLUDE[dnprdnlong](../includes/dnprdnlong-md.md)] では、カスタム情報をイベントハンドラーに渡すために、クラスから派生したクラスを指定した新しいデリゲートを宣言する必要がありました <xref:System.EventArgs?displayProperty=fullName> 。 これは、デリゲートを導入したではなくなりまし [!INCLUDE[dnprdnlong](../includes/dnprdnlong-md.md)] た <xref:System.EventHandler%601?displayProperty=fullName> 。 この汎用デリゲートを使用すると、から派生した任意のクラス <xref:System.EventArgs> をイベントハンドラーと共に使用できます。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、デリゲートを削除し、デリゲートを使用してデリゲートを置き換え <xref:System.EventHandler%601?displayProperty=fullName> ます。 デリゲートがコンパイラによって自動生成される場合は [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 、デリゲートを使用するようにイベント宣言の構文を変更し <xref:System.EventHandler%601?displayProperty=fullName> ます。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。

## <a name="example"></a>例
 次の例は、規則に違反するデリゲートを示しています。 この例では、 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] コメントを使用して、ルールを満たす例を変更する方法を説明しています。 C# の例では、変更されたコードを表示する例を次に示します。

 [!code-csharp[FxCop.Design.CustomEventHandler#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.CustomEventHandler/cs/FxCop.Design.CustomEventHandler.cs#1)]
 [!code-vb[FxCop.Design.CustomEventHandler#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.CustomEventHandler/vb/FxCop.Design.CustomEventHandler.vb#1)]

## <a name="example"></a>例
 次の例では、規則を満たす前の例からデリゲート宣言を削除し、デリゲートを使用して、メソッドとメソッドでの使用を置き換え `ClassThatRaisesEvent` `ClassThatHandlesEvent` <xref:System.EventHandler%601?displayProperty=fullName> ます。

 [!code-csharp[FxCop.Design.GenericEventHandler#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.GenericEventHandler/cs/FxCop.Design.GenericEventHandler.cs#1)]

## <a name="related-rules"></a>関連規則
 [CA1005:ジェネリック型でパラメーターを使用しすぎないでください](../code-quality/ca1005-avoid-excessive-parameters-on-generic-types.md)

 [CA1010:コレクションは、ジェネリック インターフェイスを実装しなければなりません](../code-quality/ca1010-collections-should-implement-generic-interface.md)

 [CA1000:ジェネリック型の静的メンバーを宣言しません](../code-quality/ca1000-do-not-declare-static-members-on-generic-types.md)

 [CA1002:ジェネリック リストを公開しません](../code-quality/ca1002-do-not-expose-generic-lists.md)

 [CA1006:ジェネリック型をメンバー シグネチャ内で入れ子にしません](../code-quality/ca1006-do-not-nest-generic-types-in-member-signatures.md)

 [CA1004:ジェネリック メソッドは型パラメーターを指定しなければなりません](../code-quality/ca1004-generic-methods-should-provide-type-parameter.md)

 [CA1007:適切な場所にジェネリックを使用します](../code-quality/ca1007-use-generics-where-appropriate.md)

## <a name="see-also"></a>関連項目
 [ジェネリック](https://msdn.microsoft.com/library/75ea8509-a4ea-4e7a-a2b3-cf72482e9282)
