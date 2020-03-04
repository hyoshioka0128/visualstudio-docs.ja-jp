---
title: ロード テスト用の ASP.NET プロファイラーを構成する
ms.date: 10/13/2016
ms.topic: conceptual
helpviewer_keywords:
- test settings, ASP.NET
ms.assetid: 6832fe39-04d5-4d94-8a18-3e2730bad423
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 0132401df33bd65d7e328307167b6c228155bb42
ms.sourcegitcommit: 1efb6b219ade7c35068b79fbdc573a8771ac608d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/28/2020
ms.locfileid: "78169392"
---
# <a name="how-to-configure-aspnet-profiler-for-load-tests-using-test-settings-in-visual-studio"></a>方法: Visual Studio でテストの設定を使用してロード テスト用の ASP.NET プロファイラーを構成する

ASP.NET プロファイラー診断データ アダプターを使用して、ASP.NET プロファイラー情報を収集できます。 この診断データ アダプターは、ASP.NET アプリケーションのパフォーマンス データを収集します。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

> [!NOTE]
> この診断データ アダプターは、Microsoft Test Manager を使用して実行されるテストには使用できません。 ASP.NET プロファイラー診断アダプターは、Visual Studio Enterprise を必要とする Web サイトのみを利用したロード テストで使用できます。

ASP.NET プロファイラー診断データ アダプターを使用すると、ロード テストの実行時に、アプリケーション層から ASP.NET プロファイラー データを収集できます。 プロファイラーは、実行時間が 1 時間以上になるような長時間のロード テストなどでは実行しないでください。 その理由は、プロファイラー ファイルが数百メガバイトの大きさになる可能性があるためです。 代わりに、ASP.NET プロファイラーを使用して、実行時間の短いロード テストを実行してください。その場合でも、パフォーマンスの問題を詳細に診断することができます。

> [!NOTE]
> ASP.NET プロファイラー診断データ アダプターは、インターネット インフォメーション サービス (IIS) プロセスをプロファイルします。 そのため、開発用 Web サーバーに対しては機能しません。 ロード テスト内で Web サイトをプロファイルするには、IIS が実行されているコンピューターにテスト エージェントをインストールする必要があります。 テスト エージェントはロードを生成しませんが、収集のみを目的としたエージェントとなります。 詳細については、[テスト エージェントのインストールと構成](../test/lab-management/install-configure-test-agents.md)に関するページを参照してください。

詳細については、[配布されたロード テストのテスト設定を作成する](../test/how-to-create-a-test-setting-for-a-distributed-load-test.md)」を参照してください。

## <a name="configure-the-aspnet-profiler-for-your-test-settings"></a>テストの設定に対して ASP.NET プロファイラーを構成する

この手順を実行する前に、Visual Studio からテストの設定を開き、 **[データと診断]** ページを選択する必要があります。

1. ASP.NET プロファイラーのデータの収集に使用するロールを選択します。

    > [!WARNING]
    > このロールは Web サーバーである必要があります。

2. **[ASP.NET プロファイラー]** を選択して、ASP.NET のプロファイル データの収集を有効にし、 **[構成]** を選択します。

     ASP.NET のプロファイル データの収集を構成するダイアログ ボックスが表示されます。

3. **[プロファイラー サンプリング間隔]** で、ASP.NET のプロファイル サンプルを次に取得するまで待機する CPU のクロック サイクル数 (停止なし) を示す値を入力します。

4. 階層の相互作用のプロファイルを有効にするには、 **[階層の相互作用のプロファイルを有効にする]** を選択します。

     階層の相互作用のプロファイルでは、成果物 (*MyPage.aspx*、*CompanyLogo.gif* など) ごとに Web サーバーに送信される要求の数と、各要求の処理に要する時間がカウントされます。 さらに、ページ要求の一環として使用された ADO.NET 接続と、その要求処理の一環としてクエリやストアド プロシージャ呼び出しが実行された回数が収集されます。

     2 つの異なるタイミング情報のセットが収集されます。

    - 各 Web 要求を処理するためのタイミング情報 (最小、最大、平均、および合計)

    - 各クエリを実行するためのタイミング情報 (最小、最大、平均、および合計)

テスト設定で構成された ASP.NET プロファイラー診断データ アダプターを使用すると、ASP.NET Web アプリケーションで ASP.NET プロファイル データを収集できます。

## <a name="see-also"></a>関連項目

- [テスト設定を使用して診断情報を収集する](../test/collect-diagnostic-information-using-test-settings.md)
- [方法: 配布されたロード テストのテスト設定を作成する](../test/how-to-create-a-test-setting-for-a-distributed-load-test.md)
- [テスト コントローラーとテスト エージェント](configure-test-agents-and-controllers-for-load-tests.md)