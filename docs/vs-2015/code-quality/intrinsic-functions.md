---
title: 組み込み関数 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
f1_keywords:
- _String_length_
- _Param_
- _Curr_
- _Old_
- _Nullterm_length_
- _Inexpressible_
ms.assetid: adf29f8c-89fd-4a5e-9804-35ac83e1c457
caps.latest.revision: 9
author: corob-msft
ms.author: corob
manager: jillfra
ms.openlocfilehash: a0a6cd31cbc8cf73cfa2c7e9ee7c096fa56799b9
ms.sourcegitcommit: 68f893f6e472df46f323db34a13a7034dccad25a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/15/2020
ms.locfileid: "77277965"
---
# <a name="intrinsic-functions"></a>組み込み関数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

SAL 内の式は、C/C++式にすることができます。これは、副作用のない式であることを示します。たとえば、+ +、--,、関数の呼び出しすべてにこのコンテキストでの副作用があります。  ただし、SAL には、関数に似たオブジェクトや、SAL 式で使用できる予約済みのシンボルがいくつか用意されています。 これらは*組み込み関数*と呼ばれます。  
  
## <a name="general-purpose"></a>General Purpose  
 次のているか関数注釈は、SAL の一般的なユーティリティを提供します。  
  
|Annotation|Description|  
|----------------|-----------------|  
|`_Curr_`|現在注釈が付けられているオブジェクトのシノニム。  `_At_` 注釈が使用されている場合、`_Curr_` は `_At_`の最初のパラメーターと同じです。  それ以外の場合は、パラメーター、または注釈が構文的に関連付けられている関数/戻り値全体を指定します。|  
|`_Inexpressible_(expr)`|入力データセットをスキャンして選択したメンバーをカウントすることによって計算された場合など、注釈式を使用して、バッファーのサイズが複雑すぎて表すことができない状況を表します。|  
|`_Nullterm_length_(param)`|`param` は、バッファー内の要素の数 (null 終端文字は含まれません)。 非集計の非 void 型の任意のバッファーに適用できます。|  
|`_Old_(expr)`|前提条件で評価された場合、`_Old_` は `expr`入力値を返します。  事後条件で評価されると、前提条件で評価されたように `expr` 値が返されます。|  
|`_Param_(n)`|関数に対する `n`th パラメーターは、1から `n`までカウントし、`n` はリテラル整数定数です。 パラメーターにという名前が付けられている場合、この注釈は名前によってパラメーターにアクセスするのと同じです。 **注:** `n` は、省略記号で定義された位置指定パラメーターを参照することも、名前が使用されない関数プロトタイプで使用することもできます。|  
|`return`|関数の戻りC++値を示すために、C/予約済みキーワード `return` を SAL 式で使用できます。  この値は post 状態でのみ使用できます。これは、事前状態で使用するための構文エラーです。|  
  
## <a name="string-specific"></a>文字列固有  
 次の組み込み関数注釈を使用すると、文字列を操作できます。 これらの4つの関数は、null 終端文字の前に見つかった型の要素の数を返すために、同じ目的を果たします。 違いは、参照される要素のデータの種類です。 文字で構成されていない null で終わるバッファーの長さを指定する場合は、前のセクションの `_Nullterm_length_(param)` 注釈を使用します。  
  
|Annotation|Description|  
|----------------|-----------------|  
|`_String_length_(param)`|`param` は、null 終端文字を含まない、文字列内の要素の数です。 この注釈は、文字型の文字列用に予約されています。|  
|`strlen(param)`|`param` は、null 終端文字を含まない、文字列内の要素の数です。 この注釈は、文字配列で使用するために予約されており、C ランタイム関数[strlen ()](https://msdn.microsoft.com/library/16462f2a-1e0f-4eb3-be55-bf1c83f374c2)に似ています。|  
|`wcslen(param)`|`param` は、null 終端文字までの文字列内の要素の数です (ただし、含まれません)。 この注釈は、ワイド文字配列で使用するために予約されており、C ランタイム関数[wcslen ()](https://msdn.microsoft.com/library/16462f2a-1e0f-4eb3-be55-bf1c83f374c2)に似ています。|  
  
## <a name="see-also"></a>参照  
 [SAL 注釈を使用して CC++ /コードの欠陥を減らす](../code-quality/using-sal-annotations-to-reduce-c-cpp-code-defects.md)   
 [SAL](../code-quality/understanding-sal.md)  について  
 [関数のパラメーターと戻り値に注釈を付ける](../code-quality/annotating-function-parameters-and-return-values.md)   
 [関数の動作に注釈を付ける](../code-quality/annotating-function-behavior.md)   
 [構造体とクラスに注釈を付ける](../code-quality/annotating-structs-and-classes.md)   
 [ロック動作に注釈を付ける](../code-quality/annotating-locking-behavior.md)   
 [注釈を適用するタイミングと場所を指定](../code-quality/specifying-when-and-where-an-annotation-applies.md)する   
 [ベスト プラクティスと例](../code-quality/best-practices-and-examples-sal.md)
