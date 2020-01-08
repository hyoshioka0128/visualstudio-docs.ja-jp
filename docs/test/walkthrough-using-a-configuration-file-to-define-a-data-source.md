---
title: データ ソースを定義するための構成ファイルの使用
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- configuration files [Visual Studio ALM], defining data sources
- unit tests, walkthrough
- data sources, defining with configuration files
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c76d71c106dbd2b5cbe63ab2f36defdfbd6cf127
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75590723"
---
# <a name="walkthrough-using-a-configuration-file-to-define-a-data-source"></a>チュートリアル: データ ソースを定義するための構成ファイルの使用

このチュートリアルでは、単体テスト用に *app.config* ファイルで定義されたデータ ソースを使用する方法について説明します。 ここでは、<xref:Microsoft.VisualStudio.TestTools.UnitTesting.DataSourceAttribute> クラスで使用できるデータ ソースを定義する *app.config* ファイルの作成方法を学習します。 このチュートリアルでは、次のタスクについて説明します。

- *app.config* ファイルを作成する。

- カスタム構成セクションを定義する。

- 接続文字列を定義する。

- データ ソースを定義する。

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.DataSourceAttribute> クラスを使用してデータ ソースにアクセスする。

## <a name="prerequisites"></a>必須コンポーネント

このチュートリアルを完了するには、次の条件が必要です。

- Visual Studio Enterprise

- 少なくとも 1 つのテスト メソッドにデータを提供する Microsoft Access または Microsoft Excel

- テスト プロジェクトを含む Visual Studio ソリューション

## <a name="add-an-appconfig-file-to-the-project"></a>app.config ファイルをプロジェクトに追加する

1. テスト プロジェクトに既に *app.config* ファイルが存在する場合は、「[カスタム構成セクションを定義する](#define-a-custom-configuration-section)」に進みます。

2. **ソリューション エクスプローラー**で、テスト プロジェクトを右クリックし、 **[追加]**  >  **[新しい項目]** の順に選択します。

     **[新しい項目の追加]** ウィンドウが開きます。

3. **[アプリケーション構成ファイル]** テンプレートを選択し、 **[追加]** をクリックします。

## <a name="define-a-custom-configuration-section"></a>カスタム構成セクションを定義する

*app.config* ファイルを確認します。 少なくとも XML 宣言とルート要素が含まれています。

### <a name="to-add-the-custom-configuration-section-to-the-appconfig-file"></a>app.config ファイルにカスタム構成セクションを追加するには

1. *app.config* のルート要素は **configuration** 要素である必要があります。 **configuration** 要素内に **configSections** 要素を作成します。 **configSections** は、*app.config* ファイル内で最初の要素である必要があります。

2. **configSections** 要素内に **section** 要素を作成します。

3. **section** 要素に、`name` という属性を追加し、その属性に `microsoft.visualstudio.testtools` の値を割り当てます。 `type` という別の属性を追加し、その属性に `Microsoft.VisualStudio.TestTools.UnitTesting.TestConfigurationSection, Microsoft.VisualStudio.TestPlatform.TestFramework.Extensions` の値を割り当てます。

**section** 要素は次のようになります。

```xml
<section name="microsoft.visualstudio.testtools" type="Microsoft.VisualStudio.TestTools.UnitTesting.TestConfigurationSection, Microsoft.VisualStudio.TestPlatform.TestFramework.Extensions" />
```

> [!NOTE]
> アセンブリ名は、使用しているバージョンと一致する必要があります。

## <a name="define-connection-strings"></a>接続文字列を定義する

接続文字列は、データ ソースにアクセスするためのプロバイダー固有の情報を定義します。 構成ファイルで定義された接続文字列は、アプリケーション全体で再利用可能なデータ プロバイダー情報を提供します。 このセクションでは、カスタム構成セクションで定義されているデータ ソースによって使用される 2 つの接続文字列を作成します。

### <a name="to-define-connection-strings"></a>接続文字列を定義するには

1. **configSections** 要素の後に **connectionStrings** 要素を作成します。

2. **connectionStrings** 要素内に 2 つの **add** 要素を作成します。

3. 1 つ目の **add** 要素には、Microsoft Access データベースに接続するための次の属性と値を作成します。

|属性|値|
|-|------------|
|`name`|`"MyJetConn"`|
|`connectionString`|`"Provider=Microsoft.Jet.OLEDB.4.0; Data Source=C:\testdatasource.accdb; Persist Security Info=False;"`|
|`providerName`|`"System.Data.OleDb"`|

2 つ目の **add** 要素には、Microsoft Excel スプレッドシートに接続するための次の属性と値を作成します。

|属性|値|
|-|-|
|`name`|`"MyExcelConn"`|
|`connectionString`|`"Dsn=Excel Files;dbq=data.xlsx;defaultdir=.\; driverid=790;maxbuffersize=2048;pagetimeout=5"`|
|`providerName`|`"System.Data.Odbc"`|

**connectionStrings** 要素は次のようになります。

```xml
<connectionStrings>
    <add name="MyJetConn" connectionString="Provider=Microsoft.Jet.OLEDB.4.0; Data Source=C:\testdatasource.accdb; Persist Security Info=False;" providerName="System.Data.OleDb" />
    <add name="MyExcelConn" connectionString="Dsn=Excel Files;dbq=data.xlsx;defaultdir=.\; driverid=790;maxbuffersize=2048;pagetimeout=5" providerName="System.Data.Odbc" />
</connectionStrings>
```

## <a name="define-data-sources"></a>データ ソースを定義する

データ ソース セクションには、テスト エンジンがデータ ソースからデータを取得するために使用する 4 つの属性が含まれます。

- `name` は、使用するデータ ソースを指定するために <xref:Microsoft.VisualStudio.TestTools.UnitTesting.DataSourceAttribute> で使用される ID を定義します。

- `connectionString` は、前の「接続文字列を定義する」セクションで作成した接続文字列を識別します。

- `dataTableName` は、テストで使用するデータを保持するテーブルまたはシートを定義します。

- `dataAccessMethod` は、データ ソース内のデータ値にアクセスする方法を定義します。

ここでは、単体テストで使用する 2 つのデータ ソースを定義します。

### <a name="to-define-data-sources"></a>データ ソースを定義するには

1. **connectionStrings** 要素の後に、**microsoft.visualstudio.testtools** 要素を作成します。 この部分は、「カスタム構成セクションを定義する」セクションで作成されています。

2. **microsoft.visualstudio.testtools** 要素内に **dataSources** 要素を作成します。

3. **dataSources** 要素内に 2 つの **add** 要素を作成します。

4. 1 つ目の **add** 要素には、Microsoft Access データ ソース用の次の属性と値を作成します。

|属性|値|
|-|------------|
|`name`|`"MyJetDataSource"`|
|`connectionString`|`"MyJetConn"`|
|`dataTableName`|`"MyDataTable"`|
|`dataAccessMethod`|`"Sequential"`|

2 つ目の **add** 要素には、Microsoft Excel データ ソース用の次の属性と値を作成します。

|属性|値|
|-|-|
|`Name`|`"MyExcelDataSource"`|
|`connectionString`|`"MyExcelConn"`|
|`dataTableName`|`"Sheet1$"`|
|`dataAccessMethod`|`"Sequential"`|

**microsoft.visualstudio.testtools** 要素は次のようになります。

```xml
<microsoft.visualstudio.testtools>
    <dataSources>
        <add name="MyJetDataSource" connectionString="MyJetConn" dataTableName="MyDataTable" dataAccessMethod="Sequential"/>
        <add name="MyExcelDataSource" connectionString="MyExcelConn" dataTableName="Sheet1$" dataAccessMethod="Sequential"/>
    </dataSources>
</microsoft.visualstudio.testtools>
```

最終的な *app.config* ファイルは次のようになります。

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <configSections>
        <section name="microsoft.visualstudio.testtools" type="Microsoft.VisualStudio.TestTools.UnitTesting.TestConfigurationSection, Microsoft.VisualStudio.QualityTools.UnitTestFramework, Version=8.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a"/>
    </configSections>
    <connectionStrings>
        <add name="MyJetConn" connectionString="Provider=Microsoft.Jet.OLEDB.4.0; Data Source=C:\testdatasource.accdb; Persist Security Info=False;" providerName="System.Data.OleDb" />
        <add name="MyExcelConn" connectionString="Dsn=Excel Files;dbq=data.xlsx;defaultdir=.\; driverid=790;maxbuffersize=2048;pagetimeout=5" providerName="System.Data.Odbc" />
    </connectionStrings>
    <microsoft.visualstudio.testtools>
        <dataSources>
            <add name="MyJetDataSource" connectionString="MyJetConn" dataTableName="MyDataTable" dataAccessMethod="Sequential"/>
            <add name="MyExcelDataSource" connectionString="MyExcelConn" dataTableName="Sheet1$" dataAccessMethod="Sequential"/>
        </dataSources>
    </microsoft.visualstudio.testtools>
</configuration>
```

## <a name="create-a-unit-test-that-uses-data-sources-defined-in-appconfig"></a>app.config で定義したデータ ソースを使用する単体テストを作成する

*app.config* ファイルの定義が完了したところで、*app.config* ファイルで定義されているデータ ソース内にあるデータを使用する単体テストを作成します。 このセクションでは、次のタスクを実行します。

- *app.config* ファイルにあるデータ ソースを作成する。

- 各データ ソースの値を比較する 2 つのテスト メソッド内のデータ ソースを使用する。

### <a name="to-create-a-microsoft-access-data-source"></a>Microsoft Access データ ソースを作成するには

1. *testdatasource.accdb* という名前の Microsoft Access データベースを作成します。

2. *testdatasource.accdb* 内にテーブルを作成し、`MyDataTable` と名前を付けます。

3. `Number` データ型を使用して、`MyDataTable` に `Arg1` と `Arg2` という名前の 2 つのフィールドを作成します。

4. 5 つのエンティティを `MyDataTable` に追加します。`Arg1` と `Arg2` の値は、それぞれ(10,50)、(3,2)、(6,0)、(0,8)、(12312,1000) となるようにします。

5. データベースを保存して閉じます。

6. データベースの場所を指すように接続文字列を変更します。 データベースの場所を反映するように `Data Source` の値を変更します。

### <a name="to-create-a-microsoft-excel-data-source"></a>Microsoft Excel データ ソースを作成するには

1. *data.xlsx* という名前の Microsoft Excel スプレッドシートを作成します。

2. `Sheet1` という名前のシートが *data.xlsx* にまだ存在しない場合は作成します。

3. `Sheet1` に 2 つの列ヘッダーを作成し、`Val1` と `Val2` という名前を付けます。

4. 5 つのエンティティを `Sheet1` に追加します。`Val1` と `Val2` の値は、それぞれ(1,1)、(2,2)、(3,3)、(4,4)、(5,0) となるようにします。

5. スプレッドシートを保存して閉じます。

6. スプレッドシートの場所を指すように接続文字列を変更します。 スプレッドシートの場所を反映するように `dbq` の値を変更します。

### <a name="to-create-a-unit-test-using-the-appconfig-data-sources"></a>app.config のデータ ソースを使用して単体テストを作成するには

1. 単体テストをテスト プロジェクトに追加します。

2. 自動生成された単体テストの内容を次のコードに置き換えます。

    ```csharp
    using System;
    using Microsoft.VisualStudio.TestTools.UnitTesting;

    namespace TestProject1
    {
         [TestClass]
        public class UnitTest1
        {
            private TestContext context;

            public TestContext TestContext
            {
                get { return context; }
                set { context = value; }
            }

            [TestMethod()]
            [DeploymentItem("MyTestProject\\testdatasource.accdb")]
            [DataSource("MyJetDataSource")]
            public void MyTestMethod()
            {
                int a = Int32.Parse(context.DataRow["Arg1"].ToString());
                int b = Int32.Parse(context.DataRow["Arg2"].ToString());
                Assert.AreNotEqual(a, b, "A value was equal.");
            }

            [TestMethod()]
            [DeploymentItem("MyTestProject\\data.xlsx")]
            [DataSource("MyExcelDataSource")]
            public void MyTestMethod2()
            {
                Assert.AreEqual(context.DataRow["Val1"], context.DataRow["Val2"]);
            }
        }
    }
    ```

3. DataSource 属性を確認します。 *app.config* ファイルの設定名に注意してください。

4. ソリューションをビルドして、MyTestMethod テストと MyTestMethod2 テストを実行します。

> [!IMPORTANT]
> データ ソースなどの項目を、配置ディレクトリのテストからアクセスできるように配置します。

## <a name="see-also"></a>関連項目

- [コードの単体テスト](../test/unit-test-your-code.md)
- [方法: データ ドリブン単体テストを作成する](../test/how-to-create-a-data-driven-unit-test.md)
