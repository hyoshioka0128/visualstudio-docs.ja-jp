---
title: 'CA1502: 複雑さが過剰にならないようにする |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- AvoidExcessiveComplexity
- CA1502
helpviewer_keywords:
- CA1502
- AvoidExcessiveComplexity
ms.assetid: d735454b-2f8f-47ce-907d-f7a5a5391221
caps.latest.revision: 32
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 5da2e2bf26bb1894987caa8b748181d952bd7c18
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547837"
---
# <a name="ca1502-avoid-excessive-complexity"></a>CA1502:メソッドの実装を複雑にしすぎないでください
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|アイテム|値|
|-|-|
|TypeName|AvoidExcessiveComplexity|
|CheckId|CA1502|
|カテゴリ|Microsoft の保守容易性|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因
 メソッドには、過剰なサイクロマティック複雑度があります。

## <a name="rule-description"></a>ルールの説明
 *サイクロマティック複雑度*は、メソッドを使用して線形的に独立したパスの数を測定します。これは、条件分岐の数と複雑さによって決まります。 サイクロマティック複雑度が低いのは、一般に、理解、テスト、および保守が容易なメソッドであることを示しています。 サイクロマティック複雑度は、メソッドの制御フローグラフから計算され、次のように指定されます。

 サイクロマティック複雑度 = エッジの数-ノードの数 + 1

 ノードがロジックの分岐点を表し、エッジがノード間の線を表す場合。

 このルールは、サイクロマティック複雑度が25を超える場合に違反を報告します。

 コードメトリックスの詳細については、「[マネージコードの複雑さと保守性の測定](../code-quality/measuring-complexity-and-maintainability-of-managed-code.md)」を参照してください。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、メソッドをリファクタリングして、サイクロマティック複雑度を下げます。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 複雑さを簡単に軽減できず、メソッドを簡単に理解、テスト、保守できる場合は、この規則による警告を抑制することが安全です。 特に、大規模な `switch` ( `Select` の) ステートメントを含むメソッドは、 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 除外の候補です。 開発サイクルの後半でコードベースを安定性するリスク、または以前に出荷されたコードの実行時の動作に予期しない変更を導入するリスクは、コードをリファクタリングすることによる保守容易性の利点を上回る可能性があります。

## <a name="how-cyclomatic-complexity-is-calculated"></a>サイクロマティック複雑度の計算方法
 サイクロマティック複雑度は、次のように1を追加することによって計算されます。

- ブランチの数 (、、 `if` など `while` `do` )

- 内の `case` ステートメントの数`switch`

  次の例は、さまざまなサイクロマティック複雑なメソッドを示しています。

## <a name="example"></a>例
 **サイクロマティック複雑度1**

 [!code-cpp[FxCop.Maintainability.AvoidExcessiveComplexity#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Maintainability.AvoidExcessiveComplexity/cpp/FxCop.Maintainability.AvoidExcessiveComplexity.cpp#1)]
 [!code-csharp[FxCop.Maintainability.AvoidExcessiveComplexity#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Maintainability.AvoidExcessiveComplexity/cs/FxCop.Maintainability.AvoidExcessiveComplexity.cs#1)]
 [!code-vb[FxCop.Maintainability.AvoidExcessiveComplexity#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Maintainability.AvoidExcessiveComplexity/vb/FxCop.Maintainability.AvoidExcessiveComplexity.vb#1)]

## <a name="example"></a>例
 **サイクロマティック複雑度2**

 [!code-cpp[FxCop.Maintainability.AvoidExcessiveComplexity#2](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Maintainability.AvoidExcessiveComplexity/cpp/FxCop.Maintainability.AvoidExcessiveComplexity.cpp#2)]
 [!code-csharp[FxCop.Maintainability.AvoidExcessiveComplexity#2](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Maintainability.AvoidExcessiveComplexity/cs/FxCop.Maintainability.AvoidExcessiveComplexity.cs#2)]
 [!code-vb[FxCop.Maintainability.AvoidExcessiveComplexity#2](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Maintainability.AvoidExcessiveComplexity/vb/FxCop.Maintainability.AvoidExcessiveComplexity.vb#2)]

## <a name="example"></a>例
 **サイクロマティック複雑度3**

 [!code-cpp[FxCop.Maintainability.AvoidExcessiveComplexity#3](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Maintainability.AvoidExcessiveComplexity/cpp/FxCop.Maintainability.AvoidExcessiveComplexity.cpp#3)]
 [!code-csharp[FxCop.Maintainability.AvoidExcessiveComplexity#3](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Maintainability.AvoidExcessiveComplexity/cs/FxCop.Maintainability.AvoidExcessiveComplexity.cs#3)]
 [!code-vb[FxCop.Maintainability.AvoidExcessiveComplexity#3](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Maintainability.AvoidExcessiveComplexity/vb/FxCop.Maintainability.AvoidExcessiveComplexity.vb#3)]

## <a name="example"></a>例
 **サイクロマティック複雑度8**

 [!code-cpp[FxCop.Maintainability.AvoidExcessiveComplexity#4](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Maintainability.AvoidExcessiveComplexity/cpp/FxCop.Maintainability.AvoidExcessiveComplexity.cpp#4)]
 [!code-csharp[FxCop.Maintainability.AvoidExcessiveComplexity#4](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Maintainability.AvoidExcessiveComplexity/cs/FxCop.Maintainability.AvoidExcessiveComplexity.cs#4)]
 [!code-vb[FxCop.Maintainability.AvoidExcessiveComplexity#4](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Maintainability.AvoidExcessiveComplexity/vb/FxCop.Maintainability.AvoidExcessiveComplexity.vb#4)]

## <a name="related-rules"></a>関連規則
 [CA1501:継承を使用しすぎないでください](../code-quality/ca1501-avoid-excessive-inheritance.md)

## <a name="see-also"></a>関連項目
 [マネージド コードの複雑さと保守性の測定](../code-quality/measuring-complexity-and-maintainability-of-managed-code.md)
