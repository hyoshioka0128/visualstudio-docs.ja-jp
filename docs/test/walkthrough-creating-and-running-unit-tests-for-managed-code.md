---
title: C# 単体テスト チュートリアル
ms.date: 05/14/2019
ms.topic: conceptual
helpviewer_keywords:
- unit tests, walkthrough
- unit tests, creating
- unit tests, generating
- unit tests, running
- unit tests, authoring
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
author: mikejo5000
ms.openlocfilehash: b1ec115dd960799a1242a0d60bd793d671facb18
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75590710"
---
# <a name="walkthrough-create-and-run-unit-tests-for-managed-code"></a>チュートリアル: マネージド コードの単体テストを作成し、実行する

この記事では、マネージド コード用の Microsoft 単体テスト フレームワークと Visual Studio **テスト エクスプローラー**を使用して一連の単体テストを作成、実行、およびカスタマイズする手順について説明します。 開発中の C# プロジェクトで作業を開始し、そのコードを実行するテストを作成し、テストを実行し、結果を調べます。 次に、プロジェクト コードを変更し、テストを再実行します。

## <a name="create-a-project-to-test"></a>テストするプロジェクトを作成する

::: moniker range="vs-2017"

1. Visual Studio を開きます。

2. **[ファイル]** メニューの **[新規]** > **[プロジェクト]** を選択します。

   **[新しいプロジェクト]** ダイアログ ボックスが表示されます。

3. **[Visual C#]** > **[.NET Core]** カテゴリで、 **[コンソール アプリ (.NET Core)]** プロジェクト テンプレートを選択します。

4. プロジェクトに「**Bank**」という名前を設定してから、 **[OK]** をクリックします。

   Bank プロジェクトが作成され、コード エディターに *Program.cs* ファイルが開いた状態で**ソリューション エクスプローラー**が表示されます。

   > [!NOTE]
   > エディターで *Program.cs* が開いていない場合は、**ソリューション エクスプローラー**のファイル *Program.cs* をダブルクリックして開きます。

::: moniker-end

::: moniker range=">=vs-2019"

1. Visual Studio を開きます。

2. スタート ウィンドウで、 **[新しいプロジェクトの作成]** を選択します。

3. C# **[Console App (.NET Core)]\(コンソール アプリ (.NET Core)\)** プロジェクト テンプレートを検索して選択し、 **[次へ]** をクリックします。

4. プロジェクトに「**Bank**」という名前を設定して、 **[作成]** をクリックします。

   Bank プロジェクトが作成され、コード エディターに *Program.cs* ファイルが開いた状態で**ソリューション エクスプローラー**が表示されます。

   > [!NOTE]
   > エディターで *Program.cs* が開いていない場合は、**ソリューション エクスプローラー**のファイル *Program.cs* をダブルクリックして開きます。

::: moniker-end

5. *Program.cs* のコンテンツを *BankAccount* クラスを定義する次の C# コードで置換します。

   ```csharp
   using System;

   namespace BankAccountNS
   {
       /// <summary>
       /// Bank account demo class.
       /// </summary>
       public class BankAccount
       {
           private readonly string m_customerName;
           private double m_balance;

           private BankAccount() { }

           public BankAccount(string customerName, double balance)
           {
               m_customerName = customerName;
               m_balance = balance;
           }

           public string CustomerName
           {
               get { return m_customerName; }
           }

           public double Balance
           {
               get { return m_balance; }
           }

           public void Debit(double amount)
           {
               if (amount > m_balance)
               {
                   throw new ArgumentOutOfRangeException("amount");
               }

               if (amount < 0)
               {
                   throw new ArgumentOutOfRangeException("amount");
               }

               m_balance += amount; // intentionally incorrect code
           }

           public void Credit(double amount)
           {
               if (amount < 0)
               {
                   throw new ArgumentOutOfRangeException("amount");
               }

               m_balance += amount;
           }

           public static void Main()
           {
               BankAccount ba = new BankAccount("Mr. Bryan Walton", 11.99);

               ba.Credit(5.77);
               ba.Debit(11.22);
               Console.WriteLine("Current balance is ${0}", ba.Balance);
           }
       }
   }
   ```

6. **ソリューション エクスプローラー**で右クリックして **[名前の変更]** を選択し、ファイルの名前を *BankAccount.cs* に変更します。

7. **[ビルド]** メニューの **[ソリューションのビルド]** をクリックします。

これでテストできるプロジェクトとメソッドが用意されました。 この記事のテストは `Debit` メソッドに焦点を当てています。 `Debit` メソッドは、口座から現金が引き出されるときに呼び出されます。

## <a name="create-a-unit-test-project"></a>単体テスト プロジェクトを作成する

1. **[ファイル]** メニューで **[追加]**  >  **[新しいプロジェクト]** の順に選択します。

   > [!TIP]
   > **ソリューション エクスプローラー**でソリューションを右クリックし、 **[追加]**  >  **[新しいプロジェクト]** の順に選択することもできます。

::: moniker range="vs-2017"

2. **[新しいプロジェクト]** ダイアログ ボックスで、 **[インストール済み]** 、 **[Visual C#]** の順に展開し、 **[テスト]** を選択します。

3. テンプレートの一覧から、 **[MSTest テスト プロジェクト (.NET Core)]** を選択します。

4. **[名前]** ボックスに「`BankTests`」と入力して、 **[OK]** を選択します。

   **BankTests** プロジェクトが **Bank** ソリューションに追加されます。

::: moniker-end

::: moniker range=">=vs-2019"

2. C# **MSTest テスト プロジェクト (.NET Core)** プロジェクト テンプレートを検索して選択し、 **[次へ]** をクリックします。

3. プロジェクトに **BankTests** という名前を付けます。

4. **[作成]** をクリックします。

   **BankTests** プロジェクトが **Bank** ソリューションに追加されます。

::: moniker-end

5. **BankTests** プロジェクトで、**Bank** プロジェクトへの参照を追加します。

   **ソリューション エクスプローラー**で、**BankTests** プロジェクトの **[依存関係]** を選択し、右クリック メニューの **[参照の追加]** を選択します。

6. **[参照マネージャー]** ダイアログ ボックスで、 **[プロジェクト]** を展開し、 **[ソリューション]** を選択し、 **[Bank]** チェックボックスをオンにします。

7. **[OK]** をクリックします。

## <a name="create-the-test-class"></a>テスト クラスを作成する

`BankAccount` クラスを検証するテスト クラスを作成します。 プロジェクト テンプレートによって生成された *UnitTest1.cs* ファイルを使用できますが、ファイルとクラスにはよりわかりやすい名前を付けます。

### <a name="rename-a-file-and-class"></a>ファイルとクラスの名前を変更する

1. ファイルの名前を変更するには、**ソリューション エクスプローラー**で、BankTests プロジェクトの *UnitTest1.cs* ファイルを選択します。 右クリック メニューの **[名前の変更]** をクリックし、ファイルの名前を *BankAccountTests.cs* に変更します。

::: moniker range="vs-2017"

2. クラスの名前を変更するには、ダイアログ ボックスが表示され、コード要素への参照の名前も変更するかどうかを問われたときに **[はい]** を選択します。

::: moniker-end

::: moniker range=">=vs-2019"

2. クラスの名前を変更するには、コード エディター内で `UnitTest1` にカーソルを合わせ、右クリックして、 **[名前の変更]** を選択します。 「**BankAccountTests**」と入力し、**Enter** を押します。

::: moniker-end

*BankAccountTests.cs* ファイルには次のコードが含まれるようになりました。

```csharp
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

### <a name="add-a-using-statement"></a>using ステートメントを追加する

[`using` ステートメント](/dotnet/csharp/language-reference/keywords/using-statement)をクラスに追加し、完全修飾名を使用せずにテスト対象のプロジェクトに呼び出すことができるようにします。 クラス ファイルの先頭に次のように追加します。

```csharp
using BankAccountNS;
```

### <a name="test-class-requirements"></a>テスト クラスの要件

テスト クラスの最小要件は次のとおりです。

- テスト エクスプローラーで実行する単体テスト メソッドを含むすべてのクラスについて、`[TestClass]` 属性が必要です。

- テスト エクスプローラーで認識する各テスト メソッドには、`[TestMethod]` 属性が必要です。

単体テスト プロジェクトで `[TestClass]` 属性がない別のクラスを使用することができます。また、テスト クラスで `[TestMethod]` 属性がない別のメソッドを使用することもできます。 こうした別のクラスやメソッドをテスト メソッドから呼び出すことができます。

## <a name="create-the-first-test-method"></a>最初のテスト メソッドを作成する

この手順では、`BankAccount` クラスの `Debit` メソッドの動作を検証する単体テスト メソッドを記述します。

確認する必要がある動作は少なくとも 3 つあります。

- 引き落とし金額が残高を上回る場合、このメソッドは <xref:System.ArgumentOutOfRangeException> をスローします。

- 引き落とし金額が 0 未満の場合、このメソッドは <xref:System.ArgumentOutOfRangeException> をスローします。

- 引き落とし金額が有効な場合、このメソッドは口座残高から借方金額を減算します。

> [!TIP]
> このチュートリアルでは使用しないため、既定の `TestMethod1` メソッドを削除できます。

### <a name="to-create-a-test-method"></a>テスト メソッドを作成するには

最初のテストでは、正しい金額 (つまり、口座残高未満かつ 0 を上回る金額) によって口座から正しい金額が引き出されることが確認されます。 次のメソッドを `BankAccountTests` クラスに追加します。

```csharp
[TestMethod]
public void Debit_WithValidAmount_UpdatesBalance()
{
    // Arrange
    double beginningBalance = 11.99;
    double debitAmount = 4.55;
    double expected = 7.44;
    BankAccount account = new BankAccount("Mr. Bryan Walton", beginningBalance);

    // Act
    account.Debit(debitAmount);

    // Assert
    double actual = account.Balance;
    Assert.AreEqual(expected, actual, 0.001, "Account not debited correctly");
}
```

このメソッドは単純です。期首残高を含む新しい `BankAccount` オブジェクトを設定し、有効な金額を引き出します。 期末残高が予想どおりであることを確認するには、<xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert.AreEqual%2A?displayProperty=nameWithType> メソッドを使用します。

### <a name="test-method-requirements"></a>テスト メソッドの要件

テスト メソッドは次の条件を満たしている必要があります。

- `[TestMethod]` 属性で修飾されています。

- `void` を返します。

- パラメーターを含むことができません。

## <a name="build-and-run-the-test"></a>テストをビルドして実行する

1. **[ビルド]** メニューの **[ソリューションのビルド]** をクリックします。

2. **テスト エクスプローラー**が開いていない場合、上部のメニュー バーで **[テスト]** 、 **[Windows]** 、 **[テスト エクスプローラー]** の順に選択します。

3. **[すべて実行]** をクリックしてテストを実行します。

   テストの実行中は、 **[テスト エクスプローラー]** ウィンドウの上部にあるステータス バーがアニメーション化されます。 テストの実行の終了時に、すべてのテスト メソッドが成功した場合はステータス バーが緑色に変わり、いずれかのテストが失敗した場合は赤色に変わります。

   この場合は、テストが失敗します。

4. **テスト エクスプローラー**でメソッドを選択すると、ウィンドウの下部に詳細が表示されます。

## <a name="fix-your-code-and-rerun-your-tests"></a>コードを修正してテストを再実行する

テスト結果には失敗を示すメッセージが含まれています。 `AreEqual` メソッドの場合、メッセージには、予想された内容と実際に受け取られた内容が表示されます。 残高が減少することを予想していましたが、代わりに引き出し額の分だけ増加していました。

単体テストにより、引き出し額は、*減算*する必要があるときに口座残高に*追加*されます。単体テストではバグがわかりました。

### <a name="correct-the-bug"></a>バグを修正する

エラーを修正するには、*BankAccount.cs* ファイルで次の行を

```csharp
m_balance += amount;
```

次の内容に置き換えます。

```csharp
m_balance -= amount;
```

### <a name="rerun-the-test"></a>テストを再実行する

**テスト エクスプローラー**で、 **[すべて実行]** を選択してテストを再実行します。 赤/緑のバーが緑に変わり、テストに合格したことを示します。

![テストに合格したことを示す Visual Studio 2019 のテスト エクスプローラー](media/test-explorer-banktests-passed.png)

## <a name="use-unit-tests-to-improve-your-code"></a>単体テストを使用してコードを改良する

このセクションでは、分析の反復処理、単体テストの進展、およびリファクタリングが、実稼働のコードの堅牢性と有効性を高めるうえでどのように役立つかを説明します。

### <a name="analyze-the-issues"></a>問題を分析する

有効な金額が `Debit` メソッドで正しく差し引かれているかどうかを確認するテスト メソッドを作成しました。 引き落とし金額が次のいずれかである場合、メソッドが <xref:System.ArgumentOutOfRangeException> をスローすることを確認します。

- 残高よりも大きい、または
- 0 未満。

### <a name="create-and-run-new-test-methods"></a>新しいテスト メソッドを作成し、実行する

引き落とし金額が 0 未満の場合の正しい動作を検証するテスト メソッドを作成します。

```csharp
[TestMethod]
public void Debit_WhenAmountIsLessThanZero_ShouldThrowArgumentOutOfRange()
{
    // Arrange
    double beginningBalance = 11.99;
    double debitAmount = -100.00;
    BankAccount account = new BankAccount("Mr. Bryan Walton", beginningBalance);

    // Act and assert
    Assert.ThrowsException<System.ArgumentOutOfRangeException>(() => account.Debit(debitAmount));
}
```

<xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert.ThrowsException%2A> メソッドを使用して、正しい例外がスローされたことをアサートします。 このメソッドを使用した場合、<xref:System.ArgumentOutOfRangeException> がスローされない限り、テストは失敗します。 引き落とし金額が 0 未満の場合、より汎用的な <xref:System.ApplicationException> をスローするようにテスト対象のメソッドを一時的に変更すると、テストは正しく動作します。つまり失敗します。

引き出し金額が残高を上回るケースをテストするには、次の手順を実行します。

1. `Debit_WhenAmountIsMoreThanBalance_ShouldThrowArgumentOutOfRange`という新しいテスト メソッドを作成します。

2. メソッド本体を `Debit_WhenAmountIsLessThanZero_ShouldThrowArgumentOutOfRange` から新しいメソッドにコピーします。

3. `debitAmount` を、残高を上回る数値に設定します。

2 つのテストを実行し、合格することを確認します。

### <a name="continue-the-analysis"></a>分析を継続する

テスト対象のメソッドは、さらに改善できます。 現在の実装では、テスト中にスローされた例外を招いた条件 (`amount > m_balance` または `amount < 0`) を把握する方法はありません。 メソッドのどこかで `ArgumentOutOfRangeException` がスローされたことしかわかりません。 メソッドでその引数が正しくサニティ チェックされていることを確信できるように、`BankAccount.Debit` 内の例外をスローさせた条件 (`amount > m_balance` または `amount < 0`) がわかる方がよいと考えます。

テスト対象のメソッド (`BankAccount.Debit`) をもう一度確認すると、引数の名前をパラメーターとして使用する `ArgumentOutOfRangeException` コンストラクターが両方の条件ステートメントで使用されていることがわかります。

```csharp
throw new ArgumentOutOfRangeException("amount");
```

さらに豊富な情報を報告するために使用できるコンストラクターがあります。<xref:System.ArgumentOutOfRangeException.%23ctor(System.String,System.Object,System.String)> には、引数の名前、引数の値、ユーザー定義のメッセージが含まれています。 このコンストラクターを使用するようにテスト対象のメソッドをリファクタリングできます。 さらに、一般に公開されている型メンバーを使用して、エラーを指定できます。

### <a name="refactor-the-code-under-test"></a>テスト対象のコードをリファクタリングする

最初に、エラー メッセージの 2 つの定数をクラス スコープで定義します。 これらを `BankAccount` テスト対象のクラスに入れます。

```csharp
public const string DebitAmountExceedsBalanceMessage = "Debit amount exceeds balance";
public const string DebitAmountLessThanZeroMessage = "Debit amount is less than zero";
```

次に、`Debit` メソッドの 2 つの条件ステートメントを変更します。

```csharp
if (amount > m_balance)
{
    throw new System.ArgumentOutOfRangeException("amount", amount, DebitAmountExceedsBalanceMessage);
}

if (amount < 0)
{
    throw new System.ArgumentOutOfRangeException("amount", amount, DebitAmountLessThanZeroMessage);
}
```

### <a name="refactor-the-test-methods"></a>テスト メソッドをリファクタリングする

<xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert.ThrowsException%2A?displayProperty=nameWithType> への呼び出しを削除して、テスト メソッドをリファクタリングします。 `try/catch` ブロックで `Debit()` への呼び出しをラップし、期待される特定の例外をキャッチして、それに関連したメッセージを確認します。 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.StringAssert.Contains%2A?displayProperty=fullName> メソッドには、2 つの文字列を比較する機能があります。

`Debit_WhenAmountIsMoreThanBalance_ShouldThrowArgumentOutOfRange` は次のようになります。

```csharp
[TestMethod]
public void Debit_WhenAmountIsMoreThanBalance_ShouldThrowArgumentOutOfRange()
{
    // Arrange
    double beginningBalance = 11.99;
    double debitAmount = 20.0;
    BankAccount account = new BankAccount("Mr. Bryan Walton", beginningBalance);

    // Act
    try
    {
        account.Debit(debitAmount);
    }
    catch (System.ArgumentOutOfRangeException e)
    {
        // Assert
        StringAssert.Contains(e.Message, BankAccount.DebitAmountExceedsBalanceMessage);
    }
}
```

### <a name="retest-rewrite-and-reanalyze"></a>再テストする、書き換える、再分析する

テスト対象のメソッドにバグがあっても `Debit` メソッドが <xref:System.ArgumentOutOfRangeException> をスローせず、例外と共に正しいメッセージを出力するとします。 現在、テスト メソッドはこのケースを処理しません。 `debitAmount` の値が有効な場合 (つまり、残高未満で 0 よりは大きい場合)、例外はキャッチされないので、アサートはキャッチされません。 それでも、テスト メソッドは成功します。 これは適切ではありません。例外がスローされない場合はテスト メソッドが失敗することを想定しているためです。

これはテスト メソッドのバグです。 この問題を解決するには、テスト メソッドの最後に <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert.Fail%2A> アサートを追加して、例外がスローされないケースを処理するようにします。

テストを再実行すると、正しい例外がキャッチされた場合にテストが*失敗*したことが示されます。 `catch` ブロックは例外をキャッチしますが、メソッドは引き続き実行され、新しい <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert.Fail%2A> アサート時に失敗します。 この問題を解決するには、`catch` ブロックの `StringAssert` の後に `return` ステートメントを追加します。 テストを再実行して、この問題が解決したことを確認します。 `Debit_WhenAmountIsMoreThanBalance_ShouldThrowArgumentOutOfRange` の最終バージョンは、次のようになります。

```csharp
[TestMethod]
public void Debit_WhenAmountIsMoreThanBalance_ShouldThrowArgumentOutOfRange()
{
    // Arrange
    double beginningBalance = 11.99;
    double debitAmount = 20.0;
    BankAccount account = new BankAccount("Mr. Bryan Walton", beginningBalance);

    // Act
    try
    {
        account.Debit(debitAmount);
    }
    catch (System.ArgumentOutOfRangeException e)
    {
        // Assert
        StringAssert.Contains(e.Message, BankAccount.DebitAmountExceedsBalanceMessage);
        return;
    }

    Assert.Fail("The expected exception was not thrown.");
}
```

### <a name="conclusion"></a>まとめ

テスト コードを改善することで、より堅牢で有益なテスト方法になりました。 ただし、もっと重要な点は、テスト対象のコードも改善されたことです。

> [!TIP]
> このチュートリアルでは、マネージド コード用の Microsoft 単体テスト フレームワークを使用します。 また、**テスト エクスプローラー**用のアダプターを備えたサード パーティの単体テスト フレームワークから**テスト エクスプローラー**を実行することもできます。 詳細については、「[サードパーティ製の単体テスト フレームワークをインストールする](../test/install-third-party-unit-test-frameworks.md)」をご覧ください。

## <a name="see-also"></a>関連項目

コマンド ラインからテストを実行する方法については、「[VSTest.Console.exe のコマンド ライン オプション](vstest-console-options.md)」を参照してください。
