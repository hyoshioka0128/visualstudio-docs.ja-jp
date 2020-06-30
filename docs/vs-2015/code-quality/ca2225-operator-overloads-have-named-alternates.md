---
title: 'CA2225: 演算子のオーバーロードには、代替 | という名前が付いています。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- OperatorOverloadsHaveNamedAlternates
- CA2225
helpviewer_keywords:
- OperatorOverloadsHaveNamedAlternates
- CA2225
ms.assetid: af8f7ab1-63ad-4861-afb9-b7a7a2be15e1
caps.latest.revision: 22
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 2dc43e92b92b6f963900057a76dfe88e38a3638f
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545224"
---
# <a name="ca2225-operator-overloads-have-named-alternates"></a>CA2225:演算子オーバーロードには名前付けされた代替が存在します
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|OperatorOverloadsHaveNamedAlternates|
|CheckId|CA2225|
|カテゴリ|Microsoft. 使用方法|
|互換性に影響する変更点|中断なし|

## <a name="cause"></a>原因
 演算子のオーバーロードが検出され、予想される名前の代替メソッドが検出されませんでした。

## <a name="rule-description"></a>ルールの説明
 演算子のオーバーロードでは、型の計算を表すためにシンボルを使用できます。 たとえば、追加のためにプラス記号 (+) をオーバーロードする型には、通常、"Add" という名前の代替メンバーがあります。 名前付き代替メンバーは、演算子と同じ機能へのアクセスを提供し、オーバーロードされた演算子をサポートしない言語でプログラミングする開発者向けに用意されています。

 このルールは、次の表に示す演算子を検証します。

|C#|Visual Basic|C++|代替名|
|---------|------------------|-----------|--------------------|
|+ (バイナリ)|+|+ (バイナリ)|追加|
|+=|+=|+=|追加|
|&|および|&|BitwiseAnd|
|&=|および =|&=|BitwiseAnd|
|&#124;|または|&#124;|BitwiseOr|
|&#124;=|または =|&#124;=|BitwiseOr|
|--|該当なし|--|Decrement|
|/|/|/|除算|
|/=|/=|/=|除算|
|==|=|==|次の値に等しい|
|^|Xor|^|Xor|
|^=|Xor =|^=|Xor|
|>|>|>|比較|
|>=|>=|>=|比較|
|++|該当なし|++|Increment|
|<>|!=|次の値に等しい|
|<<|<<|<<|から左へ|
|<<=|<<=|<<=|から左へ|
|<|<|<|比較|
|<=|<=|\<=|比較|
|&&|該当なし|&&|LogicalAnd|
|&#124;&#124;|該当なし|&#124;&#124;|LogicalOr|
|!|該当なし|!|LogicalNot|
|%|Mod|%|Mod または剰余|
|%=|該当なし|%=|Mod|
|* (バイナリ)|*|*|乗算|
|*=|該当なし|*=|乗算|
|~|Not|~|OnesComplement|
|>>|>>|>>|プロパティながら|
=|該当なし|>>=|プロパティながら|
|-(バイナリ)|-(バイナリ)|-(バイナリ)|減算|
|-=|該当なし|-=|減算|
|true|IsTrue|該当なし|IsTrue (プロパティ)|
| - (単項)   |該当なし|-|Negate|
|+ (単項)|該当なし|+|Plus|
|false|IsFalse|False|IsTrue (プロパティ)|

 選択した言語では、N/A = = をオーバーロードすることはできません。

 また、 `SomeType` およびという名前のメソッドがあるかどうかをチェックすることにより、型 () の暗黙的なキャスト演算子と明示的なキャスト演算子も確認し `ToSomeType` `FromSomeType` ます。

 C# では、二項演算子がオーバーロードされると、対応する代入演算子 (存在する場合) も暗黙的にオーバーロードされます。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、演算子に対して別の方法を実装します。推奨される代替名を使用して名前を指定します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 共有ライブラリを実装している場合は、この規則による警告を抑制しないでください。 アプリケーションは、このルールの警告を無視できます。

## <a name="example"></a>例
 次の例では、この規則に違反する構造体を定義しています。 この例を修正するには、パブリック `Add(int x, int y)` メソッドを構造体に追加します。

 [!code-csharp[FxCop.Usage.OperatorOverloadsHaveNamedAlternates#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.OperatorOverloadsHaveNamedAlternates/cs/FxCop.Usage.OperatorOverloadsHaveNamedAlternates.cs#1)]

## <a name="related-rules"></a>関連規則
 [CA1046:参照型で、演算子 equals をオーバーロードしないでください](../code-quality/ca1046-do-not-overload-operator-equals-on-reference-types.md)

 [CA2226:演算子は対称型オーバーロードを含まなければなりません](../code-quality/ca2226-operators-should-have-symmetrical-overloads.md)

 [CA2224:オーバーロードする演算子 equals で Equals をオーバーライドします](../code-quality/ca2224-override-equals-on-overloading-operator-equals.md)

 [CA2218:オーバーライドする Equals で GetHashCode をオーバーライドします](../code-quality/ca2218-override-gethashcode-on-overriding-equals.md)

 [CA2231:ValueType.Equals のオーバーライドで、演算子 equals をオーバーロードします](../code-quality/ca2231-overload-operator-equals-on-overriding-valuetype-equals.md)
