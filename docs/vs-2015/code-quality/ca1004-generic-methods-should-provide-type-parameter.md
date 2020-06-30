---
title: 'CA1004: ジェネリックメソッドは型パラメーター | を指定する必要がありますMicrosoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1004
- GenericMethodsShouldProvideTypeParameter
helpviewer_keywords:
- GenericMethodsShouldProvideTypeParameter
- CA1004
ms.assetid: 38755f6a-fb45-4bf2-932e-0354ad826499
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: e7a96c95313ffee82448e3485c90868c8103814a
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85539803"
---
# <a name="ca1004-generic-methods-should-provide-type-parameter"></a>CA1004:ジェネリック メソッドは型パラメーターを指定しなければなりません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|GenericMethodsShouldProvideTypeParameter|
|CheckId|CA1004|
|カテゴリ|Microsoft Design|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 外部から参照できるジェネリックメソッドのパラメーターシグネチャに、メソッドのすべての型パラメーターに対応する型が含まれていません。

## <a name="rule-description"></a>ルールの説明
 型引数を明示的に指定するのではなく、メソッドに渡す引数の型によってジェネリック メソッドの型引数を決定する方法が推論されます。 推論を有効にするには、ジェネリック メソッドのパラメーター シグネチャに、そのメソッドの型パラメーターと同じ型のパラメーターが含まれている必要があります。 この場合、型引数を指定する必要がなくなります。 すべての型パラメーターに対して推論を使用する場合、ジェネリックおよび非ジェネリックインスタンスメソッドを呼び出すための構文は同じです。 これにより、ジェネリックメソッドの使いやすさが簡単になります。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、パラメーターシグネチャにメソッドの型パラメーターごとに同じ型が含まれるようにデザインを変更します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。 簡単に理解して使用できる構文でジェネリックを提供することで、新しいライブラリの導入率を習得し、向上させるために必要な時間を短縮できます。

## <a name="example"></a>例
 次の例は、2つのジェネリックメソッドを呼び出すための構文を示しています。 の型引数 `InferredTypeArgument` は推論され、の型引数は `NotInferredTypeArgument` 明示的に指定する必要があります。

 [!code-csharp[FxCop.Design.Inference#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.Inference/cs/FxCop.Design.Inference.cs#1)]
 [!code-vb[FxCop.Design.Inference#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.Inference/vb/FxCop.Design.Inference.vb#1)]

## <a name="related-rules"></a>関連規則
 [CA1005:ジェネリック型でパラメーターを使用しすぎないでください](../code-quality/ca1005-avoid-excessive-parameters-on-generic-types.md)

 [CA1010:コレクションは、ジェネリック インターフェイスを実装しなければなりません](../code-quality/ca1010-collections-should-implement-generic-interface.md)

 [CA1000:ジェネリック型の静的メンバーを宣言しません](../code-quality/ca1000-do-not-declare-static-members-on-generic-types.md)

 [CA1002:ジェネリック リストを公開しません](../code-quality/ca1002-do-not-expose-generic-lists.md)

 [CA1006:ジェネリック型をメンバー シグネチャ内で入れ子にしません](../code-quality/ca1006-do-not-nest-generic-types-in-member-signatures.md)

 [CA1003:汎用イベント ハンドラーのインスタンスを使用します](../code-quality/ca1003-use-generic-event-handler-instances.md)

 [CA1007:適切な場所にジェネリックを使用します](../code-quality/ca1007-use-generics-where-appropriate.md)