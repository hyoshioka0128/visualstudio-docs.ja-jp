---
title: 'CA1810: 参照型の静的フィールドをインラインで初期化します |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- InitializeReferenceTypeStaticFieldsInline
- CA1810
helpviewer_keywords:
- InitializeReferenceTypeStaticFieldsInline
- CA1810
ms.assetid: e9693118-a914-4efb-9550-ec659d8d97d2
caps.latest.revision: 23
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: c4ad2f4db9290430bb8a378bd264078370ca7b66
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85543833"
---
# <a name="ca1810-initialize-reference-type-static-fields-inline"></a>CA1810:参照型の静的フィールドをインラインで初期化します
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|InitializeReferenceTypeStaticFieldsInline|
|CheckId|CA1810|
|カテゴリ|Microsoft. パフォーマンス|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因
 参照型は、明示的な静的コンストラクターを宣言します。

## <a name="rule-description"></a>ルールの説明
 型で明示的な静的コンストラクターを宣言すると、Just-In-Time (JIT) コンパイラが、静的コンストラクターが呼び出されたことを確認するために、型の静的メソッドと静的インスタンス コンストラクターに個別にチェックを追加します。 静的初期化は、静的メンバーにアクセスするか、型のインスタンスが作成されるときにトリガーされます。 ただし、静的な初期化は、型の変数を宣言しても使用しない場合にはトリガーされません。これは、初期化がグローバル状態を変更した場合に重要になる可能性があります。

 すべての静的データがインラインで初期化され、明示的な静的コンストラクターが宣言されていない場合、Microsoft 中間言語 (MSIL) コンパイラは、 `beforefieldinit` 静的データを初期化するフラグと暗黙的な静的コンストラクターを msil 型定義に追加します。 JIT コンパイラがフラグを検出すると、 `beforefieldinit` ほとんどの場合、静的コンストラクターチェックは追加されません。 静的フィールドにアクセスする前に、静的メソッドまたはインスタンスコンストラクターが呼び出される前に静的初期化が行われることは保証されていません。 静的な初期化は、型の変数が宣言された後でいつでも発生する可能性があることに注意してください。

 静的コンストラクターのチェックによってパフォーマンスが低下することがあります。 静的コンストラクターは、静的フィールドの初期化にのみ使用されることがよくあります。その場合は、静的フィールドに最初にアクセスする前に静的初期化が行われるようにする必要があります。 `beforefieldinit`動作は、これらおよびその他のほとんどの型に適しています。 これは、静的な初期化がグローバル状態に影響し、次のいずれかに該当する場合にのみ不適切です。

- グローバルな状態への影響は高価であり、型が使用されていない場合は必要ありません。

- グローバル状態の効果には、型の静的フィールドにアクセスせずにアクセスできます。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、静的データが宣言されたとき、および静的コンストラクターを削除するときに、静的データをすべて初期化します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 パフォーマンスが問題にならない場合は、このルールの警告を抑制しても安全です。または、静的な初期化によって発生するグローバル状態の変更がコストがかかる場合や、型の静的メソッドが呼び出される前に発生することを保証する必要がある場合、または型のインスタンスが作成される場合は、。

## <a name="example"></a>例
 次の例は、規則に違反する型 () を示しています。この型は、 `StaticConstructor` `NoStaticConstructor` 規則に適合するように静的コンストラクターをインライン初期化で置き換えます。

 [!code-csharp[FxCop.Performance.RefTypeStaticCtor#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Performance.RefTypeStaticCtor/cs/FxCop.Performance.RefTypeStaticCtor.cs#1)]
 [!code-vb[FxCop.Performance.RefTypeStaticCtor#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Performance.RefTypeStaticCtor/vb/FxCop.Performance.RefTypeStaticCtor.vb#1)]

 `beforefieldinit`クラスの MSIL 定義にフラグが追加されていることに注意して `NoStaticConstructor` ください。

 **. class パブリック自動 ansi staticconstructor**は、 **[mscorlib] system.object を拡張**します。クラス staticconstructor クラスを拡張します。 
 **{** 
 **} // end of class StaticConstructor** 
 **クラス public auto ansi beforefieldinit nostaticconstructor**は、 **[mscorlib] system.object の system.object** 
 **{** 
 **}//end クラスの nostaticconstructor を**拡張します。
## <a name="related-rules"></a>関連規則
 [CA2207:値型のスタティック フィールドのインラインを初期化します](../code-quality/ca2207-initialize-value-type-static-fields-inline.md)
