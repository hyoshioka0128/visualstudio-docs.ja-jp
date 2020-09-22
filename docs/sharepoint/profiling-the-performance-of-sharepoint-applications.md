---
title: SharePoint アプリケーションのパフォーマンスのプロファイリング |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.Profiling.SilverlightWebPartOnly
- VS.SharePointTools.Profiling.DotNetTrustLevel
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, profiling
- performance testing [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, performance testing
- profiling [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 2037842e57b6152990144d9ea652936e65517e13
ms.sourcegitcommit: 7a46232242783ebe23f2527f91eac8eb84b3ae05
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/17/2020
ms.locfileid: "90739955"
---
# <a name="profile-the-performance-of-sharepoint-applications"></a>SharePoint アプリケーションのパフォーマンスのプロファイリング

SharePoint アプリケーションの実行速度が遅いか効率的でない場合、Visual Studio のプロファイル機能を使用して、問題のあるコードやその他の要素を特定できます。 ロード テスト機能を使用すると、多数のユーザーがアプリケーションに同時にアクセスする場合など、ストレス下で SharePoint アプリケーションを実行する方法を決定できます。 Web パフォーマンス テストを実行すると、Web 上でのアプリケーションの実行方法を測定できます。 コード化された UI テストを使用すると、ユーザー インターフェイスを含め、SharePoint アプリケーション全体が適切に機能しているかどうかを確認できます。 これらのテストを一緒に使用すると、アプリケーションを配置する前にパフォーマンスの問題を識別するのに役立ちます。

## <a name="profile-tools-overview"></a>プロファイルツールの概要

プロファイルとは、実行中のアプリケーションのパフォーマンス動作を観察および記録するプロセスのことです。 アプリケーションをプロファイルすると、ボトルネック、非効率的なコード、メモリ割り当ての問題など、アプリケーションの実行速度の低下または過度なメモリ消費を引き起こす問題を見つけることができます。 たとえば、プロファイルを使用すると、頻繁に呼び出され、アプリケーション全体のパフォーマンスを低下させる可能性があるコードのセグメントであるホットスポットをコード内で特定できます。 特定したホットスポットは、最適化するか除去します。

統合開発環境 (IDE: Integrated Development Environment) を使用すると、このようなパフォーマンスの問題を特定し検索できます。 SharePoint プロジェクトに対するこれらのツールの動作は、他の種類の Visual Studio プロジェクトに対する動作と同じです。 プロファイリング ツールのパフォーマンス ウィザードでは、指定したテストを使用するパフォーマンス セッションを作成できます。 パフォーマンスセッションは、アプリケーションからパフォーマンス情報を収集するために使用される構成データのセットであり、1つまたは複数のプロファイリング実行の結果と共に使用されます。 パフォーマンスセッションはプロジェクトフォルダーに格納され、 **パフォーマンスエクスプローラー**で表示できます。 詳細については、「[パフォーマンス収集方法について](../profiling/understanding-performance-collection-methods.md)」を参照してください。

アプリケーションでプロファイル分析を作成して実行すると、レポートにそのパフォーマンスに関する詳細情報が示されます。 このレポートには、一定期間における CPU 使用率のグラフ、階層関数の呼び出し履歴、コール ツリーなどの項目を含めることができます。 レポートの正確な内容は、サンプリング、インストルメンテーションなど、実行するテストの種類によって異なることがあります。 詳細については、「 [プロファイルツールレポートの概要](../profiling/performance-report-overview.md)」を参照してください。

## <a name="performance-session-process"></a>パフォーマンスセッションのプロセス

アプリケーションのプロファイリングを行うには、最初に、プロファイリング ツールのパフォーマンス ウィザードを使用してパフォーマンス セッションを作成します。 メニューバーで、[ **分析**]、[ **パフォーマンスウィザードの起動**] の順に選択します。 ウィザードの完了時に、必要なプロファイリング方法、プロファイリングするアプリケーションなど、パフォーマンス セッションに必要な情報を入力します。 詳細については、「 [方法: パフォーマンスウィザードを使用して Web サイトまたは Web アプリケーションをプロファイリング](../profiling/how-to-collect-performance-data-for-a-web-site.md)する」を参照してください。 また、コマンド ライン オプションを使用して、パフォーマンス セッションを設定および実行することもできます。 詳細については、「 [コマンドラインからのプロファイルツールの使用](../profiling/using-the-profiling-tools-from-the-command-line.md)」を参照してください。 パフォーマンスセッションのすべての側面を手動で構成する場合は、「 [方法: プロファイルツールを使用してパフォーマンスセッションを手動で作成](../profiling/how-to-manually-create-performance-sessions.md)する」を参照してください。 また、単体テストからパフォーマンスセッションを作成するには、[ **テスト結果** ] ウィンドウで単体テストのショートカットメニューを開き、[ **パフォーマンスセッションの作成**] を選択します。

パフォーマンス セッションを設定したら、セッションの構成が保存され、プロファイル データを提供するようにサーバーが構成されます。その後、アプリケーションが実行されます。 アプリケーションの使用中、パフォーマンス データがログ ファイルに書き込まれます。 パフォーマンスセッションは **パフォーマンスエクスプローラー** [ **ターゲット** ] フォルダーの下に一覧表示されます。 パフォーマンスセッションが完了すると、**パフォーマンスエクスプローラー**の [**レポート**] フォルダーにそのレポートが表示されます。 レポートを表示するには、 **パフォーマンスエクスプローラー**で開きます。 パフォーマンスセッションのプロパティを表示または構成するには、 **パフォーマンスエクスプローラー**でそのショートカットメニューを開き、[ **プロパティ**] をクリックします。 パフォーマンスセッションの特定のプロパティの詳細については、「 [プロファイルツールのパフォーマンスセッションの構成](../profiling/configuring-performance-sessions.md)」を参照してください。 パフォーマンスセッションの結果を解釈する方法の詳細については、「 [プロファイルツールデータの分析](../profiling/analyzing-performance-tools-data.md)」を参照してください。

## <a name="stress-test"></a>ストレステスト

Visual Studio でロードテストと web パフォーマンステストを作成することによって、アプリケーションのストレスパフォーマンスを分析できます。 Visual Studio でロード テストを作成するときに、アプリケーションをテストするときに比較対象として使用する、シナリオと呼ばれる要素の組み合わせを指定します。 これらの要素には、ロード パターン、テスト ミックス モデル、テスト ミックス、ネットワーク ミックス、Web ブラウザー ミックスなどが含まれます。 ロード テスト シナリオには、単体テストと Web パフォーマンス テストの両方を含めることができます。

図 1: ロード テストの結果の例

![ロード テストの実行グラフ ビュー](../sharepoint/media/load-webgraphs.png "ロード テストの実行グラフ ビュー")

Web パフォーマンス テストでは、エンド ユーザーが SharePoint アプリケーションとやり取りする方法をシミュレートします。 Web パフォーマンステストを作成するには、ブラウザーセッションで HTTP 要求を記録するか、 **Web パフォーマンステストレコーダー**を使用します。 ブラウザーセッションが終了すると、web 要求が **Web パフォーマンステストエディター** に表示されます。 その後、 **Web パフォーマンステスト結果ビューアー**で結果をデバッグできます。 **Web パフォーマンステストエディター**を使用して、web パフォーマンステストを手動でビルドすることもできます。

## <a name="test-user-interfaces"></a>テストユーザーインターフェイス

コード化された UI テストでは、ユーザー インターフェイス (UI) を介して SharePoint アプリケーションが自動的に実行されます。 これらのテストでは、ボタン、メニューなどの UI コントロールが正しく動作するかどうかを確認します。 この種類のテストは、検証や他のロジックが Web ページなどの UI で実行されている場合に特に便利です。 また、コード化された UI テストを使用して、手動テストを自動化することもできます。 SharePoint アプリケーションのコード化された UI テストは、他の種類のアプリケーションのテストを作成するときと同じ方法で作成します。 詳細については、「 [コード化された UI テストを使用した SharePoint 2010 アプリケーションのテスト](../vs-2015/test/testing-sharepoint-2010-applications-with-coded-ui-tests.md?view=vs-2015)」を参照してください。

## <a name="related-topics"></a>関連トピック

|Title|説明|
|-----------|-----------------|
|[チュートリアル: SharePoint アプリケーションのプロファイリング](../sharepoint/walkthrough-profiling-a-sharepoint-application.md)|SharePoint アプリケーションのサンプリング プロファイル分析を実行する方法を示します。|
|[リリース前のアプリのパフォーマンス テスト](/azure/devops/test/load-test/run-performance-tests-app-before-release?view=vsts)|SharePoint アプリケーションのストレス テストに役立つロード テストを作成する方法について説明します。|
|[コードの単体テスト](../test/unit-test-your-code.md)|単体テストを使用してコードの論理エラーを検出する方法について説明します。|
|[コード化された UI テストを使用した SharePoint 2010 アプリケーションのテスト](../vs-2015/test/testing-sharepoint-2010-applications-with-coded-ui-tests.md?view=vs-2015)|SharePoint アプリケーションのユーザー インターフェイスをテストする方法について説明します。|

## <a name="see-also"></a>関連項目

- [SharePoint ソリューションのビルドとデバッグ](../sharepoint/building-and-debugging-sharepoint-solutions.md)
- [コード品質の向上](../test/improve-code-quality.md)