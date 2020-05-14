---
title: テスト駆動型開発のチュートリアル
ms.date: 07/24/2019
ms.topic: conceptual
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
author: mikejo5000
ms.openlocfilehash: a264975014fea88126bbca0589fe037e629dae10
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "75566281"
---
# <a name="walkthrough-test-driven-development-using-test-explorer"></a>チュートリアル: テスト エクスプローラーを使用したテスト駆動開発

単体テストを作成すれば、段階的にコードに変更を加える方法でコードの正しい動作を容易に維持することができます。 サード パーティ製を含めていくつかのフレームワークを単体テストの記述に使用できます。 一部のテスト フレームワークは、別々の言語またはプラットフォームでのテストに特化されています。 テスト エクスプローラーは、1 つのインターフェイスで、どのフレームワークでの単体テストにも対応します。 **テスト エクスプローラー**の詳細については、「[テスト エクスプローラーを使用して単体テストを実行する](run-unit-tests-with-test-explorer.md)」および[テスト エクスプローラーに関する FAQ](test-explorer-faq.md) をご覧ください。

このチュートリアルでは、Microsoft テスト フレームワーク (MSTest) を使用して、テスト済みメソッドを C# で開発する方法を示します。 他の言語にも、NUnit など他のテスト フレームワークにも容易に適合させることができます。 詳細については、「[サードパーティ製の単体テスト フレームワークをインストールする](install-third-party-unit-test-frameworks.md)」をご覧ください。

## <a name="create-a-test-and-generate-code"></a>テストを作成してコードを生成する

1. C# の **[クラス ライブラリ (.NET Standard)]** プロジェクトを作成します。 このプロジェクトには、テストするコードを含めます。 プロジェクトには「**MyMath**」という名前を付けます。

2. 同じソリューションで、新しいプロジェクト **[MSTest テスト プロジェクト (.Net Core)]** を追加します。 このテスト プロジェクトには「**MathTests**」という名前を付けます。

   ![新しいコードとテスト プロジェクト](../test/media/test-driven-development-ide.png)

3. 特定の入力に対して取得される結果を検証するシンプルなテスト メソッドを記述します。 `UnitTest1` クラスに次のコードを追加します。

   ```csharp
   [TestMethod]
   public void BasicRooterTest()
   {
     // Create an instance to test:
     Rooter rooter = new Rooter();
     // Define a test input and output value:
     double expectedResult = 2.0;
     double input = expectedResult * expectedResult;
     // Run the method under test:
     double actualResult = rooter.SquareRoot(input);
     // Verify the result:
     Assert.AreEqual(expectedResult, actualResult, delta: expectedResult / 100);
   }
   ```

4. テスト コードから型を作成します。

   1. `Rooter` にカーソルを置き、電球メニューから **[型 'Rooter' を生成する]**  >  **[新しい型の生成]** の順に選択します。

      ![新しい型のクイック アクションを生成する](media/test-driven-development-generate-new-type.png)

   2. **[型の生成]** ダイアログ ボックスで、 **[プロジェクト]** を **[MyMath]** (クラス ライブラリ プロジェクト) に設定して、 **[OK]** を選択します。

      ![Visual Studio 2019 の [型の生成] ダイアログ ボックス](media/test-driven-development-generate-type-dialog.png)

5. テスト コードからメソッドを生成します。 カーソルを `SquareRoot` に置いて、電球メニューから **Generate method 'Rooter.SquareRoot'** を選択します。

6. 単体テストを実行します。

   1. **テスト エクスプローラー**を開くには、 **[テスト]** メニューで、 **[Windows]**  >  **[テスト エクスプローラー]** の順に選択します。

   2. **テスト エクスプローラー**で、 **[すべて実行]** ボタンを選択してテストを再実行します。

   ソリューションがビルドされ、テストが実行されて失敗します。

7. テストの名前を選択します。

   テストの詳細は、 **[テスト詳細の概要]** ウィンドウに表示されます。

   ![テスト エクスプローラーでの [テスト詳細の概要]](media/test-driven-development-test-detail-summary.png)

8. **[スタック トレース]** の下にあるトップ リンクを選択して、テストが失敗した場所に移動します。

この時点で、テストとスタブが作成されています。テストに合格するには、これらを修正する必要があります。

## <a name="verify-a-code-change"></a>コードの変更を確認する

1. *Class1.cs* ファイルで、`SquareRoot` のコードを改良します。

    ```csharp
    public double SquareRoot(double input)
    {
        return input / 2;
    }
    ```

2. **テスト エクスプローラー**で **[すべて実行]** をクリックします。

   ソリューションがビルドされ、テストが実行されて合格します。

   ![合格したテストを示すテスト エクスプローラー](../test/media/test-driven-development-passed-test.png)

## <a name="extend-the-range-of-inputs"></a>入力の範囲を拡張する

あらゆる場合にコードが動作するという信頼性を強化するには、より広範囲の入力値を試みるテストを追加します。

> [!TIP]
> 合格した既存のテストは変更しないでください。 代わりに、新しいテストを追加します。 既存のテストを変更するのは、ユーザー要件が変更されたときのみに限定します。 このポリシーにより、コードを拡張する作業を行うときに、既存の機能が失われないようにすることができます。

1. 一定範囲の入力値を試みるために、次のテストをテスト クラスに追加します。

    ```csharp
    [TestMethod]
    public void RooterValueRange()
    {
        // Create an instance to test.
        Rooter rooter = new Rooter();

        // Try a range of values.
        for (double expected = 1e-8; expected < 1e+8; expected *= 3.2)
        {
            RooterOneValue(rooter, expected);
        }
    }

    private void RooterOneValue(Rooter rooter, double expectedResult)
    {
        double input = expectedResult * expectedResult;
        double actualResult = rooter.SquareRoot(input);
        Assert.AreEqual(expectedResult, actualResult, delta: expectedResult / 1000);
    }
    ```

2. **テスト エクスプローラー**で **[すべて実行]** をクリックします。

   (最初のテストには今回も合格しますが) 新しいテストには失敗します。 失敗した箇所を確認するには、失敗しているテストを選択し、 **[テスト詳細の概要]** ウィンドウで詳細を確認します。

3. テスト対象のメソッドを調べて、問題点を確認します。 `SquareRoot` コードを次のように変更します。

    ```csharp
    public double SquareRoot(double input)
    {
      double result = input;
      double previousResult = -input;
      while (Math.Abs(previousResult - result) > result / 1000)
      {
        previousResult = result;
        result = result - (result * result - input) / (2 * result);
      }
      return result;
    }
    ```

4. **テスト エクスプローラー**で **[すべて実行]** をクリックします。

   今回は、両方のテストに合格します。

## <a name="add-tests-for-exceptional-cases"></a>例外的なケース用にテストを追加する

1. 負数の入力用に新しいテストを追加します。

    ```csharp
    [TestMethod]
    public void RooterTestNegativeInputx()
    {
        Rooter rooter = new Rooter();
        try
        {
            rooter.SquareRoot(-10);
        }
        catch (System.ArgumentOutOfRangeException)
        {
            return;
        }
        Assert.Fail();
    }
    ```

2. **テスト エクスプローラー**で **[すべて実行]** をクリックします。

   テスト対象のメソッドはループするため、実行を手動で取り消す必要があります。

3. **テスト エクスプローラー**のツールバーの **[キャンセル]** を選択します。

   テストの実行が停止します。

4. メソッドの先頭に次の `if` ステートメントを追加して、`SquareRoot` コードを修正します。

    ```csharp
    public double SquareRoot(double input)
    {
        if (input <= 0.0)
        {
            throw new ArgumentOutOfRangeException();
        }
        ...
    ```

5. **テスト エクスプローラー**で **[すべて実行]** をクリックします。

   すべてのテストに合格します。

## <a name="refactor-the-code-under-test"></a>テスト対象のコードをリファクタリングする

テストを変更せずに、コードをリファクターします。

> [!TIP]
> *リファクタリング*とは、コードのパフォーマンスを高めたり、コードをわかりやすくすることを目的として行う変更です。 コードの動作を変更することを意図しないため、テストは変更されません。
>
> リファクタリングの手順は、機能を拡張する手順とは別に実行することをお勧めします。 テストを変更しないことで、リファクタリング時に誤ってバグが生じる状況を回避できます。

1. `result` メソッドで `SquareRoot` を計算する行を次のように変更します。

    ```csharp
    public double SquareRoot(double input)
    {
        if (input <= 0.0)
        {
            throw new ArgumentOutOfRangeException();
        }

        double result = input;
        double previousResult = -input;
        while (Math.Abs(previousResult - result) > result / 1000)
        {
            previousResult = result;
            result = (result + input / result) / 2;
            //was: result = result - (result * result - input) / (2*result);
        }
        return result;
    }
    ```

2. **[すべて実行]** を選択し、すべてのテストに引き続き合格することを確認します。

   ![3 つのテストに合格したことを示すテスト エクスプローラー](../test/media/test-driven-development-three-passed-tests.png)
