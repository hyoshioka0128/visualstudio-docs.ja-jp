---
title: 関数の動作に注釈を付ける |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
f1_keywords:
- _On_failure_
- _Return_type_success_
- _Always_
- _Maybe_raises_SEH_exception_
- _Raises_SEH_exception_
- _Called_from_function_class_
- _Function_class_
- _Must_inspect_result_
- _Success_
- _Check_return_
- _Use_decl_annotations_
ms.assetid: c0aa268d-6fa3-4ced-a8c6-f7652b152e61
caps.latest.revision: 13
author: corob-msft
ms.author: corob
manager: jillfra
ms.openlocfilehash: 7ebda5933f73e2511932f8968104327a56ee7606
ms.sourcegitcommit: 68f893f6e472df46f323db34a13a7034dccad25a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/15/2020
ms.locfileid: "77277871"
---
# <a name="annotating-function-behavior"></a>関数の動作に注釈を付ける
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[関数のパラメーターと戻り値](../code-quality/annotating-function-parameters-and-return-values.md)に注釈を付けるだけでなく、関数全体のプロパティに注釈を設定することもできます。  
  
## <a name="function-annotations"></a>関数の注釈  
 次の注釈は、関数全体に適用され、どのように動作するか、またはどのように動作するかを説明します。  
  
|Annotation|説明|  
|----------------|-----------------|  
|`_Called_from_function_class_(name)`|スタンドアロン専用ではありません。代わりに、`_When_` 注釈と共に使用する述語です。 詳細については、「[注釈を適用するタイミングと場所の指定](../code-quality/specifying-when-and-where-an-annotation-applies.md)」を参照してください。<br /><br /> `name` パラメーターは任意の文字列であり、一部の関数の宣言で `_Function_class_` 注釈にも含まれます。  現在分析されている関数に、同じ値の `name`を持つ `_Function_class_` を使用して注釈が付けられている場合、`_Called_from_function_class_` は0以外の値を返します。それ以外の場合は0を返します。|  
|`_Check_return_`|戻り値に注釈を指定し、呼び出し元がそれを検査する必要があることを示します。 関数が void コンテキストで呼び出された場合、チェッカーはエラーを報告します。|  
|`_Function_class_(name)`|`name` パラメーターは、ユーザーが指定する任意の文字列です。  これは、他の名前空間とは異なる名前空間に存在します。 関数、関数ポインター、または-最も便利な関数ポインター型は、1つまたは複数の関数クラスに属しているものとして指定できます。|  
|`_Raises_SEH_exception_`|常に構造化例外ハンドラー (SEH) 例外を発生させる関数に対して、`_When_` と `_On_failure_` 条件に従って注釈をします。 詳細については、「[注釈を適用するタイミングと場所の指定](../code-quality/specifying-when-and-where-an-annotation-applies.md)」を参照してください。|  
|`_Maybe_raises_SEH_exception_`|必要に応じて、`_When_` および `_On_failure_` 条件に従って SEH 例外を発生させる可能性がある関数に注釈を適用します。|  
|`_Must_inspect_result_`|戻り値、パラメーター、および globals を含む、すべての出力値に注釈を指定します。  アナライザーは、注釈付きオブジェクトの値がその後検査されない場合にエラーを報告します。 "検査" は、条件式で使用されるか、出力パラメーターまたはグローバルに割り当てられるか、またはパラメーターとして渡されるかを示します。  戻り値の場合、`_Must_inspect_result_` は `_Check_return_`を意味します。|  
|`_Use_decl_annotations_`|は、ヘッダー内の注釈のリストの代わりに、関数定義 (関数本体とも呼ばれます) で使用できます。  `_Use_decl_annotations_` を使用すると、同じ関数のスコープ内ヘッダーに表示される注釈は、`_Use_decl_annotations_` 注釈を持つ定義にも存在するかのように使用されます。|  
  
## <a name="successfailure-annotations"></a>成功または失敗の注釈  
 関数が失敗する場合があります。関数が成功すると、結果が不完全になるか、結果と異なる可能性があります。  次の一覧の注釈は、エラーの動作を表現する方法を示しています。  これらの注釈を使用するには、成功したかどうかを判断するために有効にする必要があります。したがって、`_Success_` 注釈が必要です。  `NTSTATUS` と `HRESULT` には既に `_Success_` 注釈が組み込まれていることに注意してください。ただし、`NTSTATUS` または `HRESULT`に独自の `_Success_` 注釈を指定すると、組み込みの注釈がオーバーライドされます。  
  
|Annotation|説明|  
|----------------|-----------------|  
|`_Always_(anno_list)`|`anno_list _On_failure_(anno_list)`と同じです。つまり、関数が成功したかどうかにかかわらず、`anno_list` 内の注釈が適用されます。|  
|`_On_failure_(anno_list)`|`_Success_` が、明示的に、または typedef で `_Return_type_success_` によって暗黙的にまたは暗黙的に関数に注釈を付けるためにも使用される場合にのみ使用されます。 `_On_failure_` 注釈が関数パラメーターまたは戻り値に存在する場合、`anno_list` (キリスト) の各注釈は `_When_(!expr, anno)`としてコード化されているかのように動作します。 `expr` は、必須の `_Success_` 注釈のパラメーターです。 これは、すべての事後条件に対する `_Success_` の暗黙のアプリケーションが `_On_failure_`に適用されないことを意味します。|  
|`_Return_type_success_(expr)`|Typedef に適用できます。 この型を返し、明示的に `_Success_` を持たないすべての関数に `_Success_(expr)`があるかのように注釈が付けられていることを示します。 `_Return_type_success_` は、関数または関数ポインター typedef では使用できません。|  
|`_Success_(expr)`|`expr` は、右辺値を生成する式です。 関数宣言または定義に `_Success_` 注釈が存在する場合、関数および事後条件の各注釈 (`anno`) は、`_When_(expr, anno)`としてコード化されているかのように動作します。 `_Success_` 注釈は、パラメーターや戻り値の型ではなく、関数でのみ使用できます。 関数には最大で1つの `_Success_` 注釈を指定できますが、`_When_`、`_At_`、または `_Group_`には指定できません。 詳細については、「[注釈を適用するタイミングと場所の指定](../code-quality/specifying-when-and-where-an-annotation-applies.md)」を参照してください。|  
  
## <a name="see-also"></a>参照  
 [SAL 注釈を使用して CC++ /コードの欠陥を減らす](../code-quality/using-sal-annotations-to-reduce-c-cpp-code-defects.md)   
 [SAL](../code-quality/understanding-sal.md)  について  
 [関数のパラメーターと戻り値に注釈を付ける](../code-quality/annotating-function-parameters-and-return-values.md)   
 [構造体とクラスに注釈を付ける](../code-quality/annotating-structs-and-classes.md)   
 [ロック動作に注釈を付ける](../code-quality/annotating-locking-behavior.md)   
 [注釈を適用するタイミングと場所を指定](../code-quality/specifying-when-and-where-an-annotation-applies.md)する   
 [組み込み関数](../code-quality/intrinsic-functions.md)   
 [ベスト プラクティスと例](../code-quality/best-practices-and-examples-sal.md)
