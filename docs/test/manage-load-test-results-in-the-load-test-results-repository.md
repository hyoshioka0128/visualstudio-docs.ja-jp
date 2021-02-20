---
title: ロード テストの結果の管理
description: ロード テスト中に収集されたデータを管理する方法について説明します。これは、ロード テスト結果リポジトリ SQL データベースに格納されています。
ms.custom: SEO-VS-2020
ms.date: 10/19/2016
ms.topic: how-to
helpviewer_keywords:
- load tests, results repository
- results, load test
- load test results, repository
- Load Test Results Repository
ms.assetid: 1cd63c4b-4f74-4133-b675-5e8fbeab25f3
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.openlocfilehash: 5245ccdb9130d3fac9639e7befc63ee2a5ebf70a
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99887615"
---
# <a name="manage-load-test-results-in-the-load-test-results-repository"></a>ロード テストの結果リポジトリ内のロード テスト結果の管理

ロード テストを実行すると、ロード テストの実行中に収集されたすべての情報は、*ロード テストの結果リポジトリ* と呼ばれる SQL データベースに保存されます。 ロード テストの結果リポジトリには、パフォーマンス カウンター データおよび記録されたエラーに関するすべての情報が含まれます。 結果リポジトリ データベースは、コントローラーのセットアップによって作成されるか、ロード テストを最初にローカルで実行したときに自動的に作成されます。 ローカルで実行する場合、ロード テスト スキーマが存在しなければ、データベースは自動的に作成されます。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

コントローラーの結果リポジトリの接続文字列を変更して別のサーバーを使用する場合は、新しいサーバーでスキーマを作成するために、*loadtestresultsrepository.sql* スクリプトを実行する必要があります。

Visual Studio Ultimate には、テクノロジに基づいて一般的なパフォーマンス カウンターを収集する名前付きカウンター セットが用意されています。 これらのセットは、IIS サーバー、ASP.NET サーバー、または SQL サーバーを分析する場合に役立ちます。 カウンター セットで収集されたすべてのデータは、ロード テストの結果リポジトリに保存されます。

> [!IMPORTANT]
> カウンター セットとパフォーマンス カウンター データは別のものです。 カウンター セットはメタデータです。 IIS サーバーや SQL サーバーなど、特定の役割を持つコンピューターから収集する必要があるパフォーマンス カウンターのグループを定義します。 カウンター セットは、ロード テスト定義の一部です。 パフォーマンス カウンター データは、カウンター セット、特定のコンピューターへのカウンター セットの割り当て、およびサンプル率に基づいて収集されます。

## <a name="sql-server-versions"></a>SQL Server のバージョン

ロード テストを使用する場合は、Visual Studio と共にインストールされる、SQL Server Express LocalDB を使用できます。 これは、ロード テスト用の既定のデータベース サーバーです (Microsoft Excel 統合を含む)。 SQL Server Express LocalDB は、プログラム開発者を対象にした SQL Server Express の実行モードです。 SQL Server Express LocalDB のインストールでは、SQL Server データベース エンジンを開始するために必要な最小のファイル セットがコピーされます。

チームによってデータベースへの高いニーズが予測される場合や、プロジェクトが SQL Server Express LocalDB のスケールを超える場合は、今後の拡張に対応できるように、SQL Express または SQL Server のフル バージョンへのアップグレードを検討する必要があります。 SQL Server をアップグレードする場合、SQL Server Express LocalDB の MDF ファイルと LDF ファイルはユーザー プロファイル フォルダーに格納されます。 これらのファイルを使用すると、ロード テスト データベースを SQL Server Express または SQL Server にインポートできます。

## <a name="load-test-results-store-considerations"></a>ロード テストの結果ストアに関する考慮事項

Visual Studio Enterprise をインストールすると、ロード テストの結果ストアは、コンピューターにインストールされている SQL Express のインスタンスを使用するように設定されます。 SQL Express は最大 4 GB のディスク容量しか使用できません。 長期にわたって多数のロード テストを実行する場合は、ロード テストの結果ストアが完全な SQL Server 製品 (使用可能な場合) のインスタンスを使用するように構成することを検討してください。

## <a name="load-test-analyzer-tasks"></a>ロード テスト アナライザー タスク

|タスク|関連するトピック|
|-|-----------------------|
|**ロード テストの結果リポジトリの設定:** SQL データベースに、ロード テストの結果リポジトリを設定できます。 **注:**  ロード テスト リポジトリは、テスト コントローラーをインストールするときに作成することもできます。 詳細については、[テスト エージェントのインストールと構成](../test/lab-management/install-configure-test-agents.md)に関するページを参照してください。||
|**結果リポジトリの選択と表示:** 特定の結果リポジトリを選択できます。 結果ストアはローカルの結果ストアに限定されていません。 多くの場合、ロード テストは複数のリモート エージェント コンピューターで実行されます。 エージェントまたはローカル コンピューターからのテスト結果は、ロード テストの結果ストアを作成した SQL サーバーのいずれかに保存できます。 いずれの場合も、**[テスト コントローラーの管理]** ウィンドウを使用して、ロード テストの結果を保存する場所を指定する必要があります。|-   [方法: ロード テストの結果リポジトリを選択する](../test/how-to-select-a-load-test-results-repository.md)<br />-   [方法: ロード テストの結果にアクセスして分析する](../test/how-to-access-load-test-results-for-analysis.md)|
|**リポジトリからロード テストの結果を削除:****[ロード テストの結果を開いて管理]** ダイアログ ボックスを使用して、**ロード テスト エディター** からロード テストの結果を削除できます。|-   [方法: ロード テスト結果をリポジトリから削除する](../test/how-to-delete-load-test-results-from-a-repository.md)|
|**リポジトリへの結果のインポートおよびリポジトリからの結果のエクスポート:****ロード テスト エディター** で、ロード テストの結果をインポートおよびエクスポートすることができます。|-   [方法: ロード テスト結果をリポジトリにインポートする](../test/how-to-import-load-test-results-into-a-repository.md)<br />-   [方法: ロード テスト結果をリポジトリからエクスポートする](../test/how-to-export-load-test-results-from-a-repository.md)|

## <a name="related-tasks"></a>関連タスク

[ロード テストの結果の分析](../test/analyze-load-test-results-using-the-load-test-analyzer.md)

実行中のロード テストの結果と完了したロード テストの結果は両方とも **ロード テスト アナライザー** を使用して表示できます。

## <a name="see-also"></a>関連項目

- [ロード テストの結果の分析](../test/analyze-load-test-results-using-the-load-test-analyzer.md)
- [方法 : ロード テストの結果にアクセスして分析する](../test/how-to-access-load-test-results-for-analysis.md)
