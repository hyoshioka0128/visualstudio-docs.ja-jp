---
title: 注釈を適用するタイミングと場所の指定
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- _Group_
- _At_
- _When_
- _At_buffer_
ms.assetid: 8e4f4f9c-5dfa-4835-87df-ecd1698fc650
author: corob-msft
ms.author: corob
manager: markl
ms.workload:
- multiple
ms.openlocfilehash: f6efcc158ea0b5b2e44a5b9d0750bc897e442994
ms.sourcegitcommit: 68f893f6e472df46f323db34a13a7034dccad25a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/15/2020
ms.locfileid: "77271838"
---
# <a name="specifying-when-and-where-an-annotation-applies"></a>注釈を適用するタイミングと場所の指定
注釈が条件付きの場合は、アナライザーに注釈を指定するために他の注釈が必要になることがあります。  たとえば、関数に同期または非同期の変数が含まれている場合、関数は次のように動作します。同期ケースでは、最終的には成功しますが、非同期の場合は、直ちに成功できない場合はエラーが報告されます。 関数が同期的に呼び出された場合、結果値を確認しても、返されなかったため、コードアナライザーに値は提供されません。  ただし、関数が非同期に呼び出され、関数の結果が確認されない場合は、重大なエラーが発生する可能性があります。 この例では、この記事の後半で説明する `_When_` 注釈を使用してチェックを有効にする状況を示します。

## <a name="structural-annotations"></a>構造的な注釈
注釈を適用するタイミングと場所を制御するには、次の構造注釈を使用します。

|Annotation|説明|
|----------------|-----------------|
|`_At_(expr, anno-list)`|`expr` は、左辺値を生成する式です。 `anno-list` 内の注釈は、`expr`によって指定されたオブジェクトに適用されます。 `anno-list`の各注釈に対して、注釈が事後条件で解釈される場合、`expr` は事前条件で解釈されます。注釈が事後条件で解釈される場合は、事後条件で解釈されます。|
|`_At_buffer_(expr, iter, elem-count, anno-list)`|`expr` は、左辺値を生成する式です。 `anno-list` 内の注釈は、`expr`によって指定されたオブジェクトに適用されます。 `anno-list`の各注釈に対して、注釈が事後条件で解釈される場合、`expr` は事前条件として解釈されます。注釈が事後条件で解釈される場合は、事後条件で解釈されます。<br /><br /> `iter` は、注釈 (`anno-list`を含む) にスコープが設定されている変数の名前です。 `iter` には `long`暗黙の型があります。 外側のスコープ内の同じ名前の変数は、評価からは見えません。<br /><br /> `elem-count` は、整数に評価される式です。|
|`_Group_(anno-list)`|`anno-list` 内の注釈はすべて、各注釈に適用されるグループ注釈に適用される修飾子を持っていると見なされます。|
|`_When_(expr, anno-list)`|`expr` は `bool`に変換できる式です。 0以外 (`true`) の場合、`anno-list` で指定された注釈は適用可能と見なされます。<br /><br /> 既定では、`anno-list`の各注釈に対して、`expr` は注釈が事前条件である場合は入力値を使用し、注釈が事後条件の場合は出力値を使用して解釈されます。 既定値をオーバーライドするには、入力値を使用する必要があることを示す事後条件を評価するときに、組み込み `_Old_` を使用できます。 **注:** `_When_` を使用した結果として、さまざまな注釈が有効になっている場合があります。これは、事前条件での `expr` の評価結果が、事後条件で評価された結果と異なる `*pLength`場合があるためです。|

## <a name="see-also"></a>参照

- [SAL 注釈を使って C/C++ のコード障害を減らす方法](../code-quality/using-sal-annotations-to-reduce-c-cpp-code-defects.md)
- [SAL について](../code-quality/understanding-sal.md)
- [関数パラメーターおよび戻り値の注釈設定](../code-quality/annotating-function-parameters-and-return-values.md)
- [関数の動作に注釈を付ける](../code-quality/annotating-function-behavior.md)
- [構造体とクラスに注釈を付ける](../code-quality/annotating-structs-and-classes.md)
- [ロック動作に注釈を付ける](../code-quality/annotating-locking-behavior.md)
- [組み込み関数](../code-quality/intrinsic-functions.md)
- [ベスト プラクティスと例](../code-quality/best-practices-and-examples-sal.md)
