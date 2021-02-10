---
title: テスト生成 | Microsoft IntelliTest 開発者テスト ツール
description: IntelliTest が実装のメソッドからテスト ケースをどのようにして生成し、メソッドの入力を生成し、データに対するアサーションを確認するかについて説明します。
ms.custom: SEO-VS-2020
ms.date: 05/02/2017
ms.topic: conceptual
helpviewer_keywords:
- IntelliTest, Test generation
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
author: mikejo5000
ms.openlocfilehash: 92071a3bdaf32f06a77f8502b251f1f3af019203
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99899525"
---
# <a name="test-generation"></a>テスト生成

従来の単体テストでは、テストは以下のいくつかの要素で構成されます。

* [メソッド呼び出しのシーケンス](test-generation.md#test-generators)
* メソッドを呼び出す引数。引数は[テスト入力](input-generation.md)です。
* 一連の[アサート](#assumptions-and-assertions) ステートメントにより、テストされるアプリケーションで本来意図されている動作の検証

テスト構造の例を以下に示します。

```csharp
[Test]
void MyTest() {
    // data
    ArrayList a = new ArrayList();

    // method sequence
    a.Add(5);

    // assertions
    Assert.IsTrue(a.Count==1);
    Assert.AreEqual(a[0], 5);
}
```

IntelliTest は多くの場合、より一般的な[パラメーター化された単体テスト](#parameterized-unit-testing)の関連引数値を自動的に決定できます。パラメーター化された単体テストは、メソッド呼び出しとアサートのシーケンスを提供します。

<a name="test-generators"></a>
## <a name="test-generators"></a>テスト ジェネレーター

IntelliTest はテスト ケースを生成します。実行するテストの下で実装のメソッド シーケンスを選択し、メソッドの入力を生成し、同時に派生データのアサートを確認します。

[パラメーター化された単体テスト](#parameterized-unit-testing)は直接、その本体でメソッドのシーケンスを明言します。

IntelliTest がオブジェクトを構築する必要がある場合、必要に応じて、シーケンスにコンストラクターとファクトリ メソッドの呼び出しが自動的に追加されます。

<a name="parameterized-unit-testing"></a>
## <a name="parameterized-unit-testing"></a>パラメーター化された単体テスト

*パラメーター化された単体テスト* (PUT) は、パラメーターを受け取るテストです。 通常は排他的な手法である従来の単体テストとは異なり、PUT はあらゆるパラメーター セットを受け取ります。 そんなに簡単なのでしょうか。 はい。次に IntelliTest は、テストから到達できるコードを[完全にカバー](input-generation.md#dynamic-code-coverage)する [(最小の) 入力セットを生成](input-generation.md)します。

PUT は、MSTest (または NUnit、xUnit) と同様に、[PexMethod](attribute-glossary.md#pexmethod) カスタム属性を利用して定義されます。 PUT は、[PexClass](attribute-glossary.md#pexclass) でタグ付けされるクラスで論理的にグループ化されるインスタンス メソッドです。 次は **MyPexTest** クラスに保存されている単純な PUT の例です。

```csharp
[PexMethod]
void ReplaceFirstChar(string target, char c) {

    string result = StringHelper.ReplaceFirstChar(target, c);

    Assert.AreEqual(result[0], c);
}
```

**ReplaceFirstChar** は、文字列の最初の文字を置換するメソッドです。

```csharp
class StringHelper {
    static string ReplaceFirstChar(string target, char c) {
        if (target == null) throw new ArgumentNullException();
        if (target.Length == 0) throw new ArgumentOutOfRangeException();
        return c + target.Substring(1);
    }
}
```

このテストから、IntelliTest は、テストされるコードのたくさんの実行パスをカバーする PUT の[入力を自動的に生成](input-generation.md)できます。 異なる実行パスをカバーする各入力が単体テストとして "シリアル化" されます。

```csharp
[TestMethod, ExpectedException(typeof(ArgumentNullException))]
void ReplaceFirstChar0() {
    this.ReplaceFirstChar(null, 0);
}
...
[TestMethod]
void ReplaceFirstChar10() {
    this.ReplaceFirstChar("a", 'c');
}
```

<a name="generic-parameterized"></a>
## <a name="generic-parameterized-unit-testing"></a>ジェネリックなパラメーター化単体テスト

パラメーター化された単体テストはジェネリック メソッドにすることができます。 その場合、[PexGenericArguments](attribute-glossary.md#pexgenericarguments) を利用し、メソッドのインスタンス化に使用する種類を指定する必要があります。

```csharp
[PexClass]
public partial class ListTest {
    [PexMethod]
    [PexGenericArguments(typeof(int))]
    [PexGenericArguments(typeof(object))]
    public void AddItem<T>(List<T> list, T value)
    { ... }
}
```

<a name="allowing-exceptions"></a>
## <a name="allowing-exceptions"></a>例外を許可する

IntelliTest は、予想される例外と予想外の例外に例外を選別するさまざまな検証属性を提供します。

予想される例外の場合、ネガティブなテスト ケースが生成され、**ExpectedException(typeof(*xxx*))** のような注釈が付けられます。予想外の例外の場合、失敗のテスト ケースが生成されます。

```csharp
[PexMethod, PexAllowedException(typeof(ArgumentNullException))]
void SomeTest() {...}
```

検証コントロール:

* [PexAllowedException](attribute-glossary.md#pexallowedexception): 場所を問わず、特定の例外タイプを許可します
* [PexAllowedExceptionFromAssembly](attribute-glossary.md#pexallowedexceptionfromassembly): 指定したアセンブリの特定の例外タイプを許可します
* [PexAllowedExceptionFromType](attribute-glossary.md#pexallowedexceptionfromtype): 特定の種類の特定の例外タイプを許可します
* [PexAllowedExceptionFromTypeUnderTest](attribute-glossary.md#pexallowedexceptionfromtypeundertest): テストされている種類の特定の例外タイプを許可します

<a name="internal-types"></a>
## <a name="testing-internal-types"></a>内部型をテストする

IntelliTest は認識可能な内部型を "テスト" できます。 IntelliTest が型を認識するには、Visual Studio IntelliTest ウィザードを利用し、製品またはテスト製品に次の属性を追加します。

```csharp
[assembly: InternalsVisibleTo("Microsoft.Pex, PublicKey=002400000480000094000000060200000024000052534131000400000100010007d1fa57c4aed9f0a32e84aa0faefd0de9e8fd6aec8f87fb03766c834c99921eb23be79ad9d5dcc1dd9ad236132102900b723cf980957fc4e177108fc607774f29e8320e92ea05ece4e821c0a5efe8f1645c4c0c93c1ab99285d622caa652c1dfad63d745d6f2de5f17e5eaf0fc4963d261c8a12436518206dc093344d5ad293")]
```

<a name="assumptions-and-assertions"></a>
## <a name="assumptions-and-assertions"></a>前提事項とアサーション

前提事項とアサーションを利用し、テストの[前提条件](#precondition) (前提事項) と[事後条件](#postcondition) (アサーション) を表現できます。 IntelliTest がパラメーター値のセットを生成し、コードを "調べる" とき、テストの前提事項に違反することがあります。 その場合、そのパスのテストは生成されず、メッセージなしで無視されます。

アサーションは、通常の単体テスト フレームワークでよく知られた概念です。IntelliTest は、サポートされている各テスト フレームワークにより提供される組み込み **Assert** クラスを既に "理解" しています。 ただし、ほとんどのフレームワークで **Assume** クラスは提供されません。 Assume クラスが提供されない場合、IntelliTest は [PexAssume](static-helper-classes.md#pexassume) クラスを提供します。 既存のテスト フレームワークを使用しない場合、IntelliTest には [PexAssert](static-helper-classes.md#pexassert) クラスも与えられます。

```csharp
[PexMethod]
public void Test1(object o) {
    // precondition: o should not be null
    PexAssume.IsNotNull(o);

    ...
}
```

具体的には、null を利用しない前提事項をカスタム属性としてエンコードできます。

```csharp
[PexMethod]
public void Test2([PexAssumeNotNull] object o)
// precondition: o should not be null
{
   ...
}
```

<a name="precondition"></a>
## <a name="precondition"></a>Precondition

メソッドの前提条件は、メソッドが成功となるための条件を表します。

通常、パラメーターとオブジェクトの状態を確認し、違反がある場合、**ArgumentException** または **InvalidOperationException** をスローすることで前提条件が強制されます。

IntelliTest では、[パラメーター化された単体テスト](#parameterized-unit-testing)の前提条件は [PexAssume](static-helper-classes.md#pexassume) で表現されます。

<a name="postcondition"></a>
## <a name="postcondition"></a>事後条件

メソッドの事後条件は、メソッドの実行中と実行後に当てはまらなければならない条件を表します。その前に前提条件が有効と見なされたものと想定されます。

通常、事後条件は **Assert** メソッドを呼び出すことで強制されます。

IntelliTest では、[パラメーター化された単体テスト](#parameterized-unit-testing)の事後条件は [PexAssert](static-helper-classes.md#pexassert) で表現されます。

<a name="test-failures"></a>
## <a name="test-failures"></a>テスト不合格
生成されたテスト ケースはどのような場合に不合格となりますか。

1. [構成されたパス バウンド](exploration-bounds.md)内で終了しない場合、[[TestExcludePathBoundsExceeded]](exploration-bounds.md#testexcludepathboundsexceeded) オプションが設定されていない限り、不合格として見なされます。

1. **PexAssumeFailedException** がスローされた場合、テストは合格です。 ただし、[[TestEmissionFilter]](exploration-bounds.md#testemissionfilter) が **[すべて]** に設定されていない限り、通常はフィルターで除外されます。

1. テストが[アサーション](#assumptions-and-assertions)に違反した場合、たとえば、単体テスト フレームワークのアサーション違反例外がスローされた場合、不合格です。

上記のいずれでも判断されない場合、例外がスローされない場合、または、例外がスローされない場合に限り、テストは合格です。 アサート違反は例外と同様に扱われます。

<a name="setup-teardown"></a>
## <a name="setup-and-tear-down"></a>セットアップと破棄

テスト フレームワークとの統合の一環として、IntelliTest はセットアップと破棄のメソッドを検出し、実行できます。

**例**

```csharp
using Microsoft.Pex.Framework;
using NUnit.Framework;

namespace MyTests
{
    [PexClass]
    [TestFixture]
    public partial class MyTestClass
    {
        [SetUp]
        public void Init()
        {
            // monitored
        }

        [PexMethod]
        public void MyTest(int i)
        {
        }

        [TearDown]
        public void Dispose()
        {
            // monitored
        }
    }
}
```

<a name="further-reading"></a>
## <a name="further-reading"></a>参考資料

* [テストとコードのバインディング](https://devblogs.microsoft.com/devops/smart-unit-tests-test-to-code-binding-test-case-management/)
* [1 回のテストですべてのルールを指定する](https://devblogs.microsoft.com/devops/intellitest-one-test-to-rule-them-all/)

## <a name="got-feedback"></a>フィードバックが欲しい場合

ご意見や機能に関するご要望を[開発者コミュニティ](https://aka.ms/feedback/suggest?space=8)で投稿してください。
