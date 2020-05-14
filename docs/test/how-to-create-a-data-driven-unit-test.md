---
title: データ ドリブン単体テストを作成する
ms.date: 05/08/2019
ms.topic: conceptual
f1_keywords:
- vs.test.testresults.unittest.datadriven
- vs.test.testresults.unittest.datadriven.failure
helpviewer_keywords:
- unit tests, running
- unit tests, data-driven
- data-driven unit tests
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
author: mikejo5000
ms.openlocfilehash: f50dad637d9efa2db347ff9f1b4828abf8c733af
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "75589189"
---
# <a name="how-to-create-a-data-driven-unit-test"></a>方法: データ ドリブン単体テストを作成する

マネージド コード用の Microsoft 単体テスト フレームワークを使用し、データ ソースから値を取得する単体テスト メソッドを設定できます。 メソッドはデータ ソース内の各行に対して連続して実行されるため、単一のメソッドを使用してさまざまな入力を簡単にテストできます。

データ ドリブン単体テストの作成には、次の手順が含まれます。

1. テスト メソッドで使用する値を含むデータ ソースを作成します。 データ ソースは、テストを実行するコンピューターに登録されている任意の型にすることができます。

2. プライベート <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestContext> フィールドとパブリック `TestContext` プロパティをテスト クラスに追加します。

3. 単体テスト メソッドを作成し、それを <xref:Microsoft.VisualStudio.TestTools.UnitTesting.DataSourceAttribute> 属性に追加します。

4. <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestContext.DataRow%2A> インデクサー プロパティを使用して、テストで使用する値を取得します。

## <a name="the-method-under-test"></a>テスト対象のメソッド

たとえば、次が用意されています。

1. さまざまな種類の勘定のトランザクションを受け入れて処理する `MyBank` というソリューション。

2. 勘定のトランザクションを管理する `BankDb` という `MyBank` 内のプロジェクト。

3. トランザクションが必ず銀行にとって有利になるように数値演算関数を実行する `BankDb` プロジェクト内の `Maths` というクラス。

4. `BankDb` コンポーネントの動作をテストする `BankDbTests` という単体テスト プロジェクト。

5. `Maths` クラスの動作を確認する `MathsTests` という単体テスト クラス。

ループを使用して 2 つの整数を追加する `Maths` のメソッドをテストします。

```csharp
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

## <a name="create-a-data-source"></a>データ ソースの作成

`AddIntegers` メソッドをテストするには、パラメーターの値の範囲と返される必要のある合計を指定するデータ ソースを作成します。 この例では、`MathsData` という名前の Sql Compact データベースと、次の列の名前と値を含む `AddIntegersData` という名前のテーブルを作成します

|FirstNumber|SecondNumber|Sum|
|-|------------------|-|
|0|1|1|
|1|1|2|
|2|-3|-1|

## <a name="add-a-testcontext-to-the-test-class"></a>テスト クラスへの TestContext の追加

単体テスト フレームワークは、データ ドリブン テストのデータ ソース情報を格納する `TestContext` オブジェクトを作成します。 次に、フレームワークは作成する `TestContext` プロパティの値としてこのオブジェクトを設定します。

```csharp
private TestContext testContextInstance;
public TestContext TestContext
{
    get { return testContextInstance; }
    set { testContextInstance = value; }
}
```

テスト メソッドでは、`TestContext` の `DataRow` インデクサー プロパティを使用してデータにアクセスします。

> [!NOTE]
> .NET Core では [DataSource](xref:Microsoft.VisualStudio.TestTools.UnitTesting.DataSourceAttribute) 属性がサポートされていません。 .NET Core または UWP 単体テスト プロジェクトでこの方法でテスト データにアクセスしようとすると、 **"'TestContext' does not contain a definition for 'DataRow' and no accessible extension method 'DataRow' accepting a first argument of type 'TestContext' could be found (are you missing a using directive or an assembly reference?)"** ('TestContext' に 'DataRow' の定義が含まれておらず、型 'TestContext' の最初の引数を受け取るアクセス可能な拡張メソッド 'DataRow' が見つかりません (using ディレクティブかアセンブリ参照が不足していませんか?)) のようなエラーが表示されます。

## <a name="write-the-test-method"></a>テスト メソッドの記述

`AddIntegers` のテスト メソッドは非常に単純です。 データ ソース内の各行に対して、パラメーターとして **FirstNumber** 列値と **SecondNumber** 列値を持つ `AddIntegers` を呼び出して、**Sum** 列値に対して戻り値を確認します。

```csharp
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

`Assert` メソッドには、失敗したイテレーションの `x` と `y` の値を表示するメッセージが含まれます。 既定では、アサートされた値である `expected` と `actual` が失敗したテストの詳細に既に含まれています。

### <a name="specify-the-datasourceattribute"></a>DataSourceAttribute の指定

`DataSource` 属性は、データ ソースの接続文字列とテスト メソッドで使用するテーブル名を指定します。 接続文字列の正確な情報は、使用しているデータ ソースの種類によって異なります。 この例では、SqlServerCe データベースを使用しました。

```csharp
[DataSource(@"Provider=Microsoft.SqlServerCe.Client.4.0;Data Source=C:\Data\MathsData.sdf", "AddIntegersData")]
```

DataSource 属性には 3 つのコンストラクターがあります。

```csharp
[DataSource(dataSourceSettingName)]
```

1 つのパラメーターを持つコンストラクターは、ソリューションの *app.config* ファイルに格納されている接続情報を使用します。 *dataSourceSettingsName* は、接続情報を指定する構成ファイル内の Xml 要素の名前です。

*app.config* ファイルを使用すると、単体テスト自体に変更を加えずに、データ ソースの場所を変更できます。 *app.config* ファイルの作成および使用方法の詳細については、「[チュートリアル: データ ソースを定義するための構成ファイルの使用](../test/walkthrough-using-a-configuration-file-to-define-a-data-source.md)」を参照してください

```csharp
[DataSource(connectionString, tableName)]
```

2 つのパラメーターを持つ `DataSource` コンストラクターは、データ ソースの接続文字列とテスト メソッドのデータを含むテーブルの名前を指定します。

接続文字列は、データ ソースの種類によって異なりますが、データ プロバイダーの不変名を指定する Provider 要素を含んでいる必要があります。

```csharp
[DataSource(
    dataProvider,
    connectionString,
    tableName,
    dataAccessMethod
    )]
```

### <a name="use-testcontextdatarow-to-access-the-data"></a>データにアクセスするための TestContext.DataRow の使用

`AddIntegersData` テーブル内のデータにアクセスするには、`TestContext.DataRow` インデクサーを使用します。 `DataRow` は、<xref:System.Data.DataRow> オブジェクトであるため、インデックスまたは列の名前で列の値を取得します。 値はオブジェクトとして返されるため、適切な型に変換します。

```csharp
int x = Convert.ToInt32(TestContext.DataRow["FirstNumber"]);
```

## <a name="run-the-test-and-view-results"></a>テストを実行して結果を表示する

テスト メソッドの記述が完了したら、テスト プロジェクトを構築します。 **[テストを実行しない]** グループの**テスト エクスプローラー**に、テスト メソッドが表示されます。 テストを実行して、記述し、再実行すると、**テスト エクスプローラー**に **[失敗したテスト]** 、 **[成功したテスト]** 、 **[テストを実行しない]** のグループの結果が表示されます。 **[すべて実行]** を選択してテストをすべて実行することも、 **[実行]** を選択してテストのサブセットを実行することもできます。

テストの実行中は、**テスト エクスプローラー**の上部にあるテスト結果バーがアニメーションで表示されます。 テストの実行の終了時に、すべてのテストが成功した場合はバーが緑色になり、いずれかのテストが失敗した場合は赤色になります。 **テスト エクスプローラー** ウィンドウの下部の詳細ウィンドウに、テストの実行の概要が表示されます。 テストを選択すると、そのテストの詳細が下部のペインに表示されます。

> [!NOTE]
> データの各行に対する結果と、1 つのサマリー結果もあります。 データの各行のテストが合格すると、サマリー実行は **[合格]** と表示されます。 いずれかのデータ行のテストが失敗すると、サマリー実行は **[失敗]** と表示されます。

この例で `AddIntegers_FromDataSourceTest` メソッドを実行した場合、結果バーが赤に変わり、テスト メソッドが **[失敗したテスト]** に移動されます。 データ ソースからの反復されたメソッドのいずれかが失敗した場合は、データ ドリブン テストは失敗します。 **テスト エクスプローラー** ウィンドウで、失敗したデータ ドリブン テストを選択すると、詳細ウィンドウにはデータ行インデックスによって識別される各イテレーションの結果が表示されます。 この例では、`AddIntegers` アルゴリズムが負の値を正しく処理していないことがわかります。

テスト対象のメソッドを修正して、テストを再実行すると、結果バーが緑に変わり、テスト メソッドは **[成功したテスト]** グループに移動されます。

## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.DataSourceAttribute?displayProperty=fullName>
- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestContext?displayProperty=fullName>
- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestContext.DataRow%2A?displayProperty=fullName>
- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert?displayProperty=fullName>
- [コードの単体テスト](../test/unit-test-your-code.md)
- [テスト エクスプローラーを使用して単体テストを実行する](../test/run-unit-tests-with-test-explorer.md)
- [Microsoft 単体テスト フレームワークを使用した .NET 用単体テストの記述](../test/unit-test-your-code.md)
