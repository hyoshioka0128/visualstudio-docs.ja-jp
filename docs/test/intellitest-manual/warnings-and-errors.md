---
title: 警告とエラー | Microsoft IntelliTest 開発者テスト ツール
ms.date: 05/02/2017
ms.topic: reference
helpviewer_keywords:
- IntelliTest, Warnings and errors
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
author: mikejo5000
ms.openlocfilehash: b948aa83d5055fdf3d628a84002881eba9c91ac2
ms.sourcegitcommit: f3f668ecaf11b4c2738ebc91923c6b5e38e74670
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/16/2020
ms.locfileid: "76112528"
---
# <a name="warnings-and-errors"></a>警告とエラー

## <a name="warnings-and-errors-by-category"></a>カテゴリ別の警告とエラー

* **境界**
  * [MaxBranches を超えました](#maxbranches-exceeded)
  * [MaxConstraintSolverTime を超えました](#maxconstraintsolvertime-exceeded)
  * [MaxConditions を超えました](#maxconditions-exceeded)
  * [MaxCalls を超えました](#maxcalls-exceeded)
  * [MaxStack を超えました](#maxstack-exceeded)
  * [MaxRuns を超えました](#maxruns-exceeded)
  * [MaxRunsWithoutNewTests を超えました](#maxrunswithoutnewtests-exceeded)

* **制約の解決**
  * [ソリューションを具体化できません](#cannot-concretize-solution)

* **ドメイン**
  * [オブジェクトを構築するための情報を指定してください](#help-construct)
  * [型を見つけるための情報を指定してください](#help-types)
  * [使用可能な型を推測しました](#usable-type-guessed)

* **実行**
  * [探索中に予期しないエラーが発生しました](#unexpected-exploration)
  * [TargetInvocationException](#targetinvocationexception)

* **インストルメンテーション**
  * [インストルメント化されていないメソッドが呼び出されました](#uninstrumented-method-called)
  * [外部メソッドが呼び出されました](#external-method-called)
  * [インストルメント不能なメソッドが呼び出されました](#uninstrumentable-method-called)
  * [テストの容易性の問題](#testability-issue)
  * [制限](#limitation)

* **インタープリター**
  * [観察された呼び出しが一致しません](#observed-call-mismatch)
  * [静的フィールドに格納された値](#value-static-field)

<a name="maxbranches-exceeded"></a>
## <a name="maxbranches-exceeded"></a>MaxBranches を超えました

IntelliTest は、[入力生成](input-generation.md)中に探索する実行パスの長さを制限します。 この機能により、プログラムが無限ループに入ったときに、IntelliTest が応答しなくなることを防止します。

実行および監視されるコードのすべての条件付き分岐および無条件分岐がこの上限に達するまでカウントされます。これには、[パラメーター化された単体テスト](test-generation.md#parameterized-unit-testing)の入力に依存しない分岐が含まれます。

たとえば、次のコードは、約 100 の分岐を使用します。

```csharp
for (int i=0; i<100; i++) { }
```

[PexClass](attribute-glossary.md#pexclass) や [PexMethod](attribute-glossary.md#pexmethod) などの **PexSettingsAttributeBase** から派生した属性の **MaxBranches** オプションを編集することができます。 次の例では、この上限は実質的になくなります。

```csharp
[PexMethod(MaxBranches=int.MaxValue)]
public void MyTest(...) {
    // ....
}
```

**TestExcludePathBoundsExceeded** オプションを設定し、これらの問題に対処する通常の方法を IntelliTest に通知することもできます。

テスト コードでは、[PexSymbolicValue](static-helper-classes.md#pexsymbolicvalue) を使用して、ループ条件によって生成される制約を無視することができます。

```csharp
for (int i=0;
    PexSymbolicValue.Ignore(i<100); // IntelliTest will 'forget' about this path condition
    i++)
{ }
```

<a name="maxconstraintsolvertime-exceeded"></a>
## <a name="maxconstraintsolvertime-exceeded"></a>MaxConstraintSolverTime を超えました

IntelliTest は、[制約ソルバー](input-generation.md#constraint-solver)を使用して、新しいテスト入力を計算します。 制約の解決は非常に時間がかかるプロセスになることがあるので、IntelliTest では、制約 (特に **MaxConstraintSolverTime**) を構成することができます。

多くのアプリケーションでは、タイムアウト時間を大幅に増やしても、カバレッジは向上しません。 この理由は、解決方法がない制約システムが原因でほとんどのタイムアウトが発生するためです。 ただし、IntelliTest は、すべての考えられる解決策を試さないと、これが矛盾していると判断できないことがあり、そのためにタイムアウトになります。

<a name="maxconditions-exceeded"></a>
## <a name="maxconditions-exceeded"></a>MaxConditions を超えました

IntelliTest は、[入力生成](input-generation.md)中に探索する実行パスの長さを制限します。 この機能により、プログラムが無限ループに入ったときに、IntelliTest が応答しなくなることを防止します。

[パラメーター化された単体テスト](test-generation.md#parameterized-unit-testing)の入力に依存している各条件付き分岐が、この上限に達するまでカウントされます。

たとえば、次のコード内の各パスは、**n+1** 条件を使用します。

```csharp
[PexMethod]
void ParameterizedTest(int n) {
    // conditions are "0<n", "1<n", ..., "!(n<n)"
    for (int i=0; i<n; i++)
    { ... }

    // irrelevant for MaxConditions, since conditions do not depend on input
    for (int i=0; i<100; i++)
    { ... }
}
```

[PexClass](attribute-glossary.md#pexclass) や [PexMethod](attribute-glossary.md#pexmethod) などの **PexSettingsAttributeBase** から派生した属性の **MaxConditions** オプションを編集することができます。 次に例を示します。

```csharp
[PexMethod(MaxConditions=10000)]
void ParameterizedTest(int n) {
    // ...
}
```

**TestExcludePathBoundsExceeded** オプションを設定し、これらの問題に対処する通常の方法を IntelliTest に通知することもできます。

[PexSymbolicValue](static-helper-classes.md#pexsymbolicvalue) を使用して、ループ条件によって生成される制約を無視することができます。

```csharp
[PexMethod]
void ParameterizedTest(int n) {
    int nshadow = PexSymbolicValue.Ignore(n); // IntelliTest looses track of 'n'

    // irrevelant for MaxConditions, since nshadow is not related to input
    for (int i=0; i<nshadow; i++)
    {...}
}
```

<a name="maxcalls-exceeded"></a>
## <a name="maxcalls-exceeded"></a>MaxCalls を超えました

IntelliTest は、[入力生成](input-generation.md)中に探索する実行パスの長さを制限します。 この機能により、プログラムが無限ループに入ったときに、IntelliTest が応答しなくなることを防止します。

実行および監視されるコードの各呼び出し (直接、間接、仮想、またはジャンプ) がこの上限に達するまでカウントされます。

[PexClass](attribute-glossary.md#pexclass) や [PexMethod](attribute-glossary.md#pexmethod) などの **PexSettingsAttributeBase** から派生した属性の **MaxCalls** オプションを編集することができます。 次の例では、この上限は実質的になくなります。

```csharp
[PexMethod(MaxCalls=int.MaxValue)]
public void MyTest(...) {
    // ....
}
```

**TestExcludePathBoundsExceeded** オプションを設定し、これらの問題に対処する通常の方法を IntelliTest に通知することもできます。

<a name="maxstack-exceeded"></a>
## <a name="maxstack-exceeded"></a>MaxStack を超えました

IntelliTest は、[入力生成](input-generation.md)中に探索する実行パスの呼び出し履歴のサイズを制限します。 この機能により、スタック オーバーフローが発生したときに IntelliTest が終了することを防止します。

[PexClass](attribute-glossary.md#pexclass) や [PexMethod](attribute-glossary.md#pexmethod) などの **PexSettingsAttributeBase** から派生した属性の **MaxStack** オプションを編集することができます。 次の例では、この上限は実質的になくなります (推奨されません)。

```csharp
[PexMethod(MaxStack=int.MaxValue)]
public void MyTest(...) {
    // ....
}
```

**TestExcludePathBoundsExceeded** オプションを設定し、これらの問題に対処する通常の方法を IntelliTest に通知することもできます。

<a name="maxruns-exceeded"></a>
## <a name="maxruns-exceeded"></a>MaxRuns を超えました

IntelliTest は、[入力生成](input-generation.md)中に探索する実行パスの数を制限します。 この機能により、プログラムにループまたは再帰があるときに、IntelliTest を終了します。

IntelliTest が特定の入力を持つパラメーター化されたテストを実行するたびに新しいテストケースを発行するとは限りません。 詳細については、[TestEmissionFilter](exploration-bounds.md#testemissionfilter) を参照してください。

[PexClass](attribute-glossary.md#pexclass) や [PexMethod](attribute-glossary.md#pexmethod) などの **PexSettingsAttributeBase** から派生した属性の **MaxRuns** オプションを編集することができます。 次の例では、この上限は実質的になくなります (推奨されません)。

```csharp
[PexMethod(MaxRuns=2000)]
public void MyTest(...) {
    // ....
}
```

<a name="maxrunswithoutnewtests-exceeded"></a>
## <a name="maxrunswithoutnewtests-exceeded"></a>MaxRunsWithoutNewTests を超えました

IntelliTest は、[入力生成](input-generation.md)中に探索する実行パスの数を制限します。 この機能により、プログラムにループまたは再帰があるときに、IntelliTest を終了します。

IntelliTest が特定の入力を持つパラメーター化されたテストを実行するたびに新しいテストケースを発行するとは限りません。 詳細については、[TestEmissionFilter](exploration-bounds.md#testemissionfilter) を参照してください。

IntelliTest は多くの場合、多くの興味深いテスト入力を最初に検出しますが、しばらくすると、テストを発行しなくなる場合があります。 このオプションは、別の関連するテスト入力を見つけるための再試行を IntelliTest で続ける時間の長さを制御します。

[PexClass](attribute-glossary.md#pexclass) や [PexMethod](attribute-glossary.md#pexmethod) などの **PexSettingsAttributeBase** から派生した属性の **MaxRunsWithoutNewTests** オプションを編集することができます。 次の例では、この上限は実質的になくなります (推奨されません)。

```csharp
[PexMethod(MaxRunsWithoutNewTests=2000)]
public void MyTest(...) {
    // ....
}
```

<a name="cannot-concretize-solution"></a>
## <a name="cannot-concretize-solution"></a>ソリューションを具体化できません

多くの場合、このエラーは前のエラーの結果です。 IntelliTest は、[制約ソルバー](input-generation.md#constraint-solver)を使用して、新しいテスト入力を判断します。 場合によっては、[制約ソルバー](input-generation.md#constraint-solver)によって提案されたテスト入力が無効なことがあります。 これは次の場合に発生します。

* 特定の制約が認識されていない。
* 値がユーザー定義の方法で作成され、そのためにユーザーコードでエラーが発生する。
* 含まれているいくつかの型の方に IntelliTest で制御されない初期化ロジック (たとえば、COM クラス) がある。

<a name="help-construct"></a>
## <a name="need-help-to-construct-object"></a>オブジェクトを構築するための情報を指定してください

IntelliTest は、[テスト入力を生成し](input-generation.md)、いくつかの入力がフィールドを持つオブジェクトである場合があります。
この場合、IntelliTest は、プライベート フィールドを持つクラスのインスタンスを生成しようとし、このプライベート フィールドに特定の値がある場合に興味深いプログラム動作が発生すると仮定します。

しかし、これはリフレクションを使用して実行可能ですが、IntelliTest は任意のフィールドの値を持つオブジェクトを生成しません。
代わりに、このような場合は、オブジェクトを作成するためのクラスのパブリック メソッドの使用方法に関するヒントをユーザーが提供することに依存し、プライベート フィールドに目的の値がある状態にします。

IntelliTest で興味深いオブジェクトを構築できるようにする方法については、「[既存のクラスのインスタンス化](input-generation.md#existing-classes)」を参照してください。

<a name="help-types"></a>
## <a name="need-help-to-find-types"></a>型を見つけるための情報を指定してください

IntelliTest は、すべての .NET 型の[テスト入力を生成します](input-generation.md)。 ここでは、IntelliTest は、抽象クラスから派生するか抽象インターフェイスを実装するインスタンスを作成しようとしますが、IntelliTest は制約を満たす型を知りません。

制約に一致する 1 つまたは複数の型をポイントして IntelliTest を補助することができます。 通常は、次のいずれかの属性が役に立ちます。

* 特定の型をポイントする **PexUseTypeAttribute**。

  たとえば、IntelliTest が "**System.Collections.IDictionary** に割り当てることができる型を知らない" ことを報告した場合、次の **PexUseTypeAttribute** をテスト (またはフィクスチャ クラス) に添付することで補助できます。

  ```csharp
  [PexMethod]
  [PexUseType(typeof(System.Collections.Hashtable))]
  public void MyTest(IDictionary[] dictionaries) { ... }
  ```

* **アセンブリ レベル属性**

  ```csharp
  [assembly: PexUseType(typeof(System.Collections.Hashtable))]
  ```

<a name="usable-type-guessed"></a>
## <a name="usable-type-guessed"></a>使用可能な型を推測しました

IntelliTest は、すべての .NET 型の[テスト入力を生成します](input-generation.md)。 型が抽象またはインターフェイスの場合、IntelliTest は、その型の特定の実装を選択する必要があります。 選択を行うには、どの型が存在するかを知る必要があります。

この警告が表示されたときには、IntelliTest が、いくつかの参照先アセンブリを参照して実装の型を見つけたにもかかわらず、その型を使用するかどうかを確認できないか、別の場所により適切な使用可能な型があることを示しています。 IntelliTest は、単に有望と思われる型を選択しました。

この警告を回避するために、IntelliTest の型の選択をそのまま使用するか、対応する [PexUseType](attribute-glossary.md#pexusetype) を追加することによっての他の型を使用するように IntelliTest を補助します。

<a name="unexpected-exploration"></a>
## <a name="unexpected-failure-during-exploration"></a>探索中に予期しないエラーが発生しました

テストの探索中に予期しない例外が検出されました。

[バグとして報告](#report-bug)してください。

<a name="targetinvocationexception"></a>
## <a name="targetinvocationexception"></a>TargetInvocationException

ユーザー コードで例外が発生しました。 スタック トレースを調べ、コードのバグをなくします。

<a name="uninstrumented-method-called"></a>
## <a name="uninstrumented-method-called"></a>インストルメント化されていないメソッドが呼び出されました

IntelliTest は、プログラムの実行を監視することによって[テスト入力を生成します](input-generation.md)。 IntelliTest が動作を監視できるように、関連するコードが正しくインストルメント化されることが重要です。

この警告は、インストルメント化されたコードが、インストルメントされていない別のアセンブリ内のメソッドを呼び出したときに表示されます。
両方の相互作用を IntelliTest で調査する場合、別のアセンブリ (またはその一部) もインストルメント化する必要があります。

<a name="external-method-called"></a>
## <a name="external-method-called"></a>外部メソッドが呼び出されました

IntelliTest は、.NET アプリケーションの実行を監視することによって[テスト入力を生成します](input-generation.md)。
IntelliTest は、.NET 言語で記述されていないコードに関して意味のあるテスト入力を生成できません。

この警告は、インストルメント化されたコードが、IntelliTest が分析できないアンマネージドのネイティブ メソッドを呼び出したときに表示されます。 両方の相互作用を IntelliTest で調査する場合、アンマネージド メソッドを模擬表示する必要があります。

<a name="uninstrumentable-method-called"></a>
## <a name="uninstrumentable-method-called"></a>インストルメント不能なメソッドが呼び出されました

IntelliTest は、.NET アプリケーションの実行を監視することによって[テスト入力を生成します](input-generation.md)。 ただし、技術的な理由により、IntelliTest で監視できないいくつかのメソッドがあります。 たとえば、IntelliTest は、静的コンストラクターを監視できません。

この警告は、インストルメント化されたコードが、IntelliTest が監視できないメソッドを呼び出したときに表示されます。

<a name="testability-issue"></a>
## <a name="testability-issue"></a>テストの容易性の問題

IntelliTest は、プログラムの実行を監視することによって[テスト入力を生成します](input-generation.md)。 IntelliTest は、プログラムが確定的で、関連する動作がテスト入力によって制御されている場合のみ、関連するテスト入力を生成できます。

この警告は、テスト ケースの実行中に、非確定的に動作するか環境と対話するメソッドが呼び出されたために表示されます。 例として、メソッド **System.Random** や **System.IO.File** があります。 IntelliTest で意味のあるテスト入力を作成する場合は、IntelliTest でテストの容易性の問題としてフラグを付けられたメソッドを模擬表示する必要があります。

<a name="limitation"></a>
## <a name="limitation"></a>制限

IntelliTest は、[制約ソルバー](input-generation.md#constraint-solver)を使用して[テスト入力を生成します](input-generation.md)。
ただし、[制約ソルバー](input-generation.md#constraint-solver)の範囲を超えているいくつかの操作があります。
現在次の操作が含まれます。

* ほとんどの浮動小数点操作 (浮動小数点数についてはいくつかの線形算術のみがサポートされます)。
* 浮動小数点と整数の間の変換
* **System.Decimal** 型のすべての操作

この警告は、実行されたコードが、IntelliTest で解釈できない操作を実行するかそのようなメソッドを呼び出したときに表示されます。

<a name="observed-call-mismatch"></a>
## <a name="observed-call-mismatch"></a>観察された呼び出しが一致しません

IntelliTest は、プログラムの実行を監視することによって[テスト入力を生成します](input-generation.md)。 ただし、IntelliTest がすべての命令を監視できないことがあります。 たとえば、ネイティブ コードを監視できず、インストルメント化されていないコードも監視できません。

IntelliTest は、コードを監視できないときには、そのコードに関連するテスト入力を生成できません。
多くの場合、そのメソッドの呼び出しが戻されるまで、IntelliTest はメソッドを監視できないという事実を認識しません。 ただし、この警告には以下のような原因があります。

* IntelliTest が、インストルメントされていないメソッドの呼び出しを開始する一部のコードを監視した。
* インストルメントされていないメソッドがインストルメント化されているメソッドを呼び出した。
* IntelliTest が、呼び出されたインストルメント化されたメソッドを監視している。

IntelliTest は、インストルメントされていない中間メソッドが実行した処理を知らないので、入れ子になったインストルメント化された呼び出しに関連するテスト入力を生成できない場合があります。

<a name="value-static-field"></a>
## <a name="value-stored-in-static-field"></a>静的フィールドに格納された値

IntelliTest は、単体テストが確定的である場合のみ (言い換えると同じテスト入力に対して常に同様に動作する場合のみ)、[関連するテスト入力](input-generation.md)を体系的に判断できます。 具体的には、テストを再実行できる状態のままでテストがシステムを出る必要があることを意味します。
理想的には、単体テストでグローバル状態は変更せず、グローバルとすべてのやり取りを疑似表示する必要があります。

この警告は、静的フィールドが変更され、テストの動作が非確定的になる場合があることを示します。

次の状況では、静的フィールドの変更が許容されます。

* テストの入力のために、セットアップやクリーンアップのコードが変更を元に戻す場合
* フィールドが 1 回だけ開始され、値がその後に変更されない場合

<a name="report-bug"></a>

## <a name="got-feedback"></a>フィードバックをお寄せください

ご意見や機能に関するご要望を[開発者コミュニティ](https://developercommunity.visualstudio.com/content/idea/post.html?space=8)で投稿してください。
