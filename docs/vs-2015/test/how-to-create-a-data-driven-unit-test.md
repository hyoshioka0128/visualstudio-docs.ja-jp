---
title: '方法: データ ドリブン単体テストを作成する | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-test
ms.topic: conceptual
f1_keywords:
- vs.test.testresults.unittest.datadriven
- vs.test.testresults.unittest.datadriven.failure
helpviewer_keywords:
- unit tests, running
- unit tests, data-driven
- data-driven unit tests
ms.assetid: a0322bc5-02c8-4f9f-af43-100a60b1bd28
caps.latest.revision: 35
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: b9dc5ad44a73f517b91562209abfab8b0b3e8d4a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72660535"
---
# <a name="how-to-create-a-data-driven-unit-test"></a>方法: データ ドリブン単体テストを作成する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

マネージド コード用の Microsoft の単体テスト フレームワークを使用して、データ ソースからテスト メソッドで使用される値を取得するための単体テスト メソッドを設定できます。 メソッドはデータ ソース内の各行に対して連続して実行されるため、単一のメソッドを使用してさまざまな入力を簡単にテストできます。

 このトピックには、次のセクションが含まれます。

- [テスト対象のメソッド](../test/how-to-create-a-data-driven-unit-test.md#BKMK_The_method_under_test)

- [データソースの作成](../test/how-to-create-a-data-driven-unit-test.md#BKMK_Creating_a_data_source)

- [テスト クラスへの TestContext の追加](../test/how-to-create-a-data-driven-unit-test.md#BKMK_Adding_a_TestContext_to_the_test_class)

- [テスト メソッドの記述](../test/how-to-create-a-data-driven-unit-test.md#BKMK_Writing_the_test_method)

  - [DataSourceAttribute の指定](../test/how-to-create-a-data-driven-unit-test.md#BKMK_Specifying_the_DataSourceAttribute)

  - [データにアクセスするための TestContext.DataRow の使用](../test/how-to-create-a-data-driven-unit-test.md#BKMK_Using_TestContext_DataRow_to_access_the_data)

- [テストの実行と結果の表示](../test/how-to-create-a-data-driven-unit-test.md#BKMK_Running_the_test_and_viewing_results)

  データ ドリブン単体テストの作成には、次の手順が含まれます。

1. テスト メソッドで使用する値を含むデータ ソースを作成します。 データ ソースは、テストを実行するコンピューターに登録されている任意の型にすることができます。

2. プライベート <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestContext> フィールドとパブリック `TestContext` プロパティをテスト クラスに追加します。

3. 単体テスト メソッドを作成し、それを <xref:Microsoft.VisualStudio.TestTools.UnitTesting.DataSourceAttribute> 属性に追加します。

4. <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestContext.DataRow%2A> インデクサー プロパティを使用して、テストで使用する値を取得します。

## <a name="the-method-under-test"></a><a name="BKMK_The_method_under_test"></a>テスト対象のメソッド
 たとえば、次を作成したとします。

1. さまざまな種類の勘定のトランザクションを受け入れて処理する `MyBank` というソリューション。

2. 勘定のトランザクションを管理する `BankDb` という `MyBank` 内のプロジェクト。

3. トランザクションが必ず銀行にとって有利になるように数値演算関数を実行する `DbBank` プロジェクト内の `Maths` というクラス。

4. `BankDb` コンポーネントの動作をテストする `BankDbTests` という単体テスト プロジェクト。

5. `Maths` クラスの動作を確認する `MathsTests` という単体テスト クラス。

   ループを使用して 2 つの整数を追加する `Maths` のメソッドをテストします。

```
public int AddIntegers(int first, int second)
{
    int sum = first;
    for( int i = 0; i < second; i++)
    {
        sum += 1;
    }
    return sum;
}
```

## <a name="creating-a-data-source"></a><a name="BKMK_Creating_a_data_source"></a> データソースの作成
 `AddIntegers` メソッドをテストするには、パラメーターの値の範囲と返される必要のある合計を指定するデータ ソースを作成します。 この例では、`MathsData` という名前の Sql Compact データベースと、次の列の名前と値を含む `AddIntegersData` という名前のテーブルを作成します

|FirstNumber|SecondNumber|SUM|
|-----------------|------------------|---------|
|0|1|1|
|1|1|2|
|2|-3|-1|

## <a name="adding-a-testcontext-to-the-test-class"></a><a name="BKMK_Adding_a_TestContext_to_the_test_class"></a> テストクラスへの TestContext の追加
 単体テスト フレームワークは、データ ドリブン テストのデータ ソース情報を格納する `TestContext` オブジェクトを作成します。 次に、フレームワークは作成する `TestContext` プロパティの値としてこのオブジェクトを設定します。

```

private TestContext testContextInstance;
public TestContext TestContext
{
    get { return testContextInstance; }
    set { testContextInstance = value; }
}

```

 テスト メソッドでは、`TestContext` の `DataRow` インデクサー プロパティを使用してデータにアクセスします。

## <a name="writing-the-test-method"></a><a name="BKMK_Writing_the_test_method"></a> テストメソッドの記述
 `AddIntegers` のテスト メソッドは非常に単純です。 データ ソース内の各行に対して、パラメーターとして **FirstNumber** 列値と **SecondNumber** 列値を持つ `AddIntegers` を呼び出して、**Sum** 列値に対して戻り値を確認します。

```

[DataSource(@"Provider=Microsoft.SqlServerCe.Client.4.0; Data Source=C:\Data\MathsData.sdf;", "Numbers")]
[TestMethod()]
public void AddIntegers_FromDataSourceTest()
{
    var target = new Maths();

    // Access the data
    int x = Convert.ToInt32(TestContext.DataRow["FirstNumber"]);
    int y = Convert.ToInt32(TestContext.DataRow["SecondNumber"]);
    int expected = Convert.ToInt32(TestContext.DataRow["Sum"]);
    int actual = target.IntegerMethod(x, y);
    Assert.AreEqual(expected, actual,
        "x:<{0}> y:<{1}>",
        new object[] {x, y});

}

```

 `Assert` メソッドには、失敗したイテレーションの `x` と `y` の値を表示するメッセージが含まれることに注意してください。 既定では、アサートされた値である `expected` と `actual` が失敗したテストの詳細に既に含まれています。

### <a name="specifying-the-datasourceattribute"></a><a name="BKMK_Specifying_the_DataSourceAttribute"></a> DataSourceAttribute の指定
 `DataSource` 属性は、データ ソースの接続文字列とテスト メソッドで使用するテーブル名を指定します。 接続文字列の正確な情報は、使用しているデータ ソースの種類によって異なります。 この例では、SqlServerCe データベースを使用しました。

```
[DataSource(@"Provider=Microsoft.SqlServerCe.Client.4.0;Data Source=C:\Data\MathsData.sdf", "AddIntegersData")]
```

 DataSource 属性には 3 つのコンストラクターがあります。

```
[DataSource(dataSourceSettingName)]
```

 1 つのパラメーターを持つコンストラクターは、ソリューションの app.config ファイルに格納されている接続情報を使用します。 *dataSourceSettingsName* は、接続情報を指定する構成ファイル内の Xml 要素の名前です。

 app.config ファイルを使用すると、単体テスト自体に変更を加えずに、データ ソースの場所を変更できます。 app.config ファイルの作成と使用方法については、「[チュートリアル : データ ソースを定義するための構成ファイルの使用](../test/walkthrough-using-a-configuration-file-to-define-a-data-source.md)」を参照してください

```
[DataSource(connectionString, tableName)]
```

 2 つのパラメーターを持つ `DataSource` コンストラクターは、データ ソースの接続文字列とテスト メソッドのデータを含むテーブルの名前を指定します。

 接続文字列は、データ ソースの種類によって異なりますが、データ プロバイダーの不変名を指定する Provider 要素を含んでいる必要があります。

```
[DataSource(
    dataProvider,
    connectionString,
    tableName,
    dataAccessMethod
    )]
```

### <a name="using-testcontextdatarow-to-access-the-data"></a><a name="BKMK_Using_TestContext_DataRow_to_access_the_data"></a> TestContext を使用したデータへのアクセス
 `AddIntegersData` テーブル内のデータにアクセスするには、`TestContext.DataRow` インデクサーを使用します。 `DataRow` は、<xref:System.Data.DataRow> オブジェクトであるため、インデックスまたは列の名前で列の値を取得します。 値はオブジェクトとして返されるため、適切な型に変換する必要があります。

```
int x = Convert.ToInt32(TestContext.DataRow["FirstNumber"]);

```

## <a name="running-the-test-and-viewing-results"></a><a name="BKMK_Running_the_test_and_viewing_results"></a> テストの実行と結果の表示
 テスト メソッドの記述が完了したら、テスト プロジェクトを構築します。 **[テストを実行しない]** グループのテスト エクスプローラー ウィンドウに、テスト メソッドが表示されます。 テストを実行して、記述し、再実行すると、テスト エクスプローラーに **[失敗したテスト]**、**[成功したテスト]**、および **[テストを実行しない]** のグループの結果が表示されます。 [ **すべて実行** ] を選択してすべてのテストを実行するか、[ **実行.** ..] を選択して実行するテストのサブセットを選択できます。

 テストの実行中は、エクスプローラーの上部にあるテスト結果バーがアニメーションで表示されます。 テストの実行の終了時に、すべてのテストが成功した場合はバーが緑色になり、いずれかのテストが失敗した場合は赤色になります。 テスト エクスプローラー ウィンドウの下部の詳細ウィンドウに、テストの実行の概要が表示されます。 テストを選択すると、そのテストの詳細が下部のペインに表示されます。

 この例の `AddIntegers_FromDataSourceTest` メソッドを実行すると、結果バーが赤に変わり、テスト メソッドは **[失敗したテスト]** に移動されます。データ ソースからの反復されたメソッドのいずれかが失敗した場合は、データ ドリブン テストは失敗します。 テスト エクスプローラー ウィンドウで、失敗したデータ ドリブン テストを選択すると、詳細ウィンドウにはデータ行インデックスによって識別される各イテレーションの結果が表示されます。 この例では、`AddIntegers` アルゴリズムが負の値を正しく処理していないことがわかります。

 テスト対象のメソッドを修正して、テストを再実行すると、結果バーが緑に変わり、テスト メソッドは **[成功したテスト]** グループに移動されます。

## <a name="see-also"></a>参照
 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.DataSourceAttribute?displayProperty=fullName> <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestContext?displayProperty=fullName>
 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestContext.DataRow%2A?displayProperty=fullName>
 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert?displayProperty=fullName>
 [方法: 単体テストの単体テストを作成し](https://msdn.microsoft.com/5e0f43cf-5e51-48e2-9c98-0eb9324bdc48)[て](../test/unit-test-your-code.md)実行するコードを[実行するテストエクスプローラーで単体テスト](../test/run-unit-tests-with-test-explorer.md)を作成する[マネージコード用の Microsoft 単体テストフレームワークを使用して .NET Framework の単体テストを記述](../test/writing-unit-tests-for-the-dotnet-framework-with-the-microsoft-unit-test-framework-for-managed-code.md)する
