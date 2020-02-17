---
title: ロック動作に注釈を付ける
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- _Releases_nonreentrant_lock_
- _Lock_kind_mutex_
- _Lock_kind_critical_section_
- _Acquires_lock_
- _Releases_lock_
- _Has_lock_kind_
- _Releases_exclusive_lock_
- _Post_same_lock_
- _Requires_exclusive_lock_held_
- _Requires_shared_lock_held_
- _Lock_kind_semaphore_
- _Requires_lock_held_
- _Acquires_exclusive_lock_
- _Create_lock_level_
- _Acquires_nonreentrant_lock_
- _Releases_shared_lock_
- _Has_lock_level_
- _Lock_kind_spin_lock_
- _Requires_lock_not_held_
- _Acquires_shared_lock_
- _Requires_no_locks_held_
- _Lock_level_order_
- _Lock_kind_event_
ms.assetid: 07769c25-9b97-4ab7-b175-d1c450308d7a
author: corob-msft
ms.author: corob
manager: markl
ms.workload:
- multiple
ms.openlocfilehash: ae15230557ee0c415082f981a7ad3588694eadea
ms.sourcegitcommit: 68f893f6e472df46f323db34a13a7034dccad25a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/15/2020
ms.locfileid: "77265133"
---
# <a name="annotating-locking-behavior"></a>ロック動作に注釈を付ける
マルチスレッドプログラムの同時実行のバグを回避するには、常に適切なロックの規範に従い、SAL 注釈を使用します。

同時実行のバグは、非決定的であるため、再現、診断、デバッグが困難です。 スレッドインターリーブについての考え方は最適ではなく、複数のスレッドを持つコード本体をデザインする場合には現実的ではありません。 したがって、マルチスレッドプログラムのロックの原則に従うことをお勧めします。 たとえば、複数のロックを取得している間にロックの順序を obeying と、デッドロックを回避できます。また、共有リソースにアクセスする前に適切な保護ロックを取得することで、競合状態を防ぐことができます。

残念ながら、一見単純なロックの規則は実際には難しい場合があります。 現在のプログラミング言語とコンパイラの基本的な制限は、同時実行要件の仕様と分析を直接サポートしないことです。 プログラマは、ロックの使用方法についての意図を表すために、非公式のコードコメントに依存する必要があります。

同時実行 SAL 注釈は、ロックの副作用、ロックの責任、データ guardianship、ロック順序の階層、およびその他の想定されるロック動作を指定できるように設計されています。 暗黙的な規則を明示的にすると、SAL の同時実行の注釈によって、コードでロック規則を使用する方法を一貫した方法で記述できます。 同時実行の注釈を利用すると、競合状態、デッドロック、同期操作の不一致、およびその他の微妙な同時実行エラーを検出するためのコード分析ツールの機能も強化されます。

## <a name="general-guidelines"></a>一般的なガイドライン
注釈を使用すると、実装 (呼び出し先) とクライアント (呼び出し元) の間の関数定義によって暗黙的に示されるコントラクトと、分析をさらに向上させることができるプログラムのインバリアントとその他のプロパティを示すことができます。

SAL は、重要なセクション、ミューテックス、スピンロック、およびその他のリソースオブジェクトなど、さまざまな種類のロックプリミティブをサポートしています。 多くの同時実行の注釈は、パラメーターとしてロック式を受け取ります。 慣例により、ロックは、基になるロックオブジェクトのパス式によって示されます。

いくつかのスレッド所有権の規則に注意してください。

- スピンロックは、明確なスレッド所有権を持つロックをカウントしません。

- Mutex およびクリティカルセクションは、スレッドの所有権が明確になるようにカウントされたロックです。

- セマフォとイベントは、明確なスレッド所有権を持たないロック数をカウントします。

## <a name="locking-annotations"></a>ロックの注釈
次の表に、ロックの注釈の一覧を示します。

|注釈|[説明]|
|----------------|-----------------|
|`_Acquires_exclusive_lock_(expr)`|関数に注釈を付け、post 状態のときに、`expr`によって指定されたロックオブジェクトの排他ロックカウントによって関数がインクリメントされることを示します。|
|`_Acquires_lock_(expr)`|関数に注釈を付け、post 状態のときに、`expr`によって指定されたロックオブジェクトのロックカウントによって関数がインクリメントされることを示します。|
|`_Acquires_nonreentrant_lock_(expr)`|`expr` によって指定されたロックが取得されます。  ロックが既に保持されている場合は、エラーが報告されます。|
|`_Acquires_shared_lock_(expr)`|関数に注釈を付け、post 状態のときに、`expr`によって指定されたロックオブジェクトの共有ロックカウントによって関数がインクリメントされることを示します。|
|`_Create_lock_level_(name)`|シンボルを宣言するステートメントがロックレベルであり、注釈 `_Has_Lock_level_` と `_Lock_level_order_`に使用できるように `name` ます。|
|`_Has_lock_kind_(kind)`|リソースオブジェクトの型情報を絞り込むために、任意のオブジェクトに注釈を加えます。 場合によっては、さまざまな種類のリソースに共通の型が使用され、オーバーロードされた型は、さまざまなリソース間でセマンティック要件を区別するのに十分ではありません。 定義済みの `kind` パラメーターの一覧を次に示します。<br /><br /> `_Lock_kind_mutex_`<br /> Mutex のロックの種類 ID。<br /><br /> `_Lock_kind_event_`<br /> イベントのロックの種類 ID。<br /><br /> `_Lock_kind_semaphore_`<br /> セマフォのロックの種類 ID。<br /><br /> `_Lock_kind_spin_lock_`<br /> スピンロックのロックの種類の ID。<br /><br /> `_Lock_kind_critical_section_`<br /> クリティカルセクションのロックの種類 ID。|
|`_Has_lock_level_(name)`|ロックオブジェクトに注釈を付け、`name`のロックレベルを与えます。|
|`_Lock_level_order_(name1, name2)`|`name1` と `name2`間のロックの順序を与えるステートメント。  レベル `name2`を持つロックの前に、レベル `name1` を持つロックを取得する必要があります。|
|`_Post_same_lock_(expr1, expr2)`|関数に注釈を付け、post 状態で、2つのロック (`expr1` と `expr2`) が同じロックオブジェクトであるかのように処理されることを示します。|
|`_Releases_exclusive_lock_(expr)`|関数に注釈を付け、post 状態のときに、`expr`によって指定されたロックオブジェクトの排他ロックカウントによって関数がデクリメントされることを示します。|
|`_Releases_lock_(expr)`|関数に注釈を付け、post 状態では、`expr`によって指定されたロックオブジェクトのロックカウントによって関数がデクリメントされることを示します。|
|`_Releases_nonreentrant_lock_(expr)`|`expr` によって指定されたロックが解放されます。 ロックが現在保持されていない場合は、エラーが報告されます。|
|`_Releases_shared_lock_(expr)`|関数に注釈を付け、post 状態のときに、`expr`によって指定されたロックオブジェクトの共有ロックカウントによって関数がデクリメントされることを示します。|
|`_Requires_lock_held_(expr)`|関数に注釈を付け、pre 状態で、`expr` によって指定されたオブジェクトのロックカウントが少なくとも1つであることを示します。|
|`_Requires_lock_not_held_(expr)`|関数に注釈を付け、pre 状態では `expr` によって指定されたオブジェクトのロックカウントが0であることを示します。|
|`_Requires_no_locks_held_`|関数に注釈を指定し、チェッカーが認識しているすべてのロックのロック数が0であることを示します。|
|`_Requires_shared_lock_held_(expr)`|関数に注釈を付け、pre 状態で、`expr` によって指定されたオブジェクトの共有ロックカウントが少なくとも1つであることを示します。|
|`_Requires_exclusive_lock_held_(expr)`|関数に注釈を付け、pre 状態で、`expr` によって指定されたオブジェクトの排他ロックカウントが少なくとも1つであることを示します。|

## <a name="sal-intrinsics-for-unexposed-locking-objects"></a>非公開のロック オブジェクトに対する SAL の組み込み
特定のロックオブジェクトは、関連付けられているロック関数の実装によって公開されません。  次の表に、これらの非公開のロックオブジェクトを操作する関数に対する注釈を有効にする SAL 組み込み変数を示します。

|注釈|[説明]|
|----------------|-----------------|
|`_Global_cancel_spin_lock_`|キャンセルスピンロックについて説明します。|
|`_Global_critical_region_`|クリティカル領域について説明します。|
|`_Global_interlock_`|インタロック操作について説明します。|
|`_Global_priority_region_`|優先度領域について説明します。|

## <a name="shared-data-access-annotations"></a>共有データ アクセスの注釈
次の表は、共有データアクセスの注釈を示しています。

|注釈|[説明]|
|----------------|-----------------|
|`_Guarded_by_(expr)`|変数に注釈を付け、変数がアクセスされるたびに、`expr` によって指定されたロックオブジェクトのロック数が少なくとも1つであることを示します。|
|`_Interlocked_`|変数に注釈をし、`_Guarded_by_(_Global_interlock_)`に相当します。|
|`_Interlocked_operand_`|注釈付き関数のパラメーターは、さまざまなインタロックされた関数のいずれかのターゲットオペランドです。  これらのオペランドには、特定の追加プロパティが必要です。|
|`_Write_guarded_by_(expr)`|変数に注釈を付け、変数が変更されるたびに、`expr` によって指定されたロックオブジェクトのロック数が少なくとも1つであることを示します。|

## <a name="smart-lock-and-raii-annotations"></a>注釈の Smart Lock と RAII
通常、スマートロックはネイティブロックをラップし、その有効期間を管理します。 次の表に、`move` セマンティクスをサポートするスマートロックと RAII コーディングパターンで使用できる注釈を示します。

|注釈|[説明]|
|----------------|-----------------|
|`_Analysis_assume_smart_lock_acquired_`|スマートロックが取得されたことを想定するようにアナライザーに指示します。 この注釈では、パラメーターとして参照ロックの種類が想定されています。|
|`_Analysis_assume_smart_lock_released_`|スマートロックが解放されたことを想定するようにアナライザーに指示します。 この注釈では、パラメーターとして参照ロックの種類が想定されています。|
|`_Moves_lock_(target, source)`|`source` オブジェクトから `target`にロック状態を転送する `move constructor` 操作について説明します。 `target` は新しく構築されたオブジェクトと見なされるため、以前の状態が失われ、`source` の状態に置き換えられます。 `source` も、ロック数またはエイリアシングターゲットを使用せずにクリーン状態にリセットされますが、それを指すエイリアスは変更されません。|
|`_Replaces_lock_(target, source)`|ソースから状態を転送する前に、ターゲットロックが解放される `move assignment operator` セマンティクスについて説明します。 これは、前に `_Releases_lock_(target)`を `_Moves_lock_(target, source)` の組み合わせと見なすことができます。|
|`_Swaps_locks_(left, right)`|オブジェクト `left` と `right` の状態を交換することを前提としている標準の `swap` 動作について説明します。 交換される状態には、ロック数とエイリアスターゲット (存在する場合) が含まれます。 `left` オブジェクトと `right` オブジェクトを指すエイリアスは変更されません。|
|`_Detaches_lock_(detached, lock)`|ロックラッパーの種類で、含まれているリソースと関連付け解除を許可するシナリオについて説明します。 これは、`std::unique_ptr` が内部ポインターで動作する方法と似ています。プログラマはポインターを抽出し、スマートポインターコンテナーをクリーンな状態にしておくことができます。 同様のロジックは `std::unique_lock` でサポートされており、カスタムロックラッパーに実装できます。 デタッチされたロックは、その状態 (ロックカウントとエイリアスターゲットが存在する場合) を保持しますが、ラッパーは、独自のエイリアスを保持しながら、ゼロロックカウントとエイリアスターゲットを含まないようにリセットされます。 ロック数に対する操作 (解放および取得) はありません。 この注釈は `_Moves_lock_` とまったく同じように動作しますが、デタッチされた引数は `this`ではなく `return` である必要があります。|

## <a name="see-also"></a>関連項目

- [SAL 注釈を使って C/C++ のコード障害を減らす方法](../code-quality/using-sal-annotations-to-reduce-c-cpp-code-defects.md)
- [SAL について](../code-quality/understanding-sal.md)
- [関数パラメーターおよび戻り値の注釈設定](../code-quality/annotating-function-parameters-and-return-values.md)
- [関数の動作に注釈を付ける](../code-quality/annotating-function-behavior.md)
- [構造体とクラスに注釈を付ける](../code-quality/annotating-structs-and-classes.md)
- [注釈を適用するタイミングと場所の指定](../code-quality/specifying-when-and-where-an-annotation-applies.md)
- [組み込み関数](../code-quality/intrinsic-functions.md)
- [ベスト プラクティスと例](../code-quality/best-practices-and-examples-sal.md)
- [コード分析チームのブログ](https://blogs.msdn.microsoft.com/codeanalysis/)
