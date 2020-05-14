---
title: SQL Server と R の統合
description: Visual Studio では、R から SQL クエリを作成して実行したり、ストアド プロシージャを使ったりすることができます。
ms.date: 06/25/2018
ms.topic: conceptual
author: kraigb
ms.author: kraigb
manager: jillfra
ms.workload:
- data-science
ms.openlocfilehash: 10b5dfee629b5b6e67ab544ca0bdd905ed2a120a
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "72888456"
---
# <a name="work-with-sql-server-and-r"></a>SQL Server と R の使用

Visual Studio の優れた SQL Server のサポートにより、データ サイエンティストは、SQL クエリを作成して実行する機能およびストアド プロシージャを処理する機能を利用して、R と SQL データベースを使用することができます。

> [!Note]
> SQL と R を一緒に使用するためには、SQL Server Tools がインストールされている必要があります。
> - Visual Studio 2017: Visual Studio のインストーラーを実行し、データの保存と処理のワークロードを選択して、SQL Server Data Tools を追加します。
> - Visual Studio 2015: 「[Download SQL Server Data Tools](/sql/ssdt/download-sql-server-data-tools-ssdt)」 (SQL Server Data Tools のダウンロード) にある手順に従ってください。

|   |   |
|---|---|
| ![ビデオのムービー カメラ アイコン](../install/media/video-icon.png "ビデオを見る") | SQL Server と R の概要に関する[ビデオを見る (youtube.com)](https://www.youtube.com/watch?v=n4AYr0QIwdQ) (3 分 03 秒)。 |

## <a name="create-and-run-sql-queries"></a>SQL クエリの作成と実行

RTVS では R プロジェクトへの SQL クエリの追加がサポートされており、求める結果が得られるまで、別のコンテキストで SQL クエリの反復開発を行うことができます。

SQL クエリ ファイルを追加するには、ソリューション エクスプローラーでプロジェクトを右クリックし、 **[追加]**  >  **[新しい項目]** を選択して、ファイルの種類として **[SQL クエリ]** を選択します。

![SQL クエリ項目をプロジェクトに追加](media/sql-add-item.png)

このコマンドにより、Visual Studio の Transact-SQL エディターでファイルが開き、SQL 用のフル機能 IntelliSense とクエリ実行機能を使用できます。 ただし、これらの機能が動作するためには、エディターのツール バーにある接続ボタンを使用してデータベースに接続するか、クエリの実行を試みる必要があります (**Ctrl**+**Shift**+**E** キーでも選択項目を操作できます)。 どちらの方法でも、次のような接続ダイアログが表示されます。

![SQL 接続ダイアログ ボックス](media/sql-connection-dialog.png)

接続できたら、クエリを実行して結果を確認できます。

![SQL ウィンドウのクエリ結果](media/sql-query-results.png)

Transact-SQL エディターは他のさまざまな機能をサポートしており、たとえばクエリやクエリ デバッガーの実行プランを表示することなどができます。
詳しくは、「[Transact-SQL エディターを使用したスクリプトの編集と実行](https://msdn.microsoft.com/library/hh272706.aspx)」をご覧ください。

## <a name="work-with-sql-server-stored-procedures"></a>SQL Server ストアド プロシージャの使用

[SQL Server R Services](/sql/advanced-analytics/r/sql-server-r-services) (SQL Server 2016 以降) では、T-SQL ストアド プロシージャから R コードを埋め込んで実行できます。 R コードを SQL Server コンピューターで実行し、SQL クエリから返されたデータを操作して、SQL 結果セットを生成できます。結果セットは、さらに SQL で処理するか、クライアントに返すことができます。

以下のセクションで説明するように、RTVS は、1 つの SQL ステートメント内で SQL と R コードを組み合わせるという面倒でエラーが発生しやすいプロセスを単純化します。

- [データベース接続の追加](#add-a-database-connection)
- [SQL ストアド プロシージャの作成とテスト](#write-and-test-a-sql-stored-procedure)
- [SQL ストアド プロシージャの公開](#publish-a-sql-stored-procedure)

|   |   |
|---|---|
| ![ビデオのムービー カメラ アイコン](../install/media/video-icon.png "ビデオを見る") | R と SQL ストアド プロシージャの概要に関する[ビデオを見る (youtube.com)](https://www.youtube.com/watch?v=dFKIT2OitWQ) (6 分 09 秒)。 |

### <a name="add-a-database-connection"></a>データベース接続の追加

1. **[R Tools]**  >  **[データ]**  >  **[データベース接続の追加]** を選び、 **[接続のプロパティ]** ダイアログを表示します。 ここで、データ ソース (この場合は SQL Server) の名前、サーバーの名前、認証モード、データベースの名前を指定します。 ダイアログ ボックスを閉じる前に **[テスト接続]** を選んで入力を確認します。

    ![SQL 接続ダイアログ ボックス](media/sql-connection-string-dialog.png)

1. 有効な接続で **[OK]** を選択すると、Visual Studio で新しい *settings.R* ファイル内に `dbConnection` という有効な接続が生成されます。 このファイルが RTVS で自動的にソースとして実行され、R スクリプトから接続をすぐに使用できるようになります。

![SQL 設定の R ファイル](media/sql-settings-dot-r.png)

### <a name="write-and-test-a-sql-stored-procedure"></a>SQL ストアド プロシージャの作成とテスト

新しい SQL ストアド プロシージャを追加するには、プロジェクトを右クリックして **[追加]**  >  **[新しい項目]** を選択し、テンプレートの一覧から **[R を使用した SQL ストアド プロシージャ]** を選択して、ファイルに名前を付けた後、 **[OK]** を選択します。 既定のファイル名は *SqlSProc.R* です。読みやすくするため、このセクションの残りの部分では、ファイル名 *StoredProcedure.R* が使用されています。 複数のストアド プロシージャがある場合は、各ファイルに一意のファイル名が必要です。

RTVS ではストアド プロシージャとして 3 種類のファイルが作成されます。R コードの *.R* ファイル、SQL コードの *.Query.sql* ファイル、2 つを組み合わせた *.Template.sql* ファイルの 3 つです。 後の 2 つはソリューション エクスプローラーで *.R* ファイルの子として表示されます。

![R と SQL ストアド プロシージャが表示されたソリューション エクスプローラーの展開ビュー](media/sql-solution-explorer-expanded.png)

*.R* ファイル (この例では *StoredProcedure.R*) は、R コードを記述するファイルです。 既定の内容は次のとおりです。

```R
# @InputDataSet: input data frame, result of SQL query execution
# @OutputDataSet: data frame to pass back to SQL

# Test code
# library(RODBC)
# channel <- odbcDriverConnect(dbConnection)
# InputDataSet <- sqlQuery(channel, )
# odbcClose(channel)

OutputDataSet <- InputDataSet
```

簡単に言うと、このコードは `InputDataSet` という R データフレームを受け取り、その結果を `OutputDataSet` で返します。テンプレート コードは入力を出力にコピーするだけです。

> [!Note]
> これらのデータフレームの名前は、`sp_execute_external_script` システム ストアド プロシージャ呼び出しの `@input_data_1_name` パラメーターと `@output_data_1_name` パラメーターによって制御されます。 この呼び出し規則の詳細と使用例について詳しくは、「[sp_execute_external_script (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)」をご覧ください。

コメント内に生成されたもう 1 つのコードは、短いテスト スクリプトです。[RODBC パッケージ](https://cran.r-project.org/web/packages/RODBC/index.html)を使用して SQL ステートメントを SQL Server に送信し、実行した後、結果セットを R データフレームとして取得します。 このテスト コードをコメント解除し、SQL Server から返された結果セットに作用する R コードを対話形式で記述できます。

*.Query.sql* ファイル (この例では *StoredProcedure.Query.sql*) は、`InputDataSet` 用のデータを生成する SQL クエリを記述してテストするファイルです。 この *.sql* ファイルでは、エディターが普通の Transact-SQL 機能をすべて提供します。

SQL コードに問題がないことを確認したら、そのコードを R コードと統合できます。 *.R* ファイルを開いているエディターに *.sql* ファイルをドラッグします。 次の図では、*StoredProcedure.Query.sql* が *StoredProcedure.R* 内の `sqlQuery(channel, )` のコンマの後のポイントにドラッグされています。

![R 文字列変数への SQL ファイルの読み込み](media/sql-reference-sql-file-from-r.png)

このように、このシンプルなステップによって R コードが自動的に生成されて *.sql* ファイルが開きます。このファイルの内容を文字列に読み込み、その文字列を RODBC パッケージに渡して SQL Server に送信します。

`InputDataSet` データフレームを必要に応じて処理する R コードを対話形式で記述できます。 エディター内で R コードを選択し、**Ctrl**+**Enter** キーを押すだけで、そのコードを[対話型ウィンドウ](interactive-repl-for-r-in-visual-studio.md)に送信できます。

*.Template.sql* ファイル (この例では *StoredProcedure.Template.sql*) には、最終的に、SQL ストアド プロシージャを生成するためのテンプレートが含まれます。

```sql
CREATE PROCEDURE [StoredProcedure]
AS
BEGIN
EXEC sp_execute_external_script @language = N'R'
    , @script = N'_RCODE_'
    , @input_data_1 = N'_INPUT_QUERY_'
--- Edit this line to handle the output data frame.
    WITH RESULT SETS (([MYNEWCOLUMN] NVARCHAR(max)));
END;
```

- `_RCODE_` プレース ホルダーは、 *.R* ファイル (例: *StoredProcedure.R*) のコンテンツで置き換えられます。
- `_INPUT_QUERY_` プレース ホルダーは、 *.Query.sql* ファイル (例: *StoredProcedure.Query.sql*) のコンテンツで置き換えられます。
- ストアド プロシージャから返された結果セットのスキーマを記述するために、`WITH RESULT SETS` 句を編集します。 `OutputDataSet` データフレームから、ストアド プロシージャの呼び出し元に返す列を明示的に特定します。

たとえば、次のようなクエリがあるとします。

```sql
SELECT TOP 100 medallion, hack_license FROM nyctaxi_sample
```

この場合は、次のような `WITH RESULT SETS` 句を使用して、戻り値のデータ型を指定します。

```sql
WITH RESULT SETS ((medallion NVARCHAR(max), hack_license NVARCHAR(max)));
```

### <a name="publish-a-sql-stored-procedure"></a>SQL ストアド プロシージャの公開

1. **[R Tools]**  >  **[データ]**  >  **[Publish With Options]\(オプションを使用してパブリッシュ\)** メニュー コマンドを選択します。
1. 表示されるダイアログ ボックスで、 **[パブリッシュ先]** を **[データベース]** に変更し、ターゲットを指定して、 **[パブリッシュ]** を選択します。RTVS でストアド プロシージャがビルドされ、パブリッシュされます。

    ![ストアド プロシージャの公開ダイアログ ボックス](media/sql-publish-with-options.png)

1. プロジェクト内のすべてのストアド プロシージャを公開する方法として、 **[R Tools]**  >  **[データ]**  >  **[ストアド プロシージャの公開]** コマンドを使うことができます。このコマンドは、ソリューション エクスプローラーでプロジェクトを右クリックして選ぶこともできます。

> [!Tip]
> Visual Studio で SQL Server オブジェクト エクスプローラーを開いている場合、公開したストアド プロシージャはデータベースの **[プログラミング]**  >  **[ストアド プロシージャ]** フォルダーに表示されます。 また、オブジェクト エクスプローラーから実行することもできます。そのためには、右クリックして **[プロシージャの実行]** を選ぶか、 *.sql* クエリ ウィンドウから対話形式でプロシージャを呼び出します。
