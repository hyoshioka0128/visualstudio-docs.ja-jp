---
title: 'CA1802: 適切な場所にリテラルを使用します。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- UseLiteralsWhereAppropriate
- CA1802
helpviewer_keywords:
- UseLiteralsWhereAppropriate
- CA1802
ms.assetid: 2515e4cd-9e61-486d-b067-58ba1a743ce4
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: dc8019c97d3c561000f1c6a8d083bee6253face3
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544405"
---
# <a name="ca1802-use-literals-where-appropriate"></a>CA1802:適切な場所にリテラルを使用します
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|UseLiteralsWhereAppropriate|
|CheckId|CA1802|
|カテゴリ|Microsoft. パフォーマンス|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因
 フィールドは、および (では) と宣言され `static` `readonly` `Shared` `ReadOnly` [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 、コンパイル時に計算できるという値で初期化されます。

## <a name="rule-description"></a>ルールの説明
 フィールドの値は、 `static``readonly` 宣言する型の静的コンストラクターが呼び出されるときに、実行時に計算されます。 フィールドが `static``readonly` 宣言時に初期化され、静的コンストラクターが明示的に宣言されていない場合、コンパイラは静的コンストラクターを生成してフィールドを初期化します。

 フィールドの値は `const` コンパイル時に計算され、メタデータに格納されます。これにより、フィールドと比較したときの実行時のパフォーマンスが向上し `static``readonly` ます。

 コンパイル時には対象のフィールドに割り当てられた値が計算できるであるため、宣言をフィールドに変更して、実行時では `const` なくコンパイル時に値が計算されるようにします。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、 `static` 修飾子と `readonly` 修飾子を修飾子で置き換え `const` ます。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 このルールからの警告を抑制することも、パフォーマンスが問題にならない場合はルールを無効にすることも安全です。

## <a name="example"></a>例
 次の例は、規則に違反する型と、規則に適合する型 () を示して `UseReadOnly` `UseConstant` います。

 [!code-csharp[FxCop.Performance.UseLiterals#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Performance.UseLiterals/cs/FxCop.Performance.UseLiterals.cs#1)]
 [!code-vb[FxCop.Performance.UseLiterals#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Performance.UseLiterals/vb/FxCop.Performance.UseLiterals.vb#1)]
