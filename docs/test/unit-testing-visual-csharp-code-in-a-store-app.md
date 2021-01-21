---
title: Visual C# コードの単体テスト
description: UWP アプリで C# クラスの単体テストを作成する方法について説明します。 この記事では、"テスト駆動開発" の例を示します。
ms.custom: SEO-VS-2020
ms.date: 09/27/2019
ms.topic: conceptual
ms.author: mikejo
author: mikejo5000
manager: jillfra
ms.workload:
- uwp
ms.openlocfilehash: 410d5dfefa5980bceabff99d66067987b390a615
ms.sourcegitcommit: 9ce13a961719afbb389fa033fbb1a93bea814aae
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/30/2020
ms.locfileid: "96330083"
---
# <a name="unit-test-c-code"></a>C# コードの単体テスト

この記事では、UWP アプリの C# クラスの単体テストを作成する方法の 1 つについて説明します。

テスト対象のクラスである **Rooter** クラスでは、特定の数値の平方根の推定値を計算する関数を実装します。

この記事では、"*テスト駆動開発*" の例を示します。 この方法ではまず、テスト対象のシステムの特定の動作を検証するテストを作成し、テストに成功するコードを記述します。

## <a name="create-the-solution-and-the-unit-test-project"></a>ソリューションと単体テスト プロジェクトを作成する

1. **[ファイル]** メニューで、 **[新規]**  >  **[プロジェクト]** の順にクリックします。

2. **[空のアプリ (ユニバーサル Windows)]** プロジェクト テンプレートを検索して選択します。

3. プロジェクトに **Maths** という名前を付けます。

4. **ソリューション エクスプローラー** でソリューションを右クリックし、**[追加]** > **[新しいプロジェクト]** を選択します。

5. **[単体テスト アプリ (ユニバーサル Windows)]** プロジェクト テンプレートを検索して選択します。

6. テスト プロジェクトに **RooterTests** と名前を付けます。

## <a name="verify-that-the-tests-run-in-test-explorer"></a>テスト エクスプローラーでテストの実行を確認します。

1. 次のように、*UnitTest.cs* ファイルの **TestMethod1** に何らかのテスト コードを挿入します。

   ```csharp
   [TestMethod]
   public void TestMethod1()
   {
       Assert.AreEqual(0, 0);
   }
   ```

   <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert> クラスには、テスト メソッドで結果を確認するために使用するいくつかの静的メソッドが用意されています。

::: moniker range="vs-2017"

2. **[テスト]** メニューで **[実行]** > **[すべてのテスト]** を選択します。

::: moniker-end

::: moniker range=">=vs-2019"

2. **[テスト]** メニューで **[すべてのテストを実行する]** を選択します。

::: moniker-end

   テスト プロジェクトがビルドされ、実行されます。 これには時間がかかる場合があるので、しばらくお待ちください。 **テスト エクスプローラー** のウィンドウが表示され、テストが **[成功したテスト]** に表示されます。 ウィンドウの下部の **[概要]** ウィンドウに、選択したテストに関する詳細情報が表示されます。

## <a name="add-the-rooter-class-to-the-maths-project"></a>Maths プロジェクトに Rooter クラスを追加します。

1. **ソリューション エクスプローラー** で、**Maths** プロジェクトを右クリックし、**[追加]** > **[クラス]** を選択します。

2. クラス ファイルに *Rooter.cs* という名前を付けます。

3. **Rooter** クラスの *Rooter.cs* ファイルに次のコードを追加します。

   ```csharp
   public Rooter()
   {
   }

   // estimate the square root of a number
   public double SquareRoot(double x)
   {
       return 0.0;
   }
   ```

   **Rooter** クラスで、コンストラクターと **SquareRoot** の推定器メソッドを宣言します。 **SquareRoot** メソッドは、テスト設定の基本的な構造をテストするための必要最小限の実装にすぎません。

4. `public` キーワードを **Rooter** クラスの宣言に追加して、テスト コードからアクセスできるようにします。

   ```csharp
   public class Rooter
   ```

## <a name="add-a-project-reference"></a>プロジェクト参照を追加する

1. RooterTests プロジェクトから Maths アプリに参照を追加します。

    1. **ソリューション エクスプローラー** で、**RooterTests** プロジェクトを右クリックし、**[追加]** > **[参照]** を選択します。

    2. **[参照の追加 - RooterTests]** ダイアログ ボックスの **[ソリューション]** を展開し、**[プロジェクト]** を選択します。 **Maths** プロジェクトを選択します。

        ![Maths プロジェクトへの参照の追加](../test/media/ute_cs_windows_addreference.png)

2. `using` ステートメントを *UnitTest.cs* ファイルに追加します。

    1. *UnitTest.cs* を開きます。

    2. `using Microsoft.VisualStudio.TestTools.UnitTesting;` 行の下に次のコードを追加します。

       ```csharp
       using Maths;
       ```

3. **Rooter** 関数を使用するテストを追加します。 *UnitTest.cs* に次のコードを追加します。

   ```csharp
   [TestMethod]
   public void BasicTest()
   {
       Maths.Rooter rooter = new Rooter();
       double expected = 0.0;
       double actual = rooter.SquareRoot(expected * expected);
       double tolerance = .001;
       Assert.AreEqual(expected, actual, tolerance);
   }
   ```

   新しいテストが **テスト エクスプローラー** の **[テストを実行しない]** ノードに表示されます。

4. "ペイロードに含まれている複数のファイルで同じターゲット パスが指定されています" エラーを回避するには、**ソリューション エクスプローラー** で、**Maths** プロジェクトの下の **[プロパティ]** ノードを展開した後、*Default.rd.xml* ファイルを削除します。

::: moniker range="vs-2017"

6. **テスト エクスプローラー** で **[すべて実行]** をクリックします。

   ソリューションがビルドされ、テストが実行され、成功します。

   ![テスト エクスプローラーの成功した BasicTest](../test/media/ute_cpp_testexplorer_basictest.png)

::: moniker-end

::: moniker range=">=vs-2019"

6. **テスト エクスプローラー** で **[すべてのテストを実行する]** を選択します。

   ソリューションがビルドされ、テストが実行され、成功します。

   ![テスト エクスプローラーの成功した基本テスト](../test/media/vs-2019/test-explorer-uwp-app.png)

::: moniker-end

テストおよびアプリのプロジェクトを設定し、アプリ プロジェクトで関数を呼び出すテストを実行できることを確認しました。 ここで、実際のテストおよびコードの記述を開始できます。

## <a name="iteratively-augment-the-tests-and-make-them-pass"></a>テストを繰り返し増やして成功させる

1. **RangeTest** という名前の新しいテストを追加します。

   ```csharp
   [TestMethod]
   public void RangeTest()
   {
       Rooter rooter = new Rooter();
       for (double v = 1e-6; v < 1e6; v = v * 3.2)
       {
           double expected = v;
           double actual = rooter.SquareRoot(v*v);
           double tolerance = expected/1000;
           Assert.AreEqual(expected, actual, tolerance);
       }
   }
   ```

   > [!TIP]
   > 合格したテスト内容を変更しないことをお勧めします。 代わりに、新しいテストを追加します。

2. **RangeTest** テストを実行し、失敗することを確認します。

   ![RangeTest 失敗](../test/media/ute_cpp_testexplorer_rangetest_fail.png)

   > [!TIP]
   > テストを作成したらすぐに実行して、失敗することを確認します。 これは、絶対に失敗しないテストを記述するという簡単なミスを避けることに役立ちます。

3. 新しいテストが成功するように、テスト対象のコードを増やします。 *Rooter.cs* の **SquareRoot** 関数を次のように変更します。

   ```csharp
   public double SquareRoot(double x)
   {
       double estimate = x;
       double diff = x;
       while (diff > estimate / 1000)
       {
           double previousEstimate = estimate;
           estimate = estimate - (estimate * estimate - x) / (2 * estimate);
           diff = Math.Abs(previousEstimate - estimate);
       }
       return estimate;
   }
   ```

::: moniker range="vs-2017"

4. **テスト エクスプローラー** で **[すべて実行]** をクリックします。

::: moniker-end

::: moniker range=">=vs-2019"

4. **テスト エクスプローラー** で **[すべてのテストを実行する]** を選択します。

::: moniker-end

   3 つのテストはすべて成功しました。

> [!TIP]
> 一度に 1 つのテストを追加してコードを開発します。 各反復処理の後にすべてのテストが合格することを確認します。

## <a name="refactor-the-code"></a>コードをリファクタリングする

このセクションで、アプリとテスト コードの両方をリファクターし、テストを再実行して、まだ成功することを確認します。

### <a name="simplify-the-square-root-estimation"></a>平方根の推定を簡素化する

1. 次のように 1 行のコードを変更することで、**SquareRoot** 関数の中心となる計算を簡素化します。

    ```csharp
    // Old code
    //estimate = estimate - (estimate * estimate - x) / (2 * estimate);

    // New code
    estimate = (estimate + x/estimate) / 2.0;
    ```

2. すべてのテストを実行して、回帰が発生していないことを確認します。 すべて成功するはずです。

> [!TIP]
> 安定した一連の適切な単体テストを実行することで、コードを変更したときにバグが生じていないことを確信できます。

### <a name="eliminate-duplicated-code"></a>重複するコードを削除する

**RangeTest** メソッドでは、<xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert> メソッドに渡される *tolerance* 変数の分母がハードコーディングされています。 同じ許容値の計算を使用するテストを追加する予定がある場合、複数の場所でハードコーディングされた値を使用すると、コードの保守が困難になります。

1. **UnitTest1** クラスにプライベート ヘルパー メソッドを追加して許容値を計算し、そのメソッドを **RangeTest** から呼び出します。

    ```csharp
    private double ToleranceHelper(double expected)
    {
        return expected / 1000;
    }

    ...

    [TestMethod]
    public void RangeTest()
    {
        ...
        // Old code
        // double tolerance = expected/1000;

        // New code
        double tolerance = ToleranceHelper(expected);
    }
    ...
    ```

2. **RangeTest** を実行して、まだ成功することを確認します。

> [!TIP]
> **テスト エクスプローラー** に表示したくないテスト クラスにヘルパー メソッドを追加する場合は、メソッドに <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestMethodAttribute> 属性を追加しないでください。

## <a name="see-also"></a>関連項目

- [チュートリアル: テスト エクスプローラーを使用したテスト駆動開発](quick-start-test-driven-development-with-test-explorer.md)
