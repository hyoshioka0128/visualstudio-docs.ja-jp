---
title: 探索の範囲 | Microsoft IntelliTest 開発者テスト ツール
description: PexSettingsAttributeBase は、属性としての設定範囲に対する抽象基底クラスです。 名前付きプロパティを使用して設定を変更する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 05/02/2017
ms.topic: reference
helpviewer_keywords:
- IntelliTest, Exploration bounds
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
author: mikejo5000
ms.openlocfilehash: 075eaa4613a1afe6bdeb83a9e46e639b073a200a
ms.sourcegitcommit: 8a0d0f4c4910e2feb3bc7bd19e8f49629df78df5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/18/2020
ms.locfileid: "97667924"
---
# <a name="exploration-bounds"></a>探索の範囲

**PexSettingsAttributeBase** は、属性としての設定範囲に対する抽象基底クラスです。 IntelliTest での設定の概要については、「[ウォーターフォールの設定](settings-waterfall.md)」を参照してください。

この属性とその派生属性の名前付きプロパティを使用して、設定を変更することができます。

```csharp
[PexClass(MaxRuns = 10)]
public partial class FooTest {...}
```

* **制約解決の範囲**
  * [MaxConstraintSolverTime](#maxconstraintsolvertime) - [制約ソルバー](input-generation.md#constraint-solver)が、新しい別の実行パスに従うことになる入力を検出する必要がある時間 (秒単位)。
  * [MaxConstraintSolverMemory](#maxconstraintsolvermemory) - [制約ソルバー](input-generation.md#constraint-solver)が入力の検出に使用できるサイズ (メガバイト単位)。
* **探索パスの範囲**
  * [MaxBranches](#maxbranches) - 1 回の実行パス中に実行できる分岐の最大数。
  * [MaxCalls](#maxcalls) - 1 回の実行パス中に実行できる呼び出しの最大数。
  * [MaxStack](#maxstack) - 1 回の実行パス中の任意の時点でのスタックの最大サイズ。アクティブな呼び出しフレームの数として測定されます。
  * [MaxConditions](#maxconditions) - 1 回の実行パス中に確認できる入力に対する条件の最大数。
* **探索の範囲**
  * [MaxRuns](#maxruns) - 探索中に試行される実行の最大数。
  * [MaxRunsWithoutNewTests](#maxrunswithoutnewtests) - 新しいテストが生成されずに連続する実行の最大数。
  * [MaxRunsWithUniquePaths](#maxrunswithuniquepaths) - 探索中に試行される一意の実行パスでの実行の最大数。
  * [MaxExceptions](#maxexceptions) - 検出されたすべての実行パスの組み合わせで検索できる例外の最大数。
* **テスト スイート コード生成の設定**
  * [TestExcludePathBoundsExceeded](#testexcludepathboundsexceeded) - true の場合、パスの範囲のいずれか ([MaxCalls](#maxcalls)、[MaxBranches](#maxbranches)、[MaxStack](#maxstack)、[MaxConditions](#maxconditions)) を超える実行パスは無視されます。
  * [TestEmissionFilter](#testemissionfilter) - IntelliTest がテストを生成する必要がある状況を示します。
  * [TestEmissionBranchHits](#testemissionbranchhits) - IntelliTest が生成するテストの数を制御します。

<a name="maxconstraintsolvertime"></a>
## <a name="maxconstraintsolvertime"></a>MaxConstraintSolverTime

[制約ソルバー](input-generation.md#constraint-solver)が、新しい別の実行パスを使用することになる入力を計算する必要がある時間 (秒単位)。 これは **PexSettingsAttributeBase** とその派生型のオプションです。

IntelliTest がプログラムの実行パスを深く探索すればするほど、IntelliTest がプログラムの制御フローとデータ フローからビルドする制約システムが複雑になります。 時間制限に応じて、この値を設定して、IntelliTest が新しい実行パスを検出する時間を長くしたり短くしたりすることができます。

通常、タイムアウトの理由は、IntelliTest が、ソリューションがないことが認識されていない制約システムのソリューションを見つけようとすることです。 これはタイムアウトの最も一般的なケースであるため、範囲を増やしても意味がないかもしれません。

<a name="maxconstraintsolvermemory"></a>
## <a name="maxconstraintsolvermemory"></a>MaxConstraintSolverMemory

[制約ソルバー](input-generation.md#constraint-solver)が、新しい別の実行パスを使用することになる入力を計算する必要があるメガバイト数。 これは *PexSettingsAttributeBase** とその派生型のオプションです。

IntelliTest がプログラムの実行パスを深く探索すればするほど、IntelliTest がプログラムの制御フローとデータ フローからビルドする制約システムが複雑になります。 コンピューターの使用可能なメモリに応じて、IntelliTest がより複雑な制約システムに対応できるようにこの値を設定することができます。

通常、タイムアウトの理由は、IntelliTest が、ソリューションがないことが認識されていない制約システムのソリューションを見つけようとすることです。 これはメモリ不足状態の最も一般的なケースであるため、範囲を増やしても意味がないかもしれません。

<a name="maxbranches"></a>
## <a name="maxbranches"></a>MaxBranches

1 回の実行パスで実行できる分岐の最大数。

この探索の範囲の背後にある意図は、IntelliTest が[入力生成](input-generation.md)中に探索する実行パスの長さを制限することです。 特に、プログラムが無限ループに入った場合に、IntelliTest が応答しなくなることを防ぎます。

実行および監視されるコードの各条件付き分岐および無条件分岐がこの上限に達するまでカウントされます。これには、パラメーター化されたテストの入力に依存しない分岐が含まれます。

たとえば、次のコードでは約 100 の分岐を使用します。

```csharp
for (int i=0; i<100; i++) { }
```

<a name="maxcalls"></a>
## <a name="maxcalls"></a>MaxCalls

1 回の実行パス中に実行できる呼び出しの最大数。

この探索の範囲の背後にある意図は、IntelliTest が[入力生成](input-generation.md)中に探索する実行パスの長さを制限することです。 特に、プログラムがメソッドを無限に再帰的に呼び出した (IntelliTest が回復できないスタック オーバーフローが発生することになる) 場合に、IntelliTest が応答しなくなることを防ぎます。

実行および監視されるコードの各呼び出し (直接、間接、仮想、ジャンプ) がこの上限に達するまでカウントされます。

<a name="maxstack"></a>
## <a name="maxstack"></a>MaxStack

1 回の実行パス中の任意の時点でのスタックの最大サイズ。アクティブな呼び出しフレームの数で測定されます。

この探索の範囲の背後にある意図は、IntelliTest が[入力生成](input-generation.md)中に探索する実行パスのスタックのサイズを制限することです。 特に、使用可能なスタック領域をすべて使用する (IntelliTest が回復できないスタック オーバーフローが発生することになる) ことを防ぎます。

<a name="maxconditions"></a>
## <a name="maxconditions"></a>MaxConditions

1 回の実行パス中に確認できる入力に対する条件の最大数。

この探索の範囲の背後にある意図は、IntelliTest が[入力生成](input-generation.md)中に探索する実行パスの複雑さを制限することです。 パラメーター化されたテストの入力に依存している各条件付き分岐が、この上限に達するまでカウントされます。

たとえば、次のコード内の各パスは、n+1 条件を使用します。

```csharp
[PexMethod]
void ParameterizedTest(int n)
{
     for (int i=0; i<n; i++) { // conditions are "0<n", "1<n", ..., "!(n<n)"
          ...
     }
     for (int i=0; i<100; i++) { // irrelevant for MaxConditions, since conditions do not depend on input
          ...
     }
}
```

<a name="maxruns"></a>
## <a name="maxruns"></a>MaxRuns

IntelliTest がテストの探索中に試行する実行の最大数。

この探索の範囲の背後にある意図は、ループまたは再帰を含むコードには無限の実行パスが存在する場合があるため、IntelliTest を[入力生成](input-generation.md)中に制限する必要があることです。

**MaxRuns** と **MaxRunsWithUniquePaths** の 2 つの設定は次のように関連します。

* IntelliTest は、さまざまなテスト入力で **MaxRuns** の最大回数までパラメーター化されたテスト メソッドを呼び出します。
* 実行されるコードが明確な場合、IntelliTest は毎回、異なる実行パスを使用します。 ただし、一部の条件下では、さまざまな入力で、実行されるコードが既に使用されている実行パスに従う場合があります。
* IntelliTest は、一意の実行パスの検出数をカウントします。この数は、**MaxRunsWithUniquePaths** オプションで制限されます。

<a name="maxrunswithoutnewtests"></a>
## <a name="maxrunswithoutnewtests"></a>MaxRunsWithoutNewTests

新しいテストが生成されずに連続する実行の最大数。

多くの場合、IntelliTest は短時間で多数の対象のテスト入力を検出できますが、しばらくすると、新しいテスト入力を検索せず、単体テストを生成しなくなります。 この構成オプションは、IntelliTest が新しいテストを生成せずに実行できる連続試行の数を制限するものです。 これに達すると、探索が停止します。

<a name="maxrunswithuniquepaths"></a>
## <a name="maxrunswithuniquepaths"></a>MaxRunsWithUniquePaths

IntelliTest が探索中に考慮する一意のパスの最大数。

この探索の範囲の背後にある意図は、ループまたは再帰を含むコードには無限の実行パスが存在する場合があるため、IntelliTest を[入力生成](input-generation.md)中に制限する必要があることです。

**MaxRuns** と **MaxRunsWithUniquePaths** の 2 つの設定は次のように関連します。

* IntelliTest は、さまざまなテスト入力で **MaxRuns** の最大回数までパラメーター化されたテスト メソッドを呼び出します。
* 実行されるコードが明確な場合、IntelliTest は毎回、異なる実行パスを使用します。 ただし、一部の条件下では、さまざまな入力で、実行されるコードが既に使用されている実行パスに従う場合があります。
* IntelliTest は、一意の実行パスの検出数をカウントします。この数は、**MaxRunsWithUniquePaths** オプションで制限されます。

<a name="maxexceptions"></a>
## <a name="maxexceptions"></a>MaxExceptions

探索が停止する前に検出できる例外の最大数。

この探索の範囲の背後にある意図は、多くのバグを含むコードの探索を停止することです。 IntelliTest がコードで検出したエラーが多すぎる場合、探索は停止します。

<a name="testexcludepathboundsexceeded"></a>
## <a name="testexcludepathboundsexceeded"></a>TestExcludePathBoundsExceeded

構成されたパスの範囲の [MaxCalls](#maxcalls)、[MaxBranches](#maxbranches)、[MaxStack](#maxstack)、および [MaxConditions](#maxconditions) を超える実行パスは無視されます。

この探索の範囲の背後にある意図は、(多くの場合) 終了しないテストを処理することです。 IntelliTest は、[MaxCalls](#maxcalls)、[MaxBranches](#maxbranches)、[MaxStack](#maxstack)、または [MaxConditions](#maxconditions) などの探索の範囲に達すると、テストは終了しないプロセスではなく、後でスタック オーバーフローが発生することはないと判断します。 このようなテスト ケースは他のテスト フレームワークでの問題を発生させる可能性があります。この属性は、終了しないプロセスまたはテスト ケースが原因でスタック オーバーフローが発生する可能性がある場合に、IntelliTest がテスト ケースを生成しないようにします。

<a name="testemissionfilter"></a>
## <a name="testemissionfilter"></a>TestEmissionFilter

IntelliTest が生成する必要があるテストの種類を示します。 次の値を指定できます。

* **すべて** - 想定の違反を含む、すべての場合にテストを生成します。
* **FailuresAndIncreasedBranchHits** (既定) - すべての固有エラーの場合、また、[TestEmissionBranchHits](#testemissionbranchhits) で制御される、テスト ケースのカバレッジが増えるたびにテストを生成します。
* **FailuresAndUniquePaths** - IntelliTest が検出したすべてのエラーの場合、また、実行パスが一意となるテスト入力ごとにテストを生成します。
* **Failures** - エラーの場合にのみテストを生成します。

<a name="testemissionbranchhits"></a>
## <a name="testemissionbranchhits"></a>TestEmissionBranchHits

現在の [TestEmissionFilter](#testemissionfilter) の設定に応じて、IntelliTest は、以前はカバーされていなかった、プログラムの分岐をカバーする場合に新しいテスト ケースを生成します。

**TestEmissionBranchHits** 設定により、IntelliTest が、分岐がすべてカバーされた (**TestEmissionBranchHits=1**) かどうかや、テストで 1 回または 2 回カバーされた (**TestEmissionBranchHits=2**) かどうかなどを考慮する必要があるかどうかが決まります。

**TestEmissionBranchHits=1** の場合、IntelliTest が到達する可能性のあるすべての分岐をカバーする非常に小さなテスト スイートが生成されます。 特に、このテスト スイートでは、到達したすべての基本的なブロックとステートメントもカバーします。

このオプションの既定値は **TestEmissionBranchHits=2** で、今後の回帰エラーの検出にもより適している、表現力の高いテスト スイートが生成されます。

## <a name="got-feedback"></a>フィードバックが欲しい場合

ご意見や機能に関するご要望を[開発者コミュニティ](https://aka.ms/feedback/suggest?space=8)で投稿してください。
