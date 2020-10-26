---
title: 'CA1800: 不必要にキャストしません |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1800
- DoNotCastUnnecessarily
helpviewer_keywords:
- DoNotCastUnnecessarily
- CA1800
ms.assetid: b79a010a-6627-421e-8955-6007e32fa808
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 757d66ef719b3a1f39a9164dfd50ce1fcf8799db
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85547798"
---
# <a name="ca1800-do-not-cast-unnecessarily"></a>CA1800:不必要にキャストしません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|DoNotCastUnnecessarily|
|CheckId|CA1800|
|カテゴリ|Microsoft. パフォーマンス|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因
 メソッドは、その引数の1つまたはローカル変数に対して重複するキャストを実行します。 この規則による完全な分析を行うには、デバッグ情報を使用してテストされたアセンブリをビルドし、関連付けられているプログラムデータベース (.pdb) ファイルを使用できるようにする必要があります。

## <a name="rule-description"></a>ルールの説明
 二重のキャストがあるとパフォーマンスが低下します。特に、小さな繰り返しステートメントでキャストが実行される場合はそうです。 明示的な重複キャスト操作の場合は、キャストの結果をローカル変数に格納し、重複するキャスト操作の代わりにローカル変数を使用します。

 `is`実際のキャストが実行される前にキャストが成功するかどうかをテストするために C# 演算子を使用する場合は、代わりに演算子の結果をテストすることを検討してください `as` 。 これにより、演算子によって実行される暗黙的なキャスト操作を行わずに、同じ機能が提供され `is` ます。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、メソッドの実装を変更して、キャスト操作の数を最小限にします。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 このルールからの警告を抑制することも、パフォーマンスが問題にならない場合は完全に無視することもできます。

## <a name="example"></a>例
 次の例は、C# の演算子を使用して規則に違反するメソッドを示して `is` います。 2番目のメソッドは、演算子を演算子の結果に対してテストに置き換えることによってルールを満たし `is` `as` ます。これにより、反復ごとのキャスト操作の数が2から1に減少します。

 [!code-csharp[FxCop.Performance.UnnecessaryCastsAsIs#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Performance.UnnecessaryCastsAsIs/cs/FxCop.Performance.UnnecessaryCastsAsIs.cs#1)]

## <a name="example"></a>例
 次の例は、複数の `start_Click` 重複した明示的なキャスト (規則に違反する) と、 `reset_Click` ローカル変数にキャストを格納することによって規則を満たすメソッド () を持つメソッドを示しています。

 [!code-csharp[FxCop.Performance.UnnecessaryCasts#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Performance.UnnecessaryCasts/cs/FxCop.Performance.UnnecessaryCasts.cs#1)]
 [!code-vb[FxCop.Performance.UnnecessaryCasts#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Performance.UnnecessaryCasts/vb/FxCop.Performance.UnnecessaryCasts.vb#1)]

## <a name="see-also"></a>参照
 [as](https://msdn.microsoft.com/library/a9be126b-cbf4-4990-a70d-d0e1983cad0e) [is](https://msdn.microsoft.com/library/bc62316a-d41f-4f90-8300-c6f4f0556e43)
