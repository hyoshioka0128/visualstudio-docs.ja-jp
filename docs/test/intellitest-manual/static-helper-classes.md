---
title: 静的ヘルパー クラス | Microsoft IntelliTest 開発者テスト ツール
ms.date: 05/02/2017
ms.topic: reference
helpviewer_keywords:
- IntelliTest, Static helper classes
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
author: mikejo5000
ms.openlocfilehash: 5010761213cf79756cf8da3d2fffe60dd0b61efd
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "79306987"
---
# <a name="static-helper-classes"></a>静的ヘルパー クラス

IntelliTest は、[パラメーター化された単体テスト](test-generation.md#parameterized-unit-testing)の作成時に使用できる静的ヘルパー クラスのセットを提供します。

* [PexAssume](#pexassume): 入力に対する前提事項の定義に利用され、不要な入力の除外に役立ちます
* [PexAssert](#pexassert): テスト フレームワークで単純なアサーション クラスが提供されない場合に使用する単純なアサーション クラス
* [PexChoose](#pexchoose): IntelliTest が管理する付加的テスト入力のストリーム
* [PexObserve](#pexobserve): 具体的な値を記録し、任意で、生成されたコードでその値を検証します

一部のクラスでは、IntelliTest 推論エンジンを低いレベルで操作できます。

* [PexSymbolicValue](#pexsymbolicvalue): 変数に対する記号制約を点検または変更するユーティリティ

<a name="pexassume"></a>
## <a name="pexassume"></a>PexAssume

[パラメーター化された単体テスト](test-generation.md#parameterized-unit-testing)の前提 ([前提条件](test-generation.md#precondition)など) を表す静的クラス。 このクラスのメソッドを使用して、望ましくないテスト入力をフィルターで除外することができます。

一部のテスト入力に対して想定される条件が当てはまらない場合、**PexAssumeFailedException** がスローされます。 メッセージなしでテストが無視されます。

**例**

次のパラメーター化されたテストでは **j=0** が考慮されません。

```csharp
public void TestSomething(int i, int j) {
     PexAssume.AreNotEqual(j, 0);
     int k = i/j;
     ...
}
```

**解説**

上のコードは次とほぼ等しくなります。

```csharp
     if (j==0)
          return;
```

不合格の **PexAssume** でテスト ケースが生成されないという点が異なります。 **if** ステートメントの場合、IntelliTest は別個のテスト ケースを生成し、**if** ステートメントの **then** ブランチをカバーします。

**PexAssume** にはまた、文字列、配列、コレクションに対する前提のために特別な入れ子になっているクラスが含まれています。

<a name="pexassert"></a>
## <a name="pexassert"></a>PexAssert

[パラメーター化された単体テスト](test-generation.md#parameterized-unit-testing)のアサーション ([事後条件](test-generation.md#postcondition)など) を表す静的クラス。

あるテスト入力でこのアサートされた条件が有効でない場合は、**PexAssertFailedException** がスローされ、テストが不合格となります。

**例**

次の例では、整数の絶対値が正であることが前提となります。

```csharp
public void TestSomething(int i) {
     int j = Maths.Abs(i);
     PexAssert.IsTrue(j >= 0);
     ...
}
```

<a name="pexchoose"></a>
## <a name="pexchoose"></a>PexChoose

静的クラス。テストに補助入力値を提供し、それを[パラメーター化されたモック](input-generation.md#parameterized-mocks)の実装に使用できます。

**PexChoose** クラスは特定の入力値に対するテストが成功するか失敗するかを判断する場合には有効ではありません。 **PexChoose** は入力値を提供するだけです。この入力値は*選択肢*とも呼ばれています。 入力値の制限、テストに成功または失敗したときに定義するアサーションの書き込みは、ユーザーに任されています。

**操作モード**

**PexChoose** クラスは 2 つのモードで動作します。

* IntelliTest が[入力生成](input-generation.md)中、テストとテストされるコードを記号分析するとき、選択機能により任意の値が返されます。IntelliTest はテストとテストされるコードで各値がどのように使用されるか追跡記録します。 IntelliTest は、テストとテストされるコードでさまざまな実行パスをトリガーする関連値を生成します。

* 特定のテスト ケースに生成されたコードにより、選択肢プロバイダーが特定の方法で設定されます。そのようなテスト ケースを再実行すると、特定の実行パスをトリガーする選択が行われます。

**使用方法**

* **PexChoose.Value** を呼び出し、新しい値を生成します。

```csharp
public int Foo() {
    return PexChoose.Value<int>("foo");
}
```

<a name="pexobserve"></a>
## <a name="pexobserve"></a>PexObserve

名前付き値を記録する静的クラス。

IntelliTest がコードを調べるとき、**PexObserve** により、書式設定された文字列表現を利用し、計算された値が記録されます。 値は一意の名前に関連付けられます。

```csharp
PexObserve.Value<string>("result", result);
```

**例**

```csharp
// product code
public static class MathEx {
     public static int Square(int value) { return value * value; }
}

// fixture
[TestClass]
public partial class MathExTests {
     [PexMethod]
     public int SquareTest(int a) {
        int result = MathEx.Square(a);
        // storing result
        return result;
     }
}
```

<a name="pexsymbolicvalue"></a>
## <a name="pexsymbolicvalue"></a>PexSymbolicValue

パラメーターに対する制約を無視し、値に関連付けられている記号情報を印刷するために使用される静的クラス。

**使用方法**

通常、IntelliTest は、実行中、コードのすべての実行パスをカバーしようとします。 ただし、前提とアサーションの条件を計算するときは特に、すべての可能性を調べるべきではありません。

**例**

これは **PexAssume.Arrays.ElementsAreNotNull** メソッドの実装例です。
このメソッドでは、IntelliTest がさまざまなサイズの配列の生成を試行しないように、配列値の長さに対する制約を無視します。 制約はここだけで無視されます。 配列の長さが異なると、テストされるコードの動作も異なる場合、IntelliTest はテストされるコードの制約とは異なるサイズの配列を生成できません。

```csharp
public static void AreElementsNotNull<T>(T[] value)
    where T : class
{
    PexAssume.NotNull(value);
    // the followings prevents the exploration of all array lengths
    int len = PexSymbolicValue.Ignore<int>(value.Length);

    // building up a boolean value as follows prevents exploration
    // of all combinations of non-null (instead, there are just two cases)
    bool anyNull = false;
    for (int i = 0; i < len; ++i)
        anyNull |= value[i] == null;

    // was any element null?
    if (anyNull)
        PexAssume.Fail("some element of array is a null reference");
}
```

## <a name="got-feedback"></a>フィードバックが欲しい場合

ご意見や機能に関するご要望を[開発者コミュニティ](https://developercommunity.visualstudio.com/content/idea/post.html?space=8)で投稿してください。
