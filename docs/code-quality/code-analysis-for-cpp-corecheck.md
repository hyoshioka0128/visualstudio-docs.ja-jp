---
title: C++ Core ガイドライン チェッカーの参照
ms.date: 03/22/2018
ms.topic: reference
helpviewer_keywords:
- code analysis, C++ core check
ms.assetid: f1429463-136e-41ed-8a75-a8dbf0b4fd89
author: corob-msft
ms.author: corob
manager: markl
ms.workload:
- cplusplus
ms.openlocfilehash: 2c3e1ba77f3f78de3fc1fac4185121ecb42b1b5b
ms.sourcegitcommit: 68f893f6e472df46f323db34a13a7034dccad25a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/15/2020
ms.locfileid: "77271384"
---
# <a name="c-core-guidelines-checker-reference"></a>C++ Core ガイドライン チェッカーの参照

このセクションでは、C++ Core ガイドライン チェッカーの警告を一覧表示します。 コード分析の詳細については、「 [/analyze (コード分析)](/cpp/build/reference/analyze-code-analysis) 」および「[クイックスタート:C++C/のコード分析](../code-quality/quick-start-code-analysis-for-c-cpp.md)」を参照してください。

> [!NOTE]
> いくつかの警告が 1 つ以上のグループに属しているし、すべての警告の完全なリファレンス トピックがあります。

## <a name="owner_pointer-group"></a>OWNER_POINTER Group

[C26402 DONT_HEAP_ALLOCATE_MOVABLE_RESULT](C26402.md)移動コンストラクターがある場合は、ヒープに割り当てられたオブジェクトではなく、スコープを持つオブジェクトを返します。 「 [ C++コアガイドライン R. 3](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-ptr)」を参照してください。

[C26403 RESET_OR_DELETE_OWNER](C26403.md)所有者\<T > ポインター '% variable% ' をリセットするか、明示的に削除してください。 「 [ C++コアガイドライン R. 3](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-ptr)」を参照してください。

[C26404 DONT_DELETE_INVALID](C26404.md)> 無効な状態にある可能性のある所有者\<T を削除しないでください。 「 [ C++コアガイドライン R. 3](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-ptr)」を参照してください。

[C26405 DONT_ASSIGN_TO_VALID](C26405.md)有効な状態にある可能性のある >\<T には割り当てないでください。 「 [ C++コアガイドライン R. 3](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-ptr)」を参照してください。

[C26406 DONT_ASSIGN_RAW_TO_OWNER](C26406.md)所有者\<T > に生のポインターを割り当てないでください。 「 [ C++コアガイドライン R. 3](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-ptr)」を参照してください。

[C26407 DONT_HEAP_ALLOCATE_UNNECESSARILY](C26407.md)スコープオブジェクトを優先します。不要なヒープ割り当ては行わないでください。 「 [ C++コアガイドライン r. 5](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-scoped)」を参照してください。

[C26429 USE_NOTNULL](C26429.md)シンボル '% symbol% ' は null 性がテストされていないため、not_null としてマークできます。 「 [ C++ Core ガイドライン (F. 23](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#f23-use-a-not_nullt-to-indicate-that-null-is-not-a-valid-value))」を参照してください。

[C26430 TEST_ON_ALL_PATHS](C26430.md)シンボル '% symbol% ' は、すべてのパスで null 性がテストされていません。 「 [ C++ Core ガイドライン (F. 23](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#f23-use-a-not_nullt-to-indicate-that-null-is-not-a-valid-value))」を参照してください。

[C26431 DONT_TEST_NOTNULL](C26431.md)式 '% expr% ' の型は既に gsl:: not_null です。 Null 性はテストしないでください。 「 [ C++ Core ガイドライン (F. 23](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#f23-use-a-not_nullt-to-indicate-that-null-is-not-a-valid-value))」を参照してください。

## <a name="raw_pointer-group"></a>RAW_POINTER グループ

[C26400 NO_RAW_POINTER_ASSIGNMENT](c26400.md)所有者\<T > 戻り値を持つ関数呼び出しの結果を、生のポインターに割り当てないでください。代わりに、owner\<T > を使用してください。 「 [ C++コアガイドライン I. 11](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Ri-raw)」を参照してください。

[C26401 DONT_DELETE_NON_OWNER](c26401.md)\<T > の所有者ではない生のポインターは削除しないでください。 「 [ C++コアガイドライン I. 11](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Ri-raw)」を参照してください。

[C26402 DONT_HEAP_ALLOCATE_MOVABLE_RESULT](C26402.md)  Return a scoped object instead of a heap-allocated if it has a move constructor. 「 [ C++コアガイドライン R. 3](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-ptr)」を参照してください。

[C26408 NO_MALLOC_FREE](C26408.md)Malloc () と free () を使用しないでください。 nothrow バージョンの new を delete と共に使用してください。 「 [ C++コアガイドライン (R. 10](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-mallocfree))」を参照してください。

[C26409 NO_NEW_DELETE](C26409.md)New と delete を明示的に呼び出すことは避け、代わりに std:: make_unique\<T > を使用してください。 「 [ C++コアガイドライン (R. 11](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-newdelete))」を参照してください。

[C26429 USE_NOTNULL](C26429.md)シンボル '% symbol% ' は null 性がテストされていないため、not_null としてマークできます。 「 [ C++ Core ガイドライン (F. 23](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#f23-use-a-not_nullt-to-indicate-that-null-is-not-a-valid-value))」を参照してください。

[C26430 TEST_ON_ALL_PATHS](C26430.md)シンボル '% symbol% ' は、すべてのパスで null 性がテストされていません。 「 [ C++ Core ガイドライン (F. 23](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#f23-use-a-not_nullt-to-indicate-that-null-is-not-a-valid-value))」を参照してください。

[C26431 DONT_TEST_NOTNULL](C26431.md)式 '% expr% ' の型は既に gsl:: not_null です。 Null 性はテストしないでください。 「 [ C++ Core ガイドライン (F. 23](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#f23-use-a-not_nullt-to-indicate-that-null-is-not-a-valid-value))」を参照してください。

[C26481 NO_POINTER_ARITHMETIC](C26481.md)ポインター演算は使用しないでください。 代わりに span を使用します。 「 [ C++コアガイドラインの境界](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#SS-bounds)」を参照してください。 1.

[C26485 NO_ARRAY_TO_POINTER_DECAY](C26485.md)。
式 'expr %': 配列ポインターへの減退からなし。 「 [ C++コアガイドラインの境界](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#SS-bounds)」を参照してください。 3.

## <a name="unique_pointer-group"></a>UNIQUE_POINTER Group

[C26410 NO_REF_TO_CONST_UNIQUE_PTR](C26410.md)パラメーター '% parameter% ' は `const` 一意のポインターへの参照です。代わりに const T * または const T & を使用してください。 「 [ C++コアガイドライン R. 32](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-uniqueptrparam).」を参照してください。

[C26411 NO_REF_TO_UNIQUE_PTR](C26411.md)パラメーター '% parameter% ' は一意のポインターへの参照であり、再割り当てもリセットも行われません。代わりに T * または T & を使用してください。 「 [ C++コアガイドライン R. 33](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-reseat)」を参照してください。

[C26414 RESET_LOCAL_SMART_PTR](C26414.md)ローカルスマートポインター '% symbol% ' を移動、コピー、再割り当て、またはリセットします。 「 [ C++コアガイドライン r. 5](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-scoped)」を参照してください。

[C26415 SMART_PTR_NOT_NEEDED](C26415.md)スマートポインターパラメーター '% symbol% ' は、含まれているポインターにアクセスするためにのみ使用されます。 T * または T を使用すると、代わりにします。 「 [ C++コアガイドライン r. 30](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-smartptrparam)」を参照してください。

## <a name="shared_pointer-group"></a>SHARED_POINTER グループ

[C26414 RESET_LOCAL_SMART_PTR](C26414.md)ローカルスマートポインター '% symbol% ' を移動、コピー、再割り当て、またはリセットします。 「 [ C++コアガイドライン r. 5](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-scoped)」を参照してください。

[C26415 SMART_PTR_NOT_NEEDED](C26415.md)スマートポインターパラメーター '% symbol% ' は、含まれているポインターにアクセスするためにのみ使用されます。 T * または T を使用すると、代わりにします。 「 [ C++コアガイドライン r. 30](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-smartptrparam)」を参照してください。

[C26416 NO_RVALUE_REF_SHARED_PTR](C26416.md)共有ポインターパラメーター '% symbol% ' は右辺値参照によって渡されます。 代わりに、値によって渡します。 「 [ C++ Core のガイドライン](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-sharedptrparam-owner)」を参照してください。

[C26417 NO_LVALUE_REF_SHARED_PTR](C26417.md)共有ポインターパラメーター '% symbol% ' は参照によって渡されているため、リセットまたは再割り当てされません。 T * または T を使用すると、代わりにします。 「 [ C++コアガイドライン R. 35](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-sharedptrparam)」を参照してください。

[C26418 NO_VALUE_OR_CONST_REF_SHARED_PTR](C26418.md)共有ポインターパラメーター '% symbol% ' は、コピーまたは移動されません。 T * または T を使用すると、代わりにします。 「 [ C++コアガイドライン R. 36](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-sharedptrparam-const)」を参照してください。

## <a name="declaration-group"></a>宣言のグループ

[C26426 NO_GLOBAL_INIT_CALLS](C26426.md)グローバル初期化子は、constexpr でない関数 '% symbol% ' を呼び出します。 「 [ C++コアガイドライン (22](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#i22-avoid-complex-initialization-of-global-objects))」を参照してください。

[C26427 NO_GLOBAL_INIT_EXTERNS](C26427.md)グローバル初期化子が extern オブジェクト '% symbol% ' にアクセスします。 「 [ C++コアガイドライン (22](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#i22-avoid-complex-initialization-of-global-objects))」を参照してください。

[C26444 NO_UNNAMED_RAII_OBJECTS](c26444.md)カスタムの構築および破棄によって名前のないオブジェクトを使用しないようにします。 「 [ES: いいえ (try)」を参照してください。名前のないローカル変数を宣言して](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md)ください。

## <a name="class-group"></a>クラスのグループ

[C26432 DEFINE_OR_DELETE_SPECIAL_OPS](C26432.md)型 '% symbol% ' の既定の操作を定義または削除する場合は、すべてを定義するか削除します。 「 [ C++コアガイドライン c.](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#c21-if-you-define-or-delete-any-default-operation-define-or-delete-them-all)」を参照してください。

[C26433 OVERRIDE_EXPLICITLY](c26433.md)関数 '% symbol% ' は ' override ' でマークされなければなりません。 「 [C. 128: 仮想関数では、仮想、オーバーライド、または最終」を厳密に1つ指定する必要があり](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#c128-virtual-functions-should-specify-exactly-one-of-virtual-override-or-final)ます。

[C26434 DONT_HIDE_METHODS](C26434.md)関数 '% symbol_1% ' は、非仮想関数 '% symbol_2% ' を非表示にします。 「 [ C++コアガイドライン c.](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#c128-virtual-functions-should-specify-exactly-one-of-virtual-override-or-final)」を参照してください。

[C26435 SINGLE_VIRTUAL_SPECIFICATION](c26435.md)関数 '% symbol% ' では、' virtual '、' override '、または ' final ' のいずれか1つだけを指定しなければなりません。 「 [C. 128: 仮想関数では、仮想、オーバーライド、または最終」を厳密に1つ指定する必要があり](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md)ます。

[C26436 NEED_VIRTUAL_DTOR](C26436.md)仮想関数を持つ型 '% symbol% ' には、パブリック仮想デストラクターかプロテクト非仮想デストラクターが必要です。 「 [ C++コアガイドライン c. 35](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#c35-a-base-class-destructor-should-be-either-public-and-virtual-or-protected-and-nonvirtual)」を参照してください。

[C26443 NO_EXPLICIT_DTOR_OVERRIDE](c26443.md)オーバーライドするデストラクターでは、明示的な ' override ' または ' virtual ' 指定子は使用できません。 「 [C. 128: 仮想関数では、仮想、オーバーライド、または最終」を厳密に1つ指定する必要があり](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md)ます。

## <a name="type-group"></a>種類のグループ

[C26437 DONT_SLICE](C26437.md)スライスしないでください。 「 [ C++ Core のガイドライン](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#es63-dont-slice)」を参照してください。

## <a name="style-group"></a>スタイルのグループ

[C26438 NO_GOTO](C26438.md)`goto`は避けてください。 [ C++ 76 の主要ガイドライン](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#es76-avoid-goto)を参照してください。

## <a name="function-group"></a>関数グループ

[C26439 SPECIAL_NOEXCEPT](C26439.md)この種の関数は、をスローしない場合があります。 `noexcept`を宣言します。 「 [ C++コアガイドライン (f.](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#f6-if-your-function-may-not-throw-declare-it-noexcept))」を参照してください。

[C26440 DECLARE_NOEXCEPT](C26440.md)関数 '% symbol% ' は `noexcept`として宣言できます。 「 [ C++コアガイドライン (f.](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#f6-if-your-function-may-not-throw-declare-it-noexcept))」を参照してください。

[C26447 DONT_THROW_IN_NOEXCEPT](c26447.md)関数は**noexcept**として宣言されていますが、例外をスローする可能性がある関数を呼び出しています。
コアガイドラインを参照してください[ C++ 。 F. 6: 関数がスローされない場合は、それを noexcept と宣言](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#f6-if-your-function-may-not-throw-declare-it-noexcept)します。

## <a name="concurrency-group"></a>同時実行のグループ

[C26441 NO_UNNAMED_GUARDS](C26441.md)ガードオブジェクトの名前はにする必要があります。 「 [ C++コアガイドライン cp. 44](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#cp44-remember-to-name-your-lock_guards-and-unique_locks)」を参照してください。

## <a name="const-group"></a>CONST グループ

[C26460 USE_CONST_REFERENCE_ARGUMENTS](c26460.md)関数 '% function% ' の参照引数 '% argument% ' を `const`としてマークできます。 「 [ C++コアガイドライン con. 3](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rconst-ref)」を参照してください。

[C26461 USE_CONST_POINTER_ARGUMENTS](c26461.md): 関数 '% function% ' のポインター引数 '% argument% ' は、`const`へのポインターとしてマークできます。 「 [ C++コアガイドライン con. 3](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rconst-ref)」を参照してください。

[C26462 USE_CONST_POINTER_FOR_VARIABLE](c26462.md)'% Variable% ' によってポイントされている値が1回だけ割り当てられています。 `const`へのポインターとしてマークしてください。 「 [ C++コアガイドライン con 4](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#con4-use-const-to-define-objects-with-values-that-do-not-change-after-construction)」を参照してください。

[C26463 USE_CONST_FOR_ELEMENTS](c26463.md)配列 '% array% ' の要素が1回だけ割り当てられています。マーク要素 `const`。 「 [ C++コアガイドライン con 4](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#con4-use-const-to-define-objects-with-values-that-do-not-change-after-construction)」を参照してください。

[C26464 USE_CONST_POINTER_FOR_ELEMENTS](c26464.md)配列 '% array% ' の要素によってポイントされている値は、1回だけ割り当てられます。要素を `const`へのポインターとしてマークしてください。 「 [ C++コアガイドライン con 4](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#con4-use-const-to-define-objects-with-values-that-do-not-change-after-construction)」を参照してください。

[C26496 USE_CONST_FOR_VARIABLE](c26496.md)変数 '% variable% ' が1回だけ割り当てられています。 `const`としてマークしてください。 「 [ C++コアガイドライン con 4](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#con4-use-const-to-define-objects-with-values-that-do-not-change-after-construction)」を参照してください。

[C26497 USE_CONSTEXPR_FOR_FUNCTION](c26497.md)コンパイル時の評価が必要な場合は、この関数% function% を `constexpr` としてマークできます。 「 [ C++コアガイドライン f. 4](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rf-constexpr)」を参照してください。

[C26498 USE_CONSTEXPR_FOR_FUNCTIONCALL](c26498.md)コンパイル時の評価が必要な場合は、この関数呼び出し% function% で `constexpr` を使用できます。 「 [ C++コアガイドライン con 5](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rconst-constexpr)」を参照してください。

## <a name="type-group"></a>種類のグループ

[C26465 NO_CONST_CAST_UNNECESSARY](c26465.md)`const_cast` を使用して `const`を離すことは避けてください。 `const_cast` は必要ありません。この変換では、変動性または揮発性が削除されていません。 「 [ C++コアガイドラインの種類 3](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Pro-type-constcast)」を参照してください。

[C26466 NO_STATIC_DOWNCAST_POLYMORPHIC](c26466.md)`static_cast` downcasts は使用しないでください。 ポリモーフィックな型からキャストでは、dynamic_cast を使用する必要があります。 「 [ C++コアガイドラインの種類」を](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Pro-type-downcast)参照してください。 2.

[C26471 NO_REINTERPRET_CAST_FROM_VOID_PTR](c26471.md)`reinterpret_cast`は使用しないでください。 Void * からのキャストでは、`static_cast`を使用できます。 「 [ C++コアガイドラインの種類」を](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Pro-type-reinterpretcast)参照してください。 1.

[C26472 NO_CASTS_FOR_ARITHMETIC_CONVERSION](C26472.md)算術変換には `static_cast` を使用しないでください。 使用中かっこの初期化、gsl:、またはします。 「 [ C++コアガイドラインの種類」を](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Pro-type-reinterpretcast)参照してください。 1.

[C26473 NO_IDENTITY_CAST](C26473.md)変換元の型と変換先の型が同じであるポインター型間ではキャストしないでください。 「 [ C++コアガイドラインの種類」を](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Pro-type-reinterpretcast)参照してください。 1.

[C26474 NO_IMPLICIT_CAST](C26474.md)変換が暗黙的である可能性がある場合は、ポインター型の間でキャストしないでください。 「 [ C++コアガイドラインの種類」を](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Pro-type-reinterpretcast)参照してください。 1.

[C26475 NO_FUNCTION_STYLE_CASTS](C26475.md)関数スタイルの C キャストは使用しないでください。 [ C++コアガイドライン 49](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#es49-if-you-must-use-a-cast-use-a-named-cast)を参照してください。

[C26490 NO_REINTERPRET_CAST](c26490.md)`reinterpret_cast`は使用しないでください。 「 [ C++コアガイドラインの種類」を](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#SS-type)参照してください。 1.

[C26491 NO_STATIC_DOWNCAST](c26490.md)`static_cast` downcasts は使用しないでください。 「 [ C++コアガイドラインの種類」を](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#SS-type)参照してください。 2.

[C26492 NO_CONST_CAST](c26492.md)`const_cast` を使用して `const`を離すことは避けてください。 「 [ C++コアガイドラインの種類 3](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#SS-type)」を参照してください。

[C26493 NO_CSTYLE_CAST](c26493.md)C スタイルのキャストは使用しないでください。 「 [ C++コアガイドラインの種類」を](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#SS-type)参照してください。 4.

[C26494 VAR_USE_BEFORE_INIT](c26494.md)変数 '% variable% ' は初期化されていません。 常にオブジェクトを初期化します。 「 [ C++コアガイドラインタイプ 5](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#SS-type)」を参照してください。

[C26495 MEMBER_UNINIT](c26495.md)変数 '% variable% ' は初期化されていません。 常にメンバー変数を初期化します。 「 [ C++コアガイドラインの種類. 6](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#SS-type)」を参照してください。

## <a name="bounds-group"></a>境界グループ

[C26446 USE_GSL_AT](c26446.md)Unchecked 添字演算子の代わりに `gsl::at()` を使用することをお勧めします。 「 [ C++コアガイドライン: 境界. 4: 標準ライブラリの関数と、範囲チェックされていない型を使用しない](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#probounds-bounds-safety-profile)」を参照してください。

[C26481 NO_POINTER_ARITHMETIC](C26481.md)。
ポインターの算術演算を使用しないでください。 代わりに span を使用します。 「 [ C++コアガイドラインの境界」を参照してください。1](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#SS-bounds)

[C26482 NO_DYNAMIC_ARRAY_INDEXING](c26482.md)定数式を使用して配列にインデックスを作成するだけです。 「 [ C++コアガイドラインの境界」を参照してください。2](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#SS-bounds)

[C26483 STATIC_INDEX_OUT_OF_RANGE](c26483.md)値% value% が境界 (0,% bound%) の範囲外です変数 '% variable% ' の。 配列の境界内にある定数式を使用して配列にインデックスのみ。 「 [ C++コアガイドラインの境界」を参照してください。2](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#SS-bounds)

[C26485 NO_ARRAY_TO_POINTER_DECAY](C26485.md)式 '% expr% ': 配列からポインターが減衰されていません。 「 [ C++コアガイドラインの境界」を参照してください。3](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#SS-bounds)

## <a name="gsl-group"></a>GSL グループ

[C26445 NO_SPAN_REF](c26445.md)`gsl::span` または `std::string_view` への参照は、有効期間の問題を示している場合があります。
「 [ C++コアガイドライン gsl. ビュー: ビュー」を参照してください。](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#gslview-views)

[C26446 USE_GSL_AT](c26446.md)Unchecked 添字演算子の代わりに `gsl::at()` を使用することをお勧めします。 「 [ C++コアガイドライン: 境界. 4: 標準ライブラリの関数と、範囲チェックされていない型を使用しない](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#probounds-bounds-safety-profile)」を参照してください。

[C26448 USE_GSL_FINALLY](c26448.md)最後のアクションが意図されている場合は、`gsl::finally` の使用を検討してください。 「 [ C++コアガイドライン: gsl. util: Utilities](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#SS-utilities)」を参照してください。

一時が無効にされている場合、一時から作成された[C26449 NO_SPAN_FROM_TEMPORARY](c26449.md)
`gsl::span` または `std::string_view` は無効になります。 「 [ C++主要なガイドライン: gsl. view: Views](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#gslview-views)」を参照してください。

## <a name="deprecated-warnings"></a>非推奨の警告

次の警告は、core ガイドライン チェッカーの初期の実験的なルール セットに存在し、は非推奨が、無視してかまいません。 警告は、上記のリストからの警告によって置き換えられます。

- 26412 DEREF_INVALID_POINTER
- 26413 DEREF_NULLPTR
- 26420 ASSIGN_NONOWNER_TO_EXPLICIT_OWNER
- 26421 ASSIGN_VALID_OWNER
- 26422 VALID_OWNER_LEAVING_SCOPE
- 26423 ALLOCATION_NOT_ASSIGNED_TO_OWNER
- 26424 VALID_ALLOCATION_LEAVING_SCOPE
- 26425 ASSIGNING_TO_STATIC
- 26499 NO_LIFETIME_TRACKING

## <a name="see-also"></a>参照
[コアガイドラインC++チェッカーの使用](using-the-cpp-core-guidelines-checkers.md)
