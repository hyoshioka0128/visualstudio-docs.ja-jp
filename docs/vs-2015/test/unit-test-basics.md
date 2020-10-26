---
title: 単体テストの基本 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-test
ms.topic: conceptual
f1_keywords:
- vs.UnitTest.CreateUnitTest
ms.assetid: a80ba9cd-4575-483c-b957-af7ed8dc7e20
caps.latest.revision: 29
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 0657fdd846c201b4f9bff4910bdd9fc271c399c9
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85543781"
---
# <a name="unit-test-basics"></a>単体テストの基本
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

コードが予想どおりに動作することを確認するには、単体テストを作成して実行します。 単体テストと呼ばれる理由は、プログラムの機能を、個々の *単体*としてテストできる独立したテスト可能な動作に分解するためです。 Visual Studio テスト エクスプローラーには、Visual Studio で単体テストを実行して結果を表示するための柔軟で効率的な方法が用意されています。 Visual Studio と共に、マネージド コードおよびネイティブ コード用の Microsoft 単体テスト フレームワークがインストールされます。 *単体テスト フレームワーク* を使用して、単体テストを作成して実行し、テストの結果を報告します。 変更を加えたときは単体テストを再実行し、コードが正しく機能するかテストします。 Visual Studio Enterprise を使用すると、ビルドの後でテストを自動的に実行できます。

 単体テストは、ソフトウェア開発ワークフローの構成要素になったときに、コードの品質に最大の効果をもたらします。 関数またはその他のアプリケーション コードを記述したらすぐに、標準的な入力データ、境界上のデータ、および正しくないデータに対するコードの動作を検証し、コードによる明示的または暗黙的な前提を確認する単体テストを作成してください。 *テスト駆動開発*では、コードを記述する前に単体テストを作成することで、設計ドキュメントと機能仕様の両方として単体テストを使用します。

 コードから簡単にテスト プロジェクトとテスト メソッドを生成したり、必要に応じて手動でテストを作成したりできます。 IntelliTest を使用して .NET コードを精査する際は、テスト データと単体テストのスイートを生成できます。 コードにある各ステートメントについて、そのステートメントを実行するテスト入力が生成されます。 [コードの単体テストを生成する](https://msdn.microsoft.com/library/dn823749.aspx)方法をご覧ください。

 テスト エクスプローラーは、テスト エクスプローラーのアドオン インターフェイスを実装した、サードパーティ製やオープン ソースの単体テスト フレームワークも実行できます。 Visual Studio 拡張機能マネージャーおよび Visual Studio ギャラリーを使用して、これらのフレームワークの多くを追加できます。 「[サードパーティ製の単体テスト フレームワークをインストールする](../test/install-third-party-unit-test-frameworks.md)」を参照してください。

- [クイック スタート](#BKMK_Quick_starts)

- [MyBank ソリューションの例](#BKMK_The_MyBank_Solution_example)

- [単体テストプロジェクトとテストメソッドを作成する](#BKMK_Creating_the_unit_test_projects)

- [テストを作成する](#BKMK_Writing_your_tests)

- [テスト エクスプローラーでテストを実行する](#BKMK_Running_tests_in_Test_Explorer)

- [テストを実行して表示する](#BKMK_Running_and_viewing_tests_from_the_Test_Explorer_toolbar)

## <a name="unit-testing-overview"></a><a name="BKMK_Unit_testing_overview"></a> 単体テストの概要

### <a name="quick-starts"></a><a name="BKMK_Quick_starts"></a> クイックスタート
 コーディングに直接関係する単体テストの概要については、次のいずれかのトピックを参照してください。

- [チュートリアル: マネージド コードに対する単体テストの作成と実行](../test/walkthrough-creating-and-running-unit-tests-for-managed-code.md)

- [クイック スタート: テスト エクスプローラーによるテスト駆動開発](../test/quick-start-test-driven-development-with-test-explorer.md)

- [テスト エクスプローラーを使用したネイティブ コードの単体テスト](https://msdn.microsoft.com/8a09d6d8-3613-49d8-9ffe-11375ac4736c)

## <a name="the-mybank-solution-example"></a><a name="BKMK_The_MyBank_Solution_example"></a> MyBank ソリューションの例
 このトピックでは、例として `MyBank` という架空のアプリケーションの開発を使用します。 このトピックの説明は、実際のコードがなくても理解できます。 テスト メソッドは C# で記述され、マネージド コード用の Microsoft 単体テスト フレームワークを使用して示されますが、その概念は他の言語やフレームワークに容易に移行できます。

 ![MyBank ソリューション](../test/media/ute-mybanksolution.png "UTE_MyBankSolution")

 `MyBank` アプリケーションのデザイン時の最初の計画には、個々のアカウントおよびアカウントの銀行との取引を表すアカウント コンポーネントと、個々のアカウントを集計および管理する機能を表すデータベース コンポーネントが含まれます。

 次の 2 つのプロジェクトを含む `MyBank` ソリューションを作成します。

- `Accounts`

- `BankDb`

  `Accounts` プロジェクトのデザイン時の最初の計画には、アカウントに関する基本情報を保持するクラス、アカウントでの資産の預け入れや引き出しなど、任意の種類のアカウントの共通機能を指定するインターフェイス、および当座預金アカウントを表すインターフェイスから派生したクラスが含まれます。 次のソース ファイルを作成して、Accounts プロジェクトを開始します。

- `AccountInfo.cs` は、アカウントの基本情報を定義します。

- `IAccount.cs` は、アカウントで資産の預け入れや引き出しを行うメソッドや、アカウントの残高を取得するメソッドを含む、アカウントの標準の `IAccount` インターフェイスを定義します。

- `CheckingAccount.cs` には、当座預金アカウントの `CheckingAccount` インターフェイスを実装する `IAccounts` クラスが含まれています。

  当座預金アカウントからの引き出しの際は、引き出される金額がアカウントの残高より少ないことを確認する必要があります。 そのため、この条件をチェックするメソッドで、 `IAccount.Withdaw` の `CheckingAccount` メソッドをオーバーライドします。 メソッドは次のようになります。

```csharp

public void Withdraw(double amount)
{
    if(m_balance >= amount)
    {
        m_balance -= amount;
    }
    else
    {
        throw new ArgumentException(amount, "Withdrawal exceeds balance!")
    }
}

```

 少しコードがあるので、テストしましょう。

## <a name="create-unit-test-projects-and-test-methods"></a><a name="BKMK_Creating_the_unit_test_projects"></a> 単体テスト プロジェクトとテスト メソッドを作成する
 ほとんどの場合、コードから単体テスト プロジェクトと単体テスト スタブを生成する方が手軽です。 また、必要に応じて単体テスト プロジェクトとテストを手動で作成することもできます。

 **単体テスト プロジェクトと単体テスト スタブを生成する**

1. コード エディター ウィンドウで、右クリックしてコンテキスト メニューから **[単体テストの作成]** を選択します。

    ![エディター ウィンドウで、コンテキスト メニューを表示](../test/media/createunittestsrightclick.png "CreateUnitTestsRightClick")

2. [OK] をクリックして、既定値をそのまま使用して単体テストを作成するか、単体テスト プロジェクトと単体テストの作成と名前付けに使用される値を変更します。 単体テスト メソッドに既定で追加されるコードを選択することができます。

    ![エディターで右&#45;クリックして [単体テストの作成] を選択する](../test/media/createunittestsdialog.png "CreateUnitTestsDialog")

3. 新しい単体テスト プロジェクトでは、クラス内のすべてのメソッドに単体テスト スタブが作成されます。

    ![単体テストが作成済み](../test/media/createunittestsstubs.png "CreateUnitTestsStubs")

4. ここで、先に進み、単体テストを有意義なものにするための [コードを単体テスト メソッドに追加する](#BKMK_Writing_your_tests) 方法と、コードを徹底的にテストするために追加する追加の単体テストについて確認します。

   **単体テスト プロジェクトと単体テストを手動で作成する**

   通常、単体テスト プロジェクトは 1 つのコード プロジェクトの構造を反映します。 MyBank の例で、2 つの単体テスト プロジェクト `AccountsTests` および `BankDbTests` を `MyBanks` ソリューションに追加します。 テスト プロジェクトの名前は任意ですが、標準の名前付け規則を採用することをお勧めします。

   **単体テスト プロジェクトをソリューションに追加するには**

5. **[ファイル]** メニューの **[新規作成]** をクリックし、 **[プロジェクト]** をクリックします (キーボード: Ctrl + Shift + N)。

6. [新しいプロジェクト] ダイアログ ボックスで、**[インストール済み]** ノードを展開して、テスト プロジェクトで使用する言語を選択し、**[テスト]** をクリックします。

7. Microsoft 単体テスト フレームワークの 1 つを使用するには、プロジェクト テンプレートの一覧から **[単体テスト プロジェクト]** を選択します。 それ以外の場合は、使用する単体テスト フレームワークのプロジェクト テンプレートを選択します。 この例の `Accounts` プロジェクトをテストするために、プロジェクトの名前を `AccountsTests`に設定します。

   > [!WARNING]
   > すべてのサードパーティ製およびオープン ソースの単体テスト フレームワークに、Visual Studio プロジェクトのテンプレートが用意されているわけではありません。 プロジェクトの作成については、フレームワークのドキュメントを参照してください。

8. この例の単体テスト プロジェクトで、テスト対象のコード プロジェクトへの参照を Accounts プロジェクトに追加します。

    コード プロジェクトへの参照を作成する方法は次のとおりです。

   1. ソリューション エクスプローラーでプロジェクトを選択します。

   2. **[プロジェクト]** メニューの **[参照の追加]** をクリックします。

   3. [参照マネージャー] ダイアログ ボックスで、**[ソリューション]** ノードを開き、**[プロジェクト]** を選択します。 コード プロジェクトの名前を選択し、ダイアログ ボックスを閉じます。

   各単体テスト プロジェクトには、コード プロジェクト内のクラス名を反映したクラスが含まれています。 この例では、 `AccountsTests` プロジェクトに次のクラスが含まれています。

- `AccountInfoTests` クラスには、 `AccountInfo` プロジェクトの `BankAccount` クラス用の単体テスト メソッドが含まれています。

- `CheckingAccountTests` クラスには、 `CheckingAccount` クラス用の単体テスト メソッドが含まれています。

## <a name="write-your-tests"></a><a name="BKMK_Writing_your_tests"></a> テストを作成する
 使用する単体テスト フレームワークと Visual Studio IntelliSense に従って、コード プロジェクトの単体テスト用コードを記述していきます。 ほとんどのフレームワークでは、テスト エクスプローラーで実行するには、単体テスト メソッドを識別する特定の属性を追加する必要があります。 フレームワークには、テスト メソッドが成功したか失敗したかを示す手段も用意されています。通常は、Assert ステートメントまたはメソッドの属性を使用します。 他の属性は、各テスト メソッドの前でクラスの初期化時に実行される省略可能な設定メソッド、および各テスト メソッドの後でクラスが破棄される前に実行される終了処理メソッドを識別します。

 AAA (Arrange、Act、Assert) のパターンが、テスト対象のメソッドの単体テストを記述する一般的な方法です。

- 単体テスト メソッドの **Arrange** セクションでは、オブジェクトを初期化し、テスト対象のメソッドに渡されるデータの値を設定します。

- **Act** セクションでは、設定されたパラメーターでテスト対象のメソッドを呼び出します。

- **Assert** セクションでは、テスト対象のメソッドの操作が予測どおりに動作することを検証します。

  この例の `CheckingAccount.Withdraw` メソッドをテストするために、2 つのテストを記述できます。メソッドの標準動作を検証するテストと、残高を超える引き出しが失敗することを検証するテストです。 `CheckingAccountTests` クラスで、次のメソッドを追加します。

```csharp
[TestMethod]
public void Withdraw_ValidAmount_ChangesBalance()
{
    // arrange
    double currentBalance = 10.0;
    double withdrawal = 1.0;
    double expected = 9.0;
    var account = new CheckingAccount("JohnDoe", currentBalance);
    // act
    account.Withdraw(withdrawal);
    double actual = account.Balance;
    // assert
    Assert.AreEqual(expected, actual);
}

[TestMethod]
[ExpectedException(typeof(ArgumentException))]
public void Withdraw_AmountMoreThanBalance_Throws()
{
    // arrange
    var account = new CheckingAccount("John Doe", 10.0);
    // act
    account.Withdraw(20.0);
    // assert is handled by the ExpectedException
}

```

 `Withdraw_ValidAmount_ChangesBalance` は明示的な `Assert` ステートメントを使用してテスト メソッドの成功/失敗を判定し、 `Withdraw_AmountMoreThanBalance_Throws` は `ExpectedException` 属性を使用してテスト メソッドの成功を判定していることに注意してください。 表には出ませんが、単体テスト フレームワークは try/catch ステートメントでテスト メソッドをラップしています。 ほとんどの場合、例外がキャッチされると、テスト メソッドは失敗し、例外は無視されます。 指定された例外がスローされた場合、 `ExpectedException` 属性によってテスト メソッドは成功します。

 Microsoft 単体テスト フレームワークの詳細については、次のトピックのいずれかを参照してください。

- [マネージド コード用の Microsoft 単体テスト フレームワークを使用した .NET Framework 用単体テストの記述](../test/writing-unit-tests-for-the-dotnet-framework-with-the-microsoft-unit-test-framework-for-managed-code.md)

- [C++ 用の Microsoft 単体テスト フレームワークを使用した C++ 用単体テストの記述](../test/writing-unit-tests-for-c-cpp-with-the-microsoft-unit-testing-framework-for-cpp.md)

## <a name="set-timeouts-for-unit-tests"></a>単体テストのタイムアウトを設定する
 個々のテスト メソッドで、タイムアウトを設定するには

```csharp
[TestMethod]
[Timeout(2000)]  // Milliseconds
public void My_Test()
{ ...
}
```

```vb

```

 許容される最大のタイムアウトを設定するには

```csharp
[TestMethod]
[Timeout(TestTimeout.Infinite)]  // Milliseconds
public void My_Test ()
{ ...
}
```

## <a name="run-tests-in-test-explorer"></a><a name="BKMK_Running_tests_in_Test_Explorer"></a> テストエクスプローラーでテストを実行する
 テスト プロジェクトをビルドすると、テストはテスト エクスプローラーに表示されます。 テスト エクスプローラーが表示されない場合は、Visual Studio メニューの **[テスト]** をクリックし、 **[Windows]** 、 **[テスト エクスプローラー]** の順に選択します。

 ![単体テスト エクスプローラー](../ide/media/ute-failedpassednotrunsummary.png "UTE_FailedPassedNotRunSummary")

 テストを実行して、記述し、再実行すると、テスト エクスプローラーの既定のビューに **[失敗したテスト]**、**[成功したテスト]**、**[スキップされたテスト]**、および **[テストを実行しない]** グループの結果が表示されます。 グループの見出しを選択して、そのグループ内のすべてのテストを表示するビューを開くことができます。

 グローバル レベルで検索ボックスでテキストを照合して、または定義済みのフィルターの 1 つを選択して、任意のビューでテストにフィルターを適用することもできます。 任意に選択したテストをいつでも実行できます。 テスト実行の結果は、エクスプローラー ウィンドウの上部にある成功/失敗ステータス バーですぐにわかります。 テストを選択すると、そのテスト メソッドの結果の詳細が表示されます。

### <a name="run-and-view-tests"></a><a name="BKMK_Running_and_viewing_tests_from_the_Test_Explorer_toolbar"></a> テストの実行と表示
 テスト エクスプローラーのツール バーは、対象にするテストを検出、編成、実行するのに役立ちます。

 ![テスト エクスプローラー ツールバーからテストを実行](../test/media/ute-toolbar.png "UTE_ToolBar")

 **[すべて実行]** を選択してテストをすべて実行することも、 **[実行]** を選択してテストのサブセットを実行することもできます。 一連のテストを実行した後、テスト実行の概要がテスト エクスプローラー ウィンドウの下部に表示されます。 テストを選択すると、そのテストの詳細が下部のペインに表示されます。 コンテキストメニューから [ **テストを開く** ] を選択します (キーボード: F12)。選択したテストのソースコードを表示します。

 個々のテストに実行順序を定める依存関係がない場合、ツール バーにある ![UTE&#95;parallelicon&#45;small](../test/media/ute-parallelicon-small.png "UTE_parallelicon-小") トグル ボタンで並列テストの実行を有効にします。 これにより、すべてのテスト実行にかかる時間を著しく短縮できます。

### <a name="run-tests-after-every-build"></a><a name="BKMK_Running_tests_after_every_build"></a> 各ビルドの後にテストを実行する

> [!WARNING]
> 各ビルドの後の単体テスト実行は、Visual Studio Enterprise でのみサポートされます。

|Image|説明|
|-|-|
|![ビルド後に実行](../test/media/ute-runafterbuild-btn.png "UTE_RunAfterBuild_btn")|各ローカル ビルドの後で単体テストを実行するには、標準のメニューの **[テスト]** を選択し、テスト エクスプローラーのツール バーの **[ビルド後にテストを実行]** を選択します。|

### <a name="filter-and-group-the-test-list"></a><a name="BKMK_Filtering_and_grouping_the_test_list"></a> テストリストのフィルター処理とグループ化
 多数のテストがある場合は、テスト エクスプローラーの検索ボックスに入力し、指定した文字列によって一覧をフィルター処理できます。 フィルターの一覧から選択することで、フィルター イベントをさらに制限できます。

 ![フィルターの検索カテゴリ](../test/media/ute-searchfilter.png "UTE_SearchFilter")

|Image|説明|
|-|-|
|![テスト エクスプローラー グループ ボタン](../test/media/ute-groupby-btn.png "UTE_GroupBy_btn")|カテゴリ別にテストをグループ化するには、 **[グループ化]** をクリックします。|

 詳細については、「[テストエクスプローラーを使用して単体テストを実行](../test/run-unit-tests-with-test-explorer.md)する」を参照してください。

## <a name="qa"></a>Q & A
 **Q: 単体テストのデバッグ方法を教えてください。**

 **A:** テスト エクスプローラーを使用して、テストのデバッグ セッションを開始します。 Visual Studio デバッガーを使用してコードをシームレスにステップ実行すると、テスト対象のプロジェクトと単体テストの間を切り替えることができます。 デバッグを開始するには:

1. Visual Studio エディターで、デバッグする 1 つ以上のテスト メソッドにブレークポイントを設定します。

   > [!NOTE]
   > テスト メソッドを任意の順序で実行できるため、デバッグするすべてのテスト メソッドにブレークポイントを設定します。

2. テストエクスプローラーでテストメソッドを選択し、ショートカットメニューの [ **選択したテストのデバッグ** ] をクリックします。

   [単体テストのデバッグ](../debugger/debugging-in-visual-studio.md)の詳細を確認してください。

   **Q: TDD を使用している場合にテストからコードを生成する方法を教えてください。**

   **A:** IntelliSense を使用して、プロジェクト コードにクラスとメソッドを生成します。 テスト メソッドに、生成するクラスまたはメソッドを呼び出すステートメントを記述し、その呼び出しの下で IntelliSense メニューを開きます。 新しいクラスのコンストラクターへの呼び出しの場合は、メニューから **[新しい型の生成]** を選択し、ウィザードに従ってコード プロジェクトにクラスを挿入します。 メソッドへの呼び出しの場合は、IntelliSense メニューから **[Generate new method (新しいメソッドの生成)]** を選択します。

   ![[メソッドスタブの生成] Intellisense メニュー](../test/media/ute-generatemethodstubintellisense.png "UTE_GenerateMethodStubIntellisense")

   **Q: テストを実行する入力値として複数のデータ セットを使用する単体テストを作成できますか。**

   **A:** はい。 *データ ドリブン テスト メソッド* を使用すると、1 つの単体テスト メソッドである範囲の値をテストすることができます。 テストする変数の値が格納されているデータ ソースとデータ テーブルを指定する、テスト メソッドの `DataSource` 属性を使用します。  メソッドの本体では、ColumnName インデクサーを使用して変数に行の値を割り当て `TestContext.DataRow[` *ColumnName* `]` ます。

> [!NOTE]
> ここに示すプロシージャは、マネージド コード用の Microsoft 単体テスト フレームワークを使用して記述したテスト メソッドにのみ適用できます。 別のフレームワークを使用している場合は、同等の機能についてフレームワークのドキュメントを参照してください。

 たとえば、`CheckingAccount` という名前の `AddIntegerHelper` クラスに不要なメソッドを追加するとします。 `AddIntegerHelper` は 2 つの整数を追加します。

 `AddIntegerHelper` メソッドのデータ ドリブン テストを作成するには、最初に `AccountsTest.accdb` という名前の Access データベースと `AddIntegerHelperData`という名前のテーブルを作成します。 `AddIntegerHelperData` テーブルは、追加の 1 番目と 2 番目のオペランドを指定する列、および予期される結果を指定する列を定義します。 多数の行に適切な値を入力します。

```csharp

[DataSource(
    @"Provider=Microsoft.ACE.OLEDB.12.0;Data Source=C:\Projects\MyBank\TestData\AccountsTest.accdb",
    "AddIntegerHelperData"
)]
[TestMethod()]
public void AddIntegerHelper_DataDrivenValues_AllShouldPass()
{
    var target = new CheckingAccount();
    int x = Convert.ToInt32(TestContext.DataRow["FirstNumber"]);
    int y = Convert.ToInt32(TestContext.DataRow["SecondNumber"]);
    int expected = Convert.ToInt32(TestContext.DataRow["Sum"]);
    int actual = target.AddIntegerHelper(x, y);
    Assert.AreEqual(expected, actual);
}

```

 属性付きメソッドは、テーブル内の各行に対して 1 回実行されます。 イテレーションが失敗した場合、テスト エクスプローラーがメソッドのテスト失敗を報告します。 メソッドのテスト結果の詳細ペインに、データの行ごとにメソッドの成功/失敗の状態が表示されます。

 [データ ドリブン単体テスト](../test/how-to-create-a-data-driven-unit-test.md)の詳細を確認してください。

 **Q: 単体テストでテストするコードの量を確認できますか。**

 **A:** はい。 Visual Studio のコード カバレッジ ツールを使用して、単体テストで実際にテスト中のコードの量を確認できます。 単体テスト フレームワークによって実行できるネイティブ言語とマネージド言語、およびすべての単体テスト フレームワークがサポートされています。

 選択したテストまたはソリューションのすべてのテストのコード カバレッジを実行できます。 [コード カバレッジの結果] ウィンドウに、行、関数、クラス、名前空間、およびモジュールで実行された製品コードのブロックのパーセンテージが表示されます。

 ソリューション内のテスト メソッドのコード カバレッジを実行するには、Visual Studio のメニューで、 **[テスト]** 、 **[コード カバレッジの分析]** の順に選択します。

 カバレッジの結果は、[コード カバレッジの結果] ウィンドウに表示されます。

 ![コード カバレッジの結果](../test/media/ute-codecoverageresults.png "UTE_CodeCoverageResults")

 [コード カバレッジ](../test/using-code-coverage-to-determine-how-much-code-is-being-tested.md) の詳細を確認してください。

 **Q: 外部依存関係を含むコード内のメソッドをテストする方法を教えてください。**

 **A:** はい。 Visual Studio Enterprise を使用している場合は、Microsoft Fakes は、マネージド コード用の単体テスト フレームワークを使用して記述したテスト メソッドで使用できます。

 Microsoft Fakes は、次の 2 つの方法で外部依存関係の代替クラスを作成します。

1. *スタブ* は、対象の依存関係クラスの親インターフェイスから派生した代替クラスを生成します。 スタブ メソッドは、対象クラスのパブリック仮想メソッドの代わりに使用できます。

2. *Shim* は、ランタイム インストルメンテーションを使用して、対象メソッドへの呼び出しを仮想でないメソッドの代替 shim メソッドに転換します。

   いずれの方法でも、依存関係メソッドへの呼び出しの生成されたデリゲートを使用して、テスト メソッド内の動作を指定します。

   詳細については、「 [Microsoft Fakes で単体テスト メソッドを分離する](../test/isolating-code-under-test-with-microsoft-fakes.md)」を参照してください。

   **Q: 他の単体テスト フレームワークを使用して単体テストを作成することはできますか。**

   **A:** はい。以下の手順に従って、 [他のフレームワークを検索してインストール](../test/install-third-party-unit-test-frameworks.md)してください。 Visual Studio を再起動した後、単体テストを作成するためのソリューションをもう一度開き、インストールしたフレームワークを選びます。

   ![他のインストールされている単体テスト フレームワークの選択](../test/media/createunittestsdialogextensions.png "CreateUnitTestsDialogExtensions")

   選んだフレームワークを使用して、単体テスト スタブが作成されます。
