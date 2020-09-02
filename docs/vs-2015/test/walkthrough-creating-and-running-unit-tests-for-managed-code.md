---
title: 'チュートリアル: マネージド コードに対する単体テストの作成と実行 | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-test
ms.topic: conceptual
helpviewer_keywords:
- unit tests, walkthrough
- unit tests, creating
- unit tests, generating
- unit tests, running
- unit tests, authoring
ms.assetid: 2b018b18-b412-4e0e-b0ee-b580a2f3ba9c
caps.latest.revision: 85
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 631a180789f5fff373799b78222c25a50ab32912
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72657102"
---
# <a name="walkthrough-creating-and-running-unit-tests-for-managed-code"></a>チュートリアル: マネージド コードに対する単体テストの作成と実行
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このチュートリアルでは、マネージド コード用の Microsoft 単体テスト フレームワークと Visual Studio テスト エクスプローラーを使用して一連の単体テストを作成、実行、およびカスタマイズする手順について説明します。 開発中の C# プロジェクトで作業を開始し、そのコードを実行するテストを作成し、テストを実行し、結果を調べます。 次に、プロジェクト コードを変更し、テストを再実行します。

 このトピックには、次のセクションが含まれます。

 [チュートリアルを準備する](../test/walkthrough-creating-and-running-unit-tests-for-managed-code.md#BKMK_Prepare_the_walkthrough)

 [単体テスト プロジェクトを作成する](../test/walkthrough-creating-and-running-unit-tests-for-managed-code.md#BKMK_Create_a_unit_test_project)

 [テスト クラスを作成する](../test/walkthrough-creating-and-running-unit-tests-for-managed-code.md#BKMK_Create_the_test_class)

- [テスト クラスの要件](../test/walkthrough-creating-and-running-unit-tests-for-managed-code.md#BKMK_Test_class_requirements)

  [最初のテスト メソッドを作成する](../test/walkthrough-creating-and-running-unit-tests-for-managed-code.md#BKMK_Create_the_first_test_method)

- [テスト メソッドの要件](../test/walkthrough-creating-and-running-unit-tests-for-managed-code.md#BKMK_Test_method_requirements)

  [テストをビルドして実行する](../test/walkthrough-creating-and-running-unit-tests-for-managed-code.md#BKMK_Build_and_run_the_test)

  [コードを修正してテストを再実行する](../test/walkthrough-creating-and-running-unit-tests-for-managed-code.md#BKMK_Fix_your_code_and_rerun_your_tests)

  [単体テストを使用してコードを改良する](../test/walkthrough-creating-and-running-unit-tests-for-managed-code.md#BKMK_Use_unit_tests_to_improve_your_code)

> [!NOTE]
> このチュートリアルでは、マネージド コード用の Microsoft 単体テスト フレームワークを使用します。 また、テスト エクスプローラー用のアダプターを備えたサード パーティの単体テスト フレームワークからテスト エクスプローラーを実行することもできます。 詳細については、「[サードパーティ製の単体テストフレームワークをインストール](../test/install-third-party-unit-test-frameworks.md)する」を参照してください。

> [!NOTE]
> コマンド ラインからテストを実行する方法については、「[チュートリアル: コマンド ライン テスト ユーティリティの使用](https://msdn.microsoft.com/library/52c11992-9e94-4067-a4b7-59f19d69d867)」をご覧ください。

## <a name="prerequisites"></a>前提条件

- Bank プロジェクト。 「[単体テストを作成するサンプル プロジェクト](../test/sample-project-for-creating-unit-tests.md)」をご覧ください。

## <a name="prepare-the-walkthrough"></a><a name="BKMK_Prepare_the_walkthrough"></a> チュートリアルを準備する

1. Visual Studio を開きます。

2. **[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** をクリックします。

    **[新しいプロジェクト]** ダイアログ ボックスが表示されます。

3. **[インストールされているテンプレート]** の **[Visual C#]** をクリックします。

4. アプリケーションの種類の一覧の **[クラス ライブラリ]** をクリックします。

5. In the **[名前]** ボックスに「 `Bank` をポイントし、 **[OK]**」をご覧ください。

   > [!NOTE]
   > "Bank" という名前が既に使用されている場合は、別のプロジェクト名を選択します。

    新しい Bank プロジェクトが作成され、コード エディターに Class1.cs ファイルが開いた状態でソリューション エクスプローラーが表示されます。

   > [!NOTE]
   > コード エディターに Class1.cs ファイルが表示されない場合、ソリューション エクスプローラーのファイル Class1.cs をダブルクリックして開きます。

6. 「[単体テストを作成するためのサンプル プロジェクト](../test/sample-project-for-creating-unit-tests.md)」からソース コードをコピーします。

7. Class1.cs の元の内容を、「[単体テスト作成用のサンプル プロジェクト](../test/sample-project-for-creating-unit-tests.md)」のコードで置き換えます。

8. ファイルを BankAccount.cs として保存します。

9. **[ビルド]** メニューの **[ソリューションのビルド]** をクリックします。

   Bank という名前のプロジェクトができます。 これには、テストするソース コードとテストに使用するツールが含まれています。 Bank の **BankAccountNS**名前空間には、パブリック クラス **BankAccount**が含まれます。そのメソッドを次の手順でテストします。

   このクイック スタートでは、 `Debit` メソッドについて説明します。Debit メソッドは、現金が口座から引き出され、次のコードが含まれているときに呼び出されます。

```csharp
// method under test
public void Debit(double amount)
{
    if(amount > m_balance)
    {
        throw new ArgumentOutOfRangeException("amount");
    }
    if (amount < 0)
    {
        throw new ArgumentOutOfRangeException("amount");
    }
    m_balance += amount;
}

```

## <a name="create-a-unit-test-project"></a><a name="BKMK_Create_a_unit_test_project"></a> 単体テストプロジェクトを作成する
 **必要条件**: 「 [Prepare the walkthrough](../test/walkthrough-creating-and-running-unit-tests-for-managed-code.md#BKMK_Prepare_the_walkthrough)」の手順に従います。

#### <a name="to-create-a-unit-test-project"></a>単体テスト プロジェクトを作成するには

1. **[ファイル]** メニューの **[追加]** をポイントし、 **[新しいプロジェクト]** をクリックします。

2. [新しいプロジェクト] ダイアログ ボックスで、 **[インストール済み]** 、 **[Visual C#]** の順に展開し、 **[テスト]** を選択します。

3. テンプレートの一覧から、 **[単体テスト プロジェクト]** を選択します。

4. **[名前]** ボックスに「BankTest」と入力し、 **[OK]** をクリックします。

     **BankTests** プロジェクトが **Bank** ソリューションに追加されます。

5. **BankTests** プロジェクトで、 **Bank** ソリューションへの参照を追加します。

     ソリューション エクスプローラーで、 **BankTests** プロジェクトの **[参照設定]** をクリックし、コンテキスト メニューの **[参照の追加]** をクリックします。

6. [参照マネージャー] ダイアログ ボックスで、 **[ソリューション]** を展開し、 **[Bank]** チェックボックスをオンにします。

## <a name="create-the-test-class"></a><a name="BKMK_Create_the_test_class"></a> テストクラスを作成する
 `BankAccount` クラスを検証するためのテスト クラスが必要です。 プロジェクト テンプレートによって生成された UnitTest1.cs を使用できますが、ファイルとクラスにはよりわかりやすい名前を付ける必要があります。 ソリューション エクスプローラーでファイルの名前変更機能を使用すると、この処理を 1 つの手順で実行できます。

 **クラス ファイルの名前を変更する**

 ソリューション エクスプローラーで、BankTests プロジェクトの UnitTest1.cs ファイルを選択します。 コンテキスト メニューの **[名前の変更]** をクリックし、ファイルの名前を BankAccountTests.cs に変更します。 コード要素 UnitTest1 に対するプロジェクトのすべての参照を名前変更するかどうかを確認するダイアログで **[はい]** をクリックします。 この手順により、クラスの名前が `BankAccountTest`に変更されます。

 BankAccountTests.cs ファイルには次のコードが含まれるようになりました。

```csharp
// unit test code
using System;
using Microsoft.VisualStudio.TestTools.UnitTesting;

namespace BankTests
{
    [TestClass]
    public class BankAccountTests
    {
        [TestMethod]
        public void TestMethod1()
        {
        }
    }
}
```

 **テスト対象のプロジェクトに using ステートメントを追加する**

 using ステートメントをクラスに追加して、完全修飾名を使用せずにテスト対象のプロジェクトに呼び出すことができるようにすることも可能です。 クラス ファイルの先頭に次のように追加します。

```csharp
using BankAccountNS;
```

### <a name="test-class-requirements"></a><a name="BKMK_Test_class_requirements"></a> テストクラスの要件
 テスト クラスの最小要件は次のとおりです。

- マネージド コード用の Microsoft 単体テスト フレームワークでは、テスト エクスプローラーで実行する単体テスト メソッドを含むすべてのクラスについて、 `[TestClass]` 属性が必要です。

- テスト エクスプローラーで実行する各テスト メソッドには `[TestMethod]`属性が必要です。

  単体テスト プロジェクトで `[TestClass]` 属性がない別のクラスを使用することができます。また、テスト クラスで `[TestMethod]` 属性がない別のメソッドを使用することもできます。 こうした別のクラスやメソッドをテスト メソッドで使用できます。

## <a name="create-the-first-test-method"></a><a name="BKMK_Create_the_first_test_method"></a> 最初のテストメソッドを作成する
 この手順では、 `Debit` クラスの `BankAccount` メソッドの動作を検証する単体テスト メソッドを記述します。 メソッドは上に一覧表示されています。

 テスト対象のメソッドを分析したところ、チェックする必要のある動作が 3 つ以上あると判断されます。

1. このメソッドは、[ArgumentOutOfRangeException] (<!-- TODO: review code entity reference <xref:assetId:///ArgumentOutOfRangeException?qualifyHint=False&amp;autoUpgrade=True>  -->) が残高を超える場合。

2. また、引き落とし金額が 0 未満の場合も、このメソッドは `ArgumentOutOfRangeException` をスローします。

3. 1. と 2. のチェックで金額が有効な範囲内であることが確認された場合、このメソッドは口座残高から当該金額を減算します。

   最初のテストでは、正しい金額 (口座残高未満かつ 0 を上回る金額) によって口座から正しい金額が引き出されることが確認されます。

#### <a name="to-create-a-test-method"></a>テスト メソッドを作成するには

1. 使用する `BankAccountNS;` ステートメントを BankAccountTests.cs ファイルに追加します。

2. 次のメソッドを `BankAccountTests` クラスに追加します。

   ```csharp
   // unit test code
   [TestMethod]
   public void Debit_WithValidAmount_UpdatesBalance()
   {
       // arrange
       double beginningBalance = 11.99;
       double debitAmount = 4.55;
       double expected = 7.44;
       BankAccount account = new BankAccount("Mr. Bryan Walton", beginningBalance);

       // act
       account.Debit(debitAmount);

       // assert
       double actual = account.Balance;
       Assert.AreEqual(expected, actual, 0.001, "Account not debited correctly");
   }
   ```

   このメソッドはやや単純です。 期首残高を含む新しい `BankAccount` オブジェクトを設定し、有効な金額を引き出します。 マネージド コード用の Microsoft 単体テスト フレームワークの <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert.AreEqual%2A> メソッドを使用して、期末残高が想定どおりであることを確認します。

### <a name="test-method-requirements"></a><a name="BKMK_Test_method_requirements"></a> テストメソッドの要件
 テスト メソッドは次の条件を満たしている必要があります。

- メソッドは `[TestMethod]` 属性で装飾される必要があります。

- メソッドは `void`を返します。

- メソッドはパラメーターを含むことができません。

## <a name="build-and-run-the-test"></a><a name="BKMK_Build_and_run_the_test"></a> テストをビルドして実行する

#### <a name="to-build-and-run-the-test"></a>テストをビルドして実行するには

1. **[ビルド]** メニューの **[ソリューションのビルド]** をクリックします。

     エラーがない場合は、[UnitTestExplorer] ウィンドウが表示され、 **[テストを実行しない]** グループに **[Debit_WithValidAmount_UpdatesBalance]** が表示されます。 ビルドの成功後にテスト エクスプローラーが表示されない場合は、メニューの **[テスト]** をクリックし、 **[ウィンドウ]**、  **[テスト エクスプローラー]** の順にクリックします。

2. **[すべて実行]** をクリックしてテストを実行します。 テストの実行中は、ウィンドウの上部にあるステータス バーがアニメーション化されます。 テストの実行の終了時に、すべてのテスト メソッドが成功した場合はステータス バーが緑色に変わり、いずれかのテストが失敗した場合は赤色に変わります。

3. この場合は、テストが失敗します。 このテスト メソッドは、 **[失敗したテスト]** に移動します。 が表示されます。 エクスプローラーでテスト メソッドを選択すると、ウィンドウの下部に詳細が表示されます。

## <a name="fix-your-code-and-rerun-your-tests"></a><a name="BKMK_Fix_your_code_and_rerun_your_tests"></a> コードを修正してテストを再実行する
 **テスト結果を分析する**

 テスト結果には失敗を示すメッセージが含まれています。 メソッドの場合、 `AreEquals` 予期された値 (<strong> \<*XXX*> 必要</strong>なパラメーター) と実際に受信したもの (**実際 \<*YYY*> **のパラメーター) がメッセージに表示されます。 ここでは、残高が期首残高よりも減少していることを想定していましたが、逆に、引き出し額の分が増加していました。

 Debit コードの再検査では、単体テストでバグを検出できたことが示されます。 引き出し額は、減算する必要があるときに口座残高に追加されます。

 **バグを修正する**

 エラーを修正するには、単純に行を置き換えます。

```csharp
m_balance += amount;
```

 with

```csharp
m_balance -= amount;
```

 **テストを再実行する**

 テストエクスプローラーで [ **すべて実行** ] をクリックして、テストを再実行します。 赤色/緑色のステータス バーは緑色になり、テストは **[成功したテスト]** グループに移動します。

## <a name="use-unit-tests-to-improve-your-code"></a><a name="BKMK_Use_unit_tests_to_improve_your_code"></a> 単体テストを使用してコードを改善する
 このセクションでは、分析の反復処理、単体テストの進展、およびリファクタリングが、実稼働のコードの堅牢性と有効性を高めるうえでどのように役立つかを説明します。

 **問題を分析する**

 `Debit` メソッドで有効な金額が正しく差し引かれることを確認するテスト メソッドを作成したら、元の分析における残りのケースに移ることができます。

1. 引き落とし金額が残高を上回る場合、このメソッドは `ArgumentOutOfRangeException` をスローします。

2. また、引き落とし金額が 0 未満の場合も、このメソッドは `ArgumentOutOfRangeException` をスローします。

   **テスト メソッドを作成する**

   これらの問題に対処するためのテスト メソッド作成への最初の試みは、期待の持てるものです。

```csharp
//unit test method
[TestMethod]
[ExpectedException(typeof(ArgumentOutOfRangeException))]
public void Debit_WhenAmountIsLessThanZero_ShouldThrowArgumentOutOfRange()
{
    // arrange
    double beginningBalance = 11.99;
    double debitAmount = -100.00;
    BankAccount account = new BankAccount("Mr. Bryan Walton", beginningBalance);

    // act
    account.Debit(debitAmount);

    // assert is handled by ExpectedException
}

```

 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.ExpectedExceptionAttribute> 属性を使用して、正しい例外がスローされたことをアサートします。 この属性により、 `ArgumentOutOfRangeException` がスローされない限り、テストは失敗します。 正と負の両方の `debitAmount` 値を使用してテストを実行し、金額が 0 未満のときに汎用的な <xref:System.ApplicationException> をスローするようにメソッドを一時的に変更すると、テストが正しく動作することが示されます。 引き出し金額が残高を上回るケースをテストするために必要なことは次のとおりです。

1. `Debit_WhenAmountIsMoreThanBalance_ShouldThrowArgumentOutOfRange`という新しいテスト メソッドを作成します。

2. メソッド本体を `Debit_WhenAmountIsLessThanZero_ShouldThrowArgumentOutOfRange` から新しいメソッドにコピーします。

3. `debitAmount` を、残高を上回る数値に設定します。

   **テストの実行**

   `debitAmount` を異なる値にして 2 つのメソッドを実行すると、テストで残りのケースが適切に処理されることが示されます。 3 つのすべてのテストを実行すると、元の分析のすべてのケースが正しく処理されることを確認できます。

   **分析を継続する**

   一方で、最後の 2 つのテスト メソッドには多少の問題もあります。 一方のテストの実行時に、テスト対象のコードのいずれの条件がスローされたかがはっきりしません。 そこで、2 つの条件を区別するのに役立つ方法があります。 この問題についてさらに考えてみると、いずれの条件に違反したかを把握することでテストの信頼性が高まることが明らかになります。 また、この情報は、テスト対象のメソッドで例外がスローされたときに例外を処理する実稼働のメカニズムにも役立つ可能性があります。 メソッドでのスロー時により多くの情報が生成されると、すべての懸念事項に役立ちますが、 `ExpectedException` 属性ではこの情報を提供できません。

   テスト対象のメソッドをもう一度確認すると、引数の名前をパラメーターとして使用する `ArgumentOutOfRangeException` コンストラクターが両方の条件ステートメントで使用されていることがわかります。

```csharp
throw new ArgumentOutOfRangeException("amount");
```

 また、MSDN ライブラリを検索すると、さらに豊富な情報を報告するコンストラクターが存在することがわかります。 <xref:System.ArgumentOutOfRangeException.%23ctor%2A>`(String, Object, String)` には、引数の名前、引数の値、およびユーザー定義のメッセージが含まれています。 このコンストラクターを使用するようにテスト対象のメソッドをリファクタリングできます。 さらに、一般に公開されている型メンバーを使用して、エラーを指定できます。

 **テスト対象のコードをリファクタリングする**

 最初に、エラー メッセージの 2 つの定数をクラス スコープで定義します。

```csharp
// class under test
public const string DebitAmountExceedsBalanceMessage = "Debit amount exceeds balance";
public const string DebitAmountLessThanZeroMessage = "Debit amount less than zero";
```

 次に、 `Debit` メソッドの 2 つの条件ステートメントを変更します。

```csharp
// method under test
// ...
    if (amount > m_balance)
    {
        throw new ArgumentOutOfRangeException("amount", amount, DebitAmountExceedsBalanceMessage);
    }

    if (amount < 0)
    {
        throw new ArgumentOutOfRangeException("amount", amount, DebitAmountLessThanZeroMessage);
    }
// ...
```

 **テスト メソッドをリファクタリングする**

 このテスト メソッドでは、最初に `ExpectedException` 属性を削除します。 その代わりに、スローされた例外をキャッチし、その例外が正しい条件ステートメントでスローされたことを確認します。 また一方、2 つのオプションのどちらを使用して残りの条件を検証するかをここで決める必要があります。 たとえば `Debit_WhenAmountIsMoreThanBalance_ShouldThrowArgumentOutOfRange` メソッドでは、次のアクションのいずれかを使用できます。

- 例外 ( `ActualValue` コンストラクターの 2 番目のパラメーター) の `ArgumentOutOfRangeException` プロパティが期首残高を上回っていることをアサートします。 このオプションでは、テスト メソッドの `ActualValue` 変数に対して例外の `beginningBalance` プロパティをテストし、 `ActualValue` が 0 を上回ることを確認する必要があります。

- `DebitAmountExceedsBalanceMessage` クラスに定義された `BankAccount` がメッセージ (コンストラクターの 3 番目のパラメーター) に含まれていることをアサートします。

  Microsoft 単体テスト フレームワークの <xref:Microsoft.VisualStudio.TestTools.UnitTesting.StringAssert.Contains%2A?displayProperty=fullName> メソッドでは、1 番目のオプションで必要とされる計算を行わなくても、2 番目のオプションを確認できます。

  `Debit_WhenAmountIsMoreThanBalance_ShouldThrowArgumentOutOfRange` の変更の 2 回目の試行は次のようになります。

```csharp
[TestMethod]
public void Debit_WhenAmountIsMoreThanBalance_ShouldThrowArgumentOutOfRange()
{
    // arrange
    double beginningBalance = 11.99;
    double debitAmount = 20.0;
    BankAccount account = new BankAccount("Mr. Bryan Walton", beginningBalance);

    // act
    try
    {
        account.Debit(debitAmount);
    }
    catch (ArgumentOutOfRangeException e)
    {
        // assert
        StringAssert.Contains(e.Message, BankAccount. DebitAmountExceedsBalanceMessage);
    }
}
```

 **再テストする、書き換える、再分析する**

 テスト メソッドを別の値で再テストする場合、次の事項が発生します。

1. `debitAmount` が残高を上回るアサートを使用することで適切なエラーをキャッチした場合、 `Contains` アサートは成功し、例外は無視されます。したがって、テスト メソッドは成功することになります。 これは想定どおりの動作です。

2. 0 未満の `debitAmount` を使用した場合、不適切なエラー メッセージが返されるため、アサートは失敗します。 テスト対象メソッドのコード パス上の別のポイントで一時的な `ArgumentOutOfRange` 例外を導入した場合も、アサートは失敗します。 これも適切です。

3. `debitAmount` 値が有効な場合 (残高未満だが 0 よりは大きい場合)、例外はキャッチされないので、アサートはキャッチされません。 テスト メソッドは成功します。 これは適切ではありません。例外がスローされない場合はテスト メソッドが失敗することを想定しているためです。

   3 番目の事項はテスト メソッドのバグです。 この問題を解決しようとする場合は、テスト メソッドの最後に <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert.Fail%2A> アサートを追加して、例外がスローされないケースを処理するようにします。

   ただし、再テストでは、正しい例外がキャッチされた場合にテストが失敗したことが示されます。 catch ステートメントで例外がリセットされ、メソッドは継続して実行されますが、新しいアサートで失敗します。 この新しい問題を解決するために、 `return` の後に `StringAssert`ステートメントを追加します。 再テストにより、問題を修正したことを確認します。 `Debit_WhenAmountIsMoreThanBalance_ShouldThrowArgumentOutOfRange` の最終バージョンは、次のようになります。

```csharp
[TestMethod]
public void Debit_WhenAmountIsMoreThanBalance_ShouldThrowArgumentOutOfRange()
{
    // arrange
    double beginningBalance = 11.99;
    double debitAmount = 20.0;
    BankAccount account = new BankAccount("Mr. Bryan Walton", beginningBalance);

    // act
    try
    {
        account.Debit(debitAmount);
    }
    catch (ArgumentOutOfRangeException e)
    {
        // assert
        StringAssert.Contains(e.Message, BankAccount. DebitAmountExceedsBalanceMessage);
        return;
    }
    Assert.Fail("No exception was thrown.");
}

```

 この最後のセクションでは、テスト コード向上の作業を実行したことにより、より堅牢でわかりやすいテスト メソッドになりました。 さらに重要なこととして、分析の追加によってテスト対象のプロジェクトのコードを改善することもできます。
