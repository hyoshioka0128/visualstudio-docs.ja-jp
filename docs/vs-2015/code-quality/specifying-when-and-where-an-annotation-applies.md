---
title: 注釈を適用するタイミングと場所を指定する |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
f1_keywords:
- _Group_
- _At_
- _When_
- _At_buffer_
ms.assetid: 8e4f4f9c-5dfa-4835-87df-ecd1698fc650
caps.latest.revision: 9
author: corob-msft
ms.author: corob
manager: jillfra
ms.openlocfilehash: 1eb32aa7d87da75ebf37b27aa1d425adb85f8c9b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "77278454"
---
# <a name="specifying-when-and-where-an-annotation-applies"></a>注釈を適用するタイミングと場所の指定
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

注釈が条件付きの場合は、アナライザーに注釈を指定するために他の注釈が必要になることがあります。  たとえば、関数に同期または非同期の変数が含まれている場合、関数は次のように動作します。同期ケースでは、最終的には成功しますが、非同期の場合は、直ちに成功できない場合はエラーが報告されます。 関数が同期的に呼び出された場合、結果値を確認しても、返されなかったため、コードアナライザーに値は提供されません。  ただし、関数が非同期に呼び出され、関数の結果が確認されない場合は、重大なエラーが発生する可能性があります。 この例は、 `_When_` この記事で後述する注釈を使用してチェックを有効にする状況を示しています。  
  
## <a name="structural-annotations"></a>構造的な注釈  
 注釈を適用するタイミングと場所を制御するには、次の構造注釈を使用します。  
  
|注釈|説明|  
|----------------|-----------------|  
|`_At_(expr, anno-list)`|`expr` 左辺値を生成する式です。 の注釈は、 `anno-list` によって名前が付けられたオブジェクトに適用され `expr` ます。 の各注釈に対して、注釈が事後条件で解釈される `anno-list` `expr` 場合、は事前条件で解釈されます。注釈が事後条件で解釈される場合は、事後条件で解釈されます。|  
|`_At_buffer_(expr, iter, elem-count, anno-list)`|`expr` 左辺値を生成する式です。 の注釈は、 `anno-list` によって名前が付けられたオブジェクトに適用され `expr` ます。 の各注釈に対して、注釈が事後条件で解釈される `anno-list` `expr` 場合、は事前条件で解釈され、注釈が事後条件で解釈される場合は事後条件で解釈されます。<br /><br /> `iter` 注釈をスコープとする変数の名前を指定します (を含む `anno-list` )。 `iter` には暗黙的な型があり `long` ます。 外側のスコープ内の同じ名前の変数は、評価からは見えません。<br /><br /> `elem-count` 整数に評価される式です。|  
|`_Group_(anno-list)`|の注釈 `anno-list` はすべて、各注釈に適用されるグループ注釈に適用される修飾子を持っていると見なされます。|  
|`_When_(expr, anno-list)`|`expr` に変換できる式を指定 `bool` します。 0以外 () の場合、に指定されている `true` 注釈 `anno-list` は適用可能と見なされます。<br /><br /> 既定では、の各注釈に対して `anno-list` 、 `expr` は注釈が事前条件である場合は入力値を使用し、注釈が事後条件の場合は出力値を使用して解釈されます。 既定値をオーバーライドするには、 `_Old_` 事後条件を評価して入力値を使用する必要があることを示す組み込みのを使用できます。 **注:**  を使用した結果として、さまざまな注釈が有効になる場合があり `_When_` ます。これは、変更可能な値 (など) が関係している場合に、 `*pLength` 事前条件で評価された結果が `expr` 事後条件で評価された結果と異なる可能性があるためです。|  
  
## <a name="see-also"></a>参照  
 [SAL 注釈を使用して C/c + + コードの欠陥を減らす](../code-quality/using-sal-annotations-to-reduce-c-cpp-code-defects.md)   
 [SAL について](../code-quality/understanding-sal.md)   
 [関数のパラメーターと戻り値に注釈を付ける](../code-quality/annotating-function-parameters-and-return-values.md)   
 [関数の動作に注釈を付ける](../code-quality/annotating-function-behavior.md)   
 [構造体とクラスに注釈を付ける](../code-quality/annotating-structs-and-classes.md)   
 [ロック動作に注釈を付ける](../code-quality/annotating-locking-behavior.md)   
 [組み込み関数](../code-quality/intrinsic-functions.md)   
 [ベスト プラクティスと例](../code-quality/best-practices-and-examples-sal.md)
