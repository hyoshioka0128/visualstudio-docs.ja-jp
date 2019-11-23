---
title: C++ Core ガイドライン チェッカーの参照
ms.date: 03/22/2018
ms.topic: reference
helpviewer_keywords:
- code analysis, C++ core check
ms.assetid: f1429463-136e-41ed-8a75-a8dbf0b4fd89
author: mikeblome
ms.author: mblome
manager: markl
ms.workload:
- cplusplus
ms.openlocfilehash: 9a5fe14c1bcb2b375a104a928513134b1789d437
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72745962"
---
# <a name="c-core-guidelines-checker-reference"></a>C++ Core ガイドライン チェッカーの参照

このセクションでは、C++ Core ガイドライン チェッカーの警告を一覧表示します。 コード分析の詳細については、次を参照してください。 [/analyze (コード分析)](/cpp/build/reference/analyze-code-analysis)と[クイック スタート: c/c++ のコード分析](../code-quality/quick-start-code-analysis-for-c-cpp.md)します。

> [!NOTE]
> いくつかの警告が 1 つ以上のグループに属しているし、すべての警告の完全なリファレンス トピックがあります。

## <a name="owner_pointer-group"></a>OWNER_POINTER Group

[C26402 DONT_HEAP_ALLOCATE_MOVABLE_RESULT](C26402.md) Return a scoped object instead of a heap-allocated if it has a move constructor. 参照してください[C++ Core Guidelines R.3](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-ptr)します。

[C26403 RESET_OR_DELETE_OWNER](C26403.md)リセット owner を明示的に削除または\<T > ポインターが '% 変数 %' です。 参照してください[C++ Core Guidelines R.3](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-ptr)します。

[C26404 DONT_DELETE_INVALID](C26404.md)所有者を削除しないでください\<T > 無効な状態である可能性があります。 参照してください[C++ Core Guidelines R.3](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-ptr)します。

[C26405 DONT_ASSIGN_TO_VALID](C26405.md)所有者に割り当てないでください\<T > 有効な状態である可能性があります。 参照してください[C++ Core Guidelines R.3](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-ptr)します。

[C26406 DONT_ASSIGN_RAW_TO_OWNER](C26406.md)所有者に生のポインターを割り当てないでください\<T >。 参照してください[C++ Core Guidelines R.3](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-ptr)します。

[C26407 DONT_HEAP_ALLOCATE_UNNECESSARILY](C26407.md) Prefer scoped objects, don't heap-allocate unnecessarily. 参照してください[C++ Core Guidelines R.5](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-scoped)します。

[C26429 USE_NOTNULL](C26429.md)シンボル 'symbol %' が null 性テスト、not_ として指定できます。 参照してください[C++ Core Guidelines F.23](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#f23-use-a-not_nullt-to-indicate-that-null-is-not-a-valid-value)します。

[C26430 TEST_ON_ALL_PATHS](C26430.md)シンボル 'symbol %' には、すべてのパスでの null 性テストされていません。 参照してください[C++ Core Guidelines F.23](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#f23-use-a-not_nullt-to-indicate-that-null-is-not-a-valid-value)します。

[C26431 DONT_TEST_NOTNULL](C26431.md) 'expr %' の式の型は、既に gsl::not_null です。 Null 性はテストしないでください。 参照してください[C++ Core Guidelines F.23](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#f23-use-a-not_nullt-to-indicate-that-null-is-not-a-valid-value)します。

## <a name="raw_pointer-group"></a>RAW_POINTER グループ

[C26400 NO_RAW_POINTER_ASSIGNMENT](c26400.md)所有者の割り当てまたは関数呼び出しの結果を割り当てないでください\<T > 値を返す生のポインターには、所有者を使用して\<T > 代わりにします。 参照してください[C++ Core Guidelines I.11](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Ri-raw)します。

[C26401 DONT_DELETE_NON_OWNER](c26401.md) owner ではない生のポインターを削除しないでください\<T >。 参照してください[C++ Core Guidelines I.11](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Ri-raw)します。

[C26402 DONT_HEAP_ALLOCATE_MOVABLE_RESULT](C26402.md)  Return a scoped object instead of a heap-allocated if it has a move constructor. 参照してください[C++ Core Guidelines R.3](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-ptr)します。

[C26408 NO_MALLOC_FREE](C26408.md) malloc() と free() は避け、nothrow 版の new を delete を使用します。 参照してください[C++ Core Guidelines R.10](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-mallocfree)します。

[C26409 NO_NEW_DELETE](C26409.md)新しいを呼び出すことは避けと delete を明示的に、std::make_unique ごを使用して、\<T > 代わりにします。 参照してください[C++ Core Guidelines R.11](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-newdelete)します。

[C26429 USE_NOTNULL](C26429.md)シンボル 'symbol %' が null 性テスト、not_ として指定できます。 参照してください[C++ Core Guidelines F.23](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#f23-use-a-not_nullt-to-indicate-that-null-is-not-a-valid-value)します。

[C26430 TEST_ON_ALL_PATHS](C26430.md)シンボル 'symbol %' には、すべてのパスでの null 性テストされていません。 参照してください[C++ Core Guidelines F.23](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#f23-use-a-not_nullt-to-indicate-that-null-is-not-a-valid-value)します。

[C26431 DONT_TEST_NOTNULL](C26431.md) 'expr %' の式の型は、既に gsl::not_null です。 Null 性はテストしないでください。 参照してください[C++ Core Guidelines F.23](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#f23-use-a-not_nullt-to-indicate-that-null-is-not-a-valid-value)します。

[C26481 NO_POINTER_ARITHMETIC](C26481.md)ポインターの算術演算を使用しないでください。 代わりに span を使用します。 参照してください[C++ Core ガイドライン Bounds.1](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#SS-bounds)します。

[C26485 NO_ARRAY_TO_POINTER_DECAY](C26485.md).
式 'expr %': 配列ポインターへの減退からなし。 参照してください[C++ Core ガイドライン Bounds.3](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#SS-bounds)します。

## <a name="unique_pointer-group"></a>UNIQUE_POINTER Group

[C26410 NO_REF_TO_CONST_UNIQUE_PTR](C26410.md) 'パラメーター %'、パラメーターへの参照は、`const`ユニーク ポインターは、const T * または const T を使用して、&、代わりにします。 参照してください[C++ Core Guidelines R.32](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-uniqueptrparam)します。

[C26411 NO_REF_TO_UNIQUE_PTR](C26411.md) T * または T を使用して 'パラメーター %' のパラメーターはユニーク ポインターに対する参照であり、再割り当てもリセットは、&、代わりにします。 参照してください[C++ Core Guidelines R.33](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-reseat)します。

[C26414 RESET_LOCAL_SMART_PTR](C26414.md)移動、コピー、再割り当て、またはローカル スマート ポインター 'シンボル %' をリセットします。 参照してください[C++ Core Guidelines R.5](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-scoped)します。

[C26415 SMART_PTR_NOT_NEEDED](C26415.md)スマート ポインター パラメーター 'シンボル %' が含まれているポインターへのアクセスにのみ使用します。 T * または T を使用すると、代わりにします。 参照してください[C++ Core Guidelines R.30](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-smartptrparam)します。

## <a name="shared_pointer-group"></a>SHARED_POINTER グループ

[C26414 RESET_LOCAL_SMART_PTR](C26414.md)移動、コピー、再割り当て、またはローカル スマート ポインター 'シンボル %' をリセットします。 参照してください[C++ Core Guidelines R.5](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-scoped)します。

[C26415 SMART_PTR_NOT_NEEDED](C26415.md)スマート ポインター パラメーター 'シンボル %' が含まれているポインターへのアクセスにのみ使用します。 T * または T を使用すると、代わりにします。 参照してください[C++ Core Guidelines R.30](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-smartptrparam)します。

[C26416 NO_RVALUE_REF_SHARED_PTR](C26416.md)右辺値参照によって渡される共有ポインター パラメーター 'シンボル %' です。 代わりに、値によって渡します。 参照してください[C++ Core Guidelines R.34](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-sharedptrparam-owner)します。

[C26417 NO_LVALUE_REF_SHARED_PTR](C26417.md)共有ポインター パラメーター 'シンボル %' が参照によって渡されるとリセットまたは再割り当ています。 T * または T を使用すると、代わりにします。 参照してください[C++ Core Guidelines R.35](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-sharedptrparam)します。

[C26418 NO_VALUE_OR_CONST_REF_SHARED_PTR](C26418.md) Shared pointer parameter '%symbol%' is not copied or moved. T * または T を使用すると、代わりにします。 参照してください[C++ Core Guidelines R.36](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-sharedptrparam-const)します。

## <a name="declaration-group"></a>宣言のグループ

[C26426 NO_GLOBAL_INIT_CALLS](C26426.md)グローバル初期化子は非 constexpr 関数 'シンボル %' です。 参照してください[C++ Core Guidelines I.22](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#i22-avoid-complex-initialization-of-global-objects)します。

[C26427 NO_GLOBAL_INIT_EXTERNS](C26427.md)グローバル初期化子 'シンボル %' の extern オブジェクトにアクセスします。 参照してください[C++ Core Guidelines I.22](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#i22-avoid-complex-initialization-of-global-objects)します。

[C26444 NO_UNNAMED_RAII_OBJECTS](c26444.md)無名のカスタムの構築と破棄を持つオブジェクトを避けてください。 参照してください[ES.84: (しようとしないでください) 名前のないローカル変数を宣言](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md)します。

## <a name="class-group"></a>クラスのグループ

[C26432 DEFINE_OR_DELETE_SPECIAL_OPS](C26432.md)定義型 'シンボル %' で、既定の操作を削除するかを定義またはそのすべてを削除します。 参照してください[C++ Core Guidelines C.21](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#c21-if-you-define-or-delete-any-default-operation-define-or-delete-them-all)します。

[C26433 OVERRIDE_EXPLICITLY](c26433.md)関数 'シンボル %' を 'override' とマークする必要があります。 参照してください[C.128: 仮想関数が正確に 1 つのオーバーライドでは仮想、または最後に指定する必要があります](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#c128-virtual-functions-should-specify-exactly-one-of-virtual-override-or-final)します。

[C26434 DONT_HIDE_METHODS](C26434.md)関数 '%symbol_1% 'が 'symbol_2%' の非仮想関数を非表示にします。 参照してください[C++ Core Guidelines C.128](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#c128-virtual-functions-should-specify-exactly-one-of-virtual-override-or-final)します。

[C26435 SINGLE_VIRTUAL_SPECIFICATION](c26435.md)関数 'シンボル %' は 'virtual'、'override' または 'final' の 1 つだけを指定する必要があります。 参照してください[C.128: 仮想関数が正確に 1 つのオーバーライドでは仮想、または最後に指定する必要があります](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md)します。

[C26436 NEED_VIRTUAL_DTOR](C26436.md)かパブリック仮想または保護された非仮想デストラクターの型 '% のシンボル %' で仮想関数が必要です。 参照してください[C++ Core Guidelines C.35](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#c35-a-base-class-destructor-should-be-either-public-and-virtual-or-protected-and-nonvirtual)します。

[C26443 NO_EXPLICIT_DTOR_OVERRIDE](c26443.md)オーバーライド デストラクターでは、明示的な 'オーバーライド' または '仮想' 指定子は使用しないでください。 参照してください[C.128: 仮想関数が正確に 1 つのオーバーライドでは仮想、または最後に指定する必要があります](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md)します。

## <a name="type-group"></a>種類のグループ

[C26437 DONT_SLICE](C26437.md)スライスしないでします。 参照してください[C++ Core Guidelines ES.63](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#es63-dont-slice)します。

## <a name="style-group"></a>スタイルのグループ

[C26438 NO_GOTO](C26438.md)回避`goto`します。 参照してください[C++ Core Guidelines ES.76](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#es76-avoid-goto)します。

## <a name="function-group"></a>関数グループ

[C26439 SPECIAL_NOEXCEPT](C26439.md)この種の関数がスローしないことがあります。 宣言`noexcept`します。 参照してください[C++ Core Guidelines F.6](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#f6-if-your-function-may-not-throw-declare-it-noexcept)します。

[C26440 DECLARE_NOEXCEPT](C26440.md) 'シンボル %' 関数を宣言する`noexcept`します。 参照してください[C++ Core Guidelines F.6](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#f6-if-your-function-may-not-throw-declare-it-noexcept)します。

[C26447 DONT_THROW_IN_NOEXCEPT](c26447.md)関数が宣言されて**noexcept**が例外をスローする可能性がある関数を呼び出しています。
参照してください[C++ Core Guidelines: F.6: 場合は、関数はスローされませんが、宣言 noexcept](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#f6-if-your-function-may-not-throw-declare-it-noexcept)します。

## <a name="concurrency-group"></a>同時実行のグループ

[C26441 NO_UNNAMED_GUARDS](C26441.md)ガード オブジェクトを指定する必要があります。 参照してください[C++ コア ガイドライン cp.44](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#cp44-remember-to-name-your-lock_guards-and-unique_locks)します。

## <a name="const-group"></a>CONST グループ

[C26460 USE_CONST_REFERENCE_ARGUMENTS](c26460.md)関数 '% 関数 %' の参照引数 '引数 %' としてマークできます`const`します。 参照してください[C++ コア ガイドライン con.3](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rconst-ref)します。

[C26461 USE_CONST_POINTER_ARGUMENTS](c26461.md): 関数 '% 関数 %' のポインター引数 '引数 %' へのポインターとしてマークできます`const`します。 参照してください[C++ コア ガイドライン con.3](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rconst-ref)します。

[C26462 USE_CONST_POINTER_FOR_VARIABLE](c26462.md) '% 変数 %' が指す値が 1 回だけ割り当てへのポインターとしてマーク`const`します。 参照してください[C++ コア ガイドライン con.4](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#con4-use-const-to-define-objects-with-values-that-do-not-change-after-construction)します。

[C26463 USE_CONST_FOR_ELEMENTS](c26463.md) '配列 %' の配列の要素が 1 回だけマーク要素で割り当てられた`const`します。 参照してください[C++ コア ガイドライン con.4](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#con4-use-const-to-define-objects-with-values-that-do-not-change-after-construction)します。

[C26464 USE_CONST_POINTER_FOR_ELEMENTS](c26464.md) '配列 %' の配列の要素を指す値が 1 回だけへのポインターとしてマーク要素で割り当てられた`const`します。 参照してください[C++ コア ガイドライン con.4](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#con4-use-const-to-define-objects-with-values-that-do-not-change-after-construction)します。

[C26496 USE_CONST_FOR_VARIABLE](c26496.md)変数 '% 変数 %' が 1 回だけ割り当て、としてマーク`const`します。 参照してください[C++ コア ガイドライン con.4](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#con4-use-const-to-define-objects-with-values-that-do-not-change-after-construction)します。

[C26497 USE_CONSTEXPR_FOR_FUNCTION](c26497.md)この関数 % 関数のマークを付けるでした`constexpr`コンパイル時の評価が必要な場合。 参照してください[C++ Core Guidelines F.4](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rf-constexpr)します。

[C26498 USE_CONSTEXPR_FOR_FUNCTIONCALL](c26498.md)この関数の呼び出し関数 % が使用できる`constexpr`コンパイル時の評価が必要な場合。 参照してください[C++ コア ガイドライン con.5](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rconst-constexpr)します。

## <a name="type-group"></a>種類のグループ

[C26465 NO_CONST_CAST_UNNECESSARY](c26465.md)使わない`const_cast`キャストに`const`します。 `const_cast` 不要です。この変換では、const 性または揮発性を削除中はされません。 参照してください[C++ Core ガイドライン Type.3](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Pro-type-constcast)します。

[C26466 NO_STATIC_DOWNCAST_POLYMORPHIC](c26466.md)使わない`static_cast`ダウン キャストします。 ポリモーフィックな型からキャストでは、dynamic_cast を使用する必要があります。 参照してください[C++ Core ガイドライン Type.2](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Pro-type-downcast)します。

[C26471 NO_REINTERPRET_CAST_FROM_VOID_PTR](c26471.md) Don't use `reinterpret_cast`. Void * からのキャストが使用できる`static_cast`します。 参照してください[C++ Core ガイドライン Type.1](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Pro-type-reinterpretcast)します。

[C26472 NO_CASTS_FOR_ARITHMETIC_CONVERSION](C26472.md)使用しないでください、`static_cast`の算術変換します。 使用中かっこの初期化、gsl:、またはします。 参照してください[C++ Core ガイドライン Type.1](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Pro-type-reinterpretcast)します。

[C26473 NO_IDENTITY_CAST](C26473.md)ソースの種類とターゲットの種類が同じであるポインター型間でのキャストはありません。 参照してください[C++ Core ガイドライン Type.1](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Pro-type-reinterpretcast)します。

[C26474 NO_IMPLICIT_CAST](C26474.md)ポインター型の変換は暗黙的な可能性がありますとの間でのキャストはありません。 参照してください[C++ Core ガイドライン Type.1](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Pro-type-reinterpretcast)します。

[C26475 NO_FUNCTION_STYLE_CASTS](C26475.md)関数 C スタイルのキャストは使用しないでください。 参照してください[C++ Core Guidelines ES.49](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#es49-if-you-must-use-a-cast-use-a-named-cast)します。

[C26490 NO_REINTERPRET_CAST](c26490.md)使わない`reinterpret_cast`します。 参照してください[C++ Core ガイドライン Type.1](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#SS-type)します。

[C26491 NO_STATIC_DOWNCAST](c26490.md)使わない`static_cast`ダウン キャストします。 参照してください[C++ Core ガイドライン Type.2](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#SS-type)します。

[C26492 NO_CONST_CAST](c26492.md)使わない`const_cast`キャストに`const`します。 参照してください[C++ Core ガイドライン Type.3](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#SS-type)します。

[C26493 NO_CSTYLE_CAST](c26493.md) C スタイルのキャストを使用しないでください。 参照してください[C++ Core ガイドライン Type.4](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#SS-type)します。

[C26494 VAR_USE_BEFORE_INIT](c26494.md)変数 '% 変数 %' が初期化されていません。 常にオブジェクトを初期化します。 参照してください[C++ Core ガイドライン Type.5](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#SS-type)します。

[C26495 MEMBER_UNINIT](c26495.md)変数 '% 変数 %' が初期化されていません。 常にメンバー変数を初期化します。 参照してください[C++ Core ガイドライン Type.6](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#SS-type)します。

## <a name="bounds-group"></a>境界グループ

[C26446 USE_GSL_AT](c26446.md)使用したい`gsl::at()`添字演算子の代わりにします。 参照してください[C++ Core Guidelines: Bounds.4: 標準ライブラリ関数と境界チェックではない型を使用しない](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#probounds-bounds-safety-profile)します。

[C26481 NO_POINTER_ARITHMETIC](C26481.md).
ポインターの算術演算を使用しないでください。 代わりに span を使用します。 参照してください[C++ Core ガイドライン Bounds.1](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#SS-bounds)

[C26482 NO_DYNAMIC_ARRAY_INDEXING](c26482.md)定数式を使用して配列にのみインデックスを作成します。 参照してください[C++ Core ガイドライン Bounds.2](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#SS-bounds)

[C26483 STATIC_INDEX_OUT_OF_RANGE](c26483.md)値 %value% の値が範囲外 (0 の場合、バインドされた %) の変数 '% 変数 %' です。 配列の境界内にある定数式を使用して配列にインデックスのみ。 参照してください[C++ Core ガイドライン Bounds.2](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#SS-bounds)

[C26485 NO_ARRAY_TO_POINTER_DECAY](C26485.md)式 'expr %': 配列ポインターへの減退からなし。 参照してください[C++ Core ガイドライン Bounds.3](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#SS-bounds)

## <a name="gsl-group"></a>GSL グループ

[C26445 NO_SPAN_REF](c26445.md)への参照を`gsl::span`または`std::string_view`有効期間の問題の兆候である可能性があります。
参照してください[C++ Core ガイドライン GSL.view: ビュー](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#gslview-views)

[C26446 USE_GSL_AT](c26446.md)使用したい`gsl::at()`添字演算子の代わりにします。 参照してください[C++ Core Guidelines: Bounds.4: 標準ライブラリ関数と境界チェックではない型を使用しない](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#probounds-bounds-safety-profile)します。

[C26448 USE_GSL_FINALLY](c26448.md)最後のアクションが意図されている場合は、`gsl::finally` の使用を検討してください。 参照してください[C++ Core Guidelines: GSL.util: ユーティリティ](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#SS-utilities)します。

[C26449 NO_SPAN_FROM_TEMPORARY](c26449.md) 
 `gsl::span`または`std::string_view`テンポラリから作成は無効になるときにテンポラリが無効になります。 参照してください[C++ Core Guidelines: GSL.view: ビュー](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#gslview-views)します。

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
[C++ Core ガイドラインのチェッカーを使用します。](using-the-cpp-core-guidelines-checkers.md)
