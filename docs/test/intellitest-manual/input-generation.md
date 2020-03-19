---
title: 動的なシンボリック実行 | Microsoft IntelliTest 開発者テスト ツール
ms.date: 05/02/2017
ms.topic: conceptual
helpviewer_keywords:
- IntelliTest, Dynamic symbolic execution
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
author: mikejo5000
ms.openlocfilehash: e5a3248d3f081bcab08c08110d305f0aa6235817
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "79306993"
---
# <a name="input-generation-using-dynamic-symbolic-execution"></a>動的なシンボリック実行を使用する入力生成

IntelliTest は、プログラムの分岐条件を分析して、[パラメーター化された単体テスト](test-generation.md#parameterized-unit-testing)の入力を生成します。 テスト入力は、プログラムの新しい分岐動作をトリガーできるかどうかに応じて、選択されます。 分析はインクリメンタル処理です。 仮テスト入力パラメーター `q: I -> {true, false}` に対して、述語 `I` が絞り込まれます。 `q` は、IntelliTest で既に観察されている動作セットを表します。 最初は、まだ何も観測されていないため、`q := false` となります。

ループの手順は次のとおりです。

1. IntelliTest により、`i`制約ソルバー`q(i)=false`を使用して、[ のように入力 ](#constraint-solver) が決定されます。 構造により、入力 `i` では新しい実行パスが使用されます。 最初は、これが意味するのは、`i` が何らかの入力になることです。実行パスが見つけられていないためです。

1. IntelliTest により、選択された入力 `i` でテストが実行され、テストの実行とテスト対象のプログラムが監視されます。

1. 実行中、プログラムは、プログラムのすべての条件付き分岐で決定される特定のパスを使用します。 実行を決定するすべての条件セットは*パス条件*と呼ばれ、仮入力パラメーターで述語 `p: I -> {true, false}` として書き込まれます。 IntelliTest は、この述語の表現を計算します。

1. IntelliTest で `q := (q or p)` が設定されます。 つまり、`p` で表されるパスが示されたことを記録します。

1. 手順 1. に進みます。

IntelliTest の[制約ソルバー](#constraint-solver)は、.NET プログラムで表示される可能性のあるすべての型の値を処理できます。

* [整数](#integers-and-floats)と[浮動小数点数](#integers-and-floats)
* [オブジェクト](#objects)
* [構造体](#structs)
* [配列](#arrays-and-strings)と[文字列](#arrays-and-strings)

IntelliTest は、示された前提事項に違反する入力をフィルター処理で除外します。

即時入力 ([パラメーター化された単体テスト](test-generation.md#parameterized-unit-testing)に対する引数) を除き、テストでは [PexChoose](static-helper-classes.md#pexchoose) 静的クラスからさらに入力値を取得できます。 選択内容によって、[パラメーター化されたモック](#parameterized-mocks)の動作も決まります。

## <a name="constraint-solver"></a>制約ソルバー

IntelliTest は制約ソルバーを使用して、テストの関連する入力値と、テスト対象のプログラムを決定します。

IntelliTest は [Z3](https://github.com/Z3Prover/z3/wiki) 制約ソルバーを使用します。

## <a name="dynamic-code-coverage"></a>動的コード カバレッジ

ランタイム監視の副作用として、IntelliTest は動的コード カバレッジ データを収集します。
これは*動的*と呼ばれます。IntelliTest は実行されたコードのみを認識するため、他のカバレッジ ツールで通常行われるようにカバレッジに絶対値を指定できません。

たとえば、IntelliTest が動的カバレッジを 5/10 基本ブロックとして報告した場合、10 個のうち 5 個のブロックがカバーされたことを意味します。この場合、分析でこれまでに到達したすべてのメソッド (テスト対象のアセンブリに存在するすべてのメソッドではない) のブロックの総数は 10 です。
その後の分析で、さらに到達可能なメソッドが検出されたときに、分子 (この例では 5) と分母 (10) の両方が増える可能性があります。

## <a name="integers-and-floats"></a>整数と浮動小数点数

IntelliTest の[制約ソルバー](#constraint-solver)は、テストとテスト対象のプログラムに対して異なる実行パスをトリガーするために、**byte**、**int**、**float** などのプリミティブ型のテスト入力値を決定します。

## <a name="objects"></a>Objects

IntelliTest で[既存の .NET クラスのインスタンスを作成](#existing-classes)できます。また、特定のインターフェイスを実装し、用途に応じて異なる方法で動作する[モック オブジェクトの作成](#parameterized-mocks)を IntelliTest を使用して自動で行うこともできます。

<a name="existing-classes"></a>
## <a name="instantiate-existing-classes"></a>既存クラスのインスタンス化

**何が問題なのでしょうか。**

IntelliTest は、テストとテスト対象のプログラムを実行するときに実行された命令を監視します。 特に、フィールドへのすべてのアクセスを監視します。 その後、[制約ソルバー](#constraint-solver)を使用して、オブジェクトとそのフィールド値を含む、新しいテスト入力を決定し、テストとテスト対象のプログラムが他の適切な方法で動作するようにします。

つまり、IntelliTest は、特定の型のオブジェクトを作成し、そのフィールド値を設定する必要があります。 クラスが[表示](#visibility)され、既定のコンストラクターが[表示](#visibility)される場合、IntelliTest はそのクラスのインスタンスを作成できます。
クラスのすべてのフィールドが[表示](#visibility)される場合、IntelliTest で自動的にフィールドを設定できます。

型が表示されない場合や、フィールドが[表示](#visibility)されない場合、IntelliTest のみでオブジェクトを作成して、適切な状態にし、最大のコード カバレッジを実現することはできません。 IntelliTest の場合はリフレクションを使用して、任意の方法でインスタンスを作成して初期化することが可能ですが、通常、これは望ましくありません。オブジェクトが、通常のプログラム実行時には発生することのない状態になる可能性があるためです。 代わりに、IntelliTest はユーザーからのヒントに依存します。

## <a name="visibility"></a>表示

.NET には、詳細な可視性モデルがあります。型、メソッド、フィールド、その他のメンバーを**プライベート**、**パブリック**、**内部**などにすることができます。

IntelliTest は、テストを生成する際に、生成されたテストのコンテキスト内からの .NET 可視性ルールに関して正当なアクション (コンストラクター、メソッドの呼び出しや、フィールドの設定など) のみを実行しようとします。

ルールは以下のとおりです。

* **内部メンバーの可視性**
  * IntelliTest は、生成されたテストで、外部の [PexClass](attribute-glossary.md#pexclass) に表示された内部メンバーにアクセスできると見なします。
  .NET の **InternalsVisibleToAttribute** では、他のアセンブリに内部メンバーの可視性を拡張します。

* **[PexClass](attribute-glossary.md#pexclass) のプライベートおよびファミリ (C# で保護されている) メンバーの可視性**
  * IntelliTest は常に、[PexClass](attribute-glossary.md#pexclass) に直接、またはサブクラスに生成されたテストを配置します。 そのため、IntelliTest は、表示されたすべてのファミリ メンバー (C# で**保護されている**) を使用できると見なします。
  * 生成されたテストが (通常は部分クラスを使用して) [PexClass](attribute-glossary.md#pexclass) に直接配置されている場合、IntelliTest は [PexClass](attribute-glossary.md#pexclass) のすべてのプライベート メンバーも使用できると見なします。

* **パブリック メンバーの可視性**
  * IntelliTest は、[PexClass](attribute-glossary.md#pexclass) のコンテキストで表示される、エクスポートされたすべてのメンバーを使用できると見なします。

## <a name="parameterized-mocks"></a>パラメーター化されたモック

インターフェイス型のパラメーターを持つメソッドはどのようにテストするのですか? 非シール クラスについてはどうですか? IntelliTest は、このメソッドが呼び出されたときに、後でどの実装が使用されるかを認識できません。 おそらく、テスト時に使用できる実際の実装もありません。

従来の答えは、明示的な動作で*モック オブジェクト*を使用することです。

モック オブジェクトはインターフェイスを実装 (または、非シール クラスを拡張) します。 これは実際の実装ではなく、モック オブジェクトを使用するテストの実行を許可する単なるショートカットを表します。 その動作は、使用される各テスト ケースの一部として手動で定義します。 モック オブジェクトとその予期される動作の定義を容易にするツールは多数あります。それでも、この動作は手動で定義する必要があります。

モック オブジェクトのハード コーディングされた値の代わりに、IntelliTest は値を生成できます。 [パラメーター化された単体テスト](test-generation.md#parameterized-unit-testing)を有効にする場合と同じように、IntelliTest ではパラメーター化されたモックも有効にされます。

パラメーター化されたモックには次の 2 つの異なる実行モードがあります。

* **選択**: コードを探索する場合、パラメーター化されたモックは追加のテスト入力のソースであり、IntelliTest は対象の値を選択しようとします。
* **再生**: 以前に生成されたテストを実行する場合、パラメーター化されたモックはスタブのように (つまり、定義されたとおりに) 動作します。

パラメーター化されたモックの値を取得するには、[PexChoose](static-helper-classes.md#pexchoose) を使用します。

## <a name="structs"></a>構造体

IntelliTest の**構造体**の値に関する推論は、[オブジェクト](#objects)の処理方法に似ています。

## <a name="arrays-and-strings"></a>配列と文字列

IntelliTest は、テストとテスト対象のプログラムを実行するときに実行された命令を監視します。 特に、プログラムが文字列または配列の長さ (および多次元配列の下限と長さ) に依存する場合に監視します。
また、プログラムが文字列または配列のさまざまな要素を使用する方法を監視します。 その後、[制約ソルバー](#constraint-solver)を使用して、テストとテスト対象のプログラムが適切に動作するように長さと要素の値を決定します。

IntelliTest は、適切なプログラムの動作をトリガーするのに必要な配列と文字列のサイズを最小化しようとします。

<a name="additional-inputs"></a>
## <a name="obtain-additional-inputs"></a>追加入力の取得

[PexChoose](static-helper-classes.md#pexchoose) 静的クラスを使用して、テストへの追加入力を取得することができ、[パラメーター化されたモック](#parameterized-mocks)を実装できます。

## <a name="got-feedback"></a>フィードバックが欲しい場合

ご意見や機能に関するご要望を[開発者コミュニティ](https://developercommunity.visualstudio.com/content/idea/post.html?space=8)で投稿してください。

## <a name="further-reading"></a>関連項目

* [それはどのように機能しますか?](https://devblogs.microsoft.com/devops/smart-unit-tests-a-mental-model/)
