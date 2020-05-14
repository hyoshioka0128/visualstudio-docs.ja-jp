---
title: テスト コントローラーとテスト エージェントのトラブルシューティング
ms.date: 10/20/2016
ms.topic: troubleshooting
helpviewer_keywords:
- load tests, test controllers
- load tests, troubleshooting
- load tests, test agents
- troubleshooting, test controllers and agents in load tests
ms.assetid: 77329348-3a5d-43de-b6cb-90f93296a081
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 51d7e15ec71eec7134dfc49b3515385970e593a0
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "75565956"
---
# <a name="strategies-for-troubleshooting-test-controllers-and-test-agents-in-load-tests"></a>ロード テストにおけるテスト コントローラーとテスト エージェントのトラブルシューティングの方法

この記事では、Visual Studio でテスト コントローラーとテスト エージェントを操作するときに発生する可能性がある一般的な問題について説明します。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="unable-to-collect-performance-counters-on-test-agent-computer"></a>テスト エージェント コンピューターのパフォーマンス カウンターの値を収集できない

ロード テストを実行するときに、テスト エージェント コンピューターに接続してパフォーマンス カウンターのデータを取得しようとすると、エラーが表示されることがあります。 パフォーマンス カウンターのデータをリモート コンピューターに提供するサービスは、リモート レジストリ サービスです。 一部のオペレーティング システムでは、リモート レジストリ サービスが自動的に起動しません。 この問題を解消するには、リモート レジストリ サービスを手動で開始します。

> [!NOTE]
> リモート レジストリ サービスには、**コントロール パネル**からアクセスできます。 **[管理ツール]** をクリックして **[サービス]** をクリックします。

これ以外の原因として、パフォーマンス カウンターを読み取るために必要なアクセス許可がない場合もあります。 ローカル テストの実行では、テストを実行するユーザーのアカウントが、Power Users グループ (以上) または Performance Monitor Users グループのメンバーである必要があります。 リモート テストの実行では、コントローラーの実行に使用するよう構成されているアカウントが、Power Users グループ (以上) または Performance Monitor Users グループのメンバーである必要があります。

## <a name="set-the-logging-level-on-a-test-controller-computer"></a>テスト コントローラー コンピューターのログ レベルを設定する

テスト コントローラー コンピューターのログ レベルを制御できます。 これは、特定の環境におけるロード テストの実行時に発生する問題を診断するのに役立ちます。

### <a name="to-set-the-logging-level-on-a-test-controller-computer"></a>テスト コントローラー コンピューターのログ レベルを設定するには

1. テスト コントローラー サービスを停止します。 コマンド プロンプトで、「`net stop vsttcontroller`」と入力します。

2. *QTController.exe.config* というファイルを開きます。このファイルは、コントローラーのインストール ディレクトリに含まれています。

3. このファイルの system diagnostics セクションの `EqtTraceLevel` スイッチのエントリを編集します。 コードは次のようになります。

    ```xml
    <system.diagnostics>
        <trace autoflush="true" indentsize="4">
            <listeners>
                <add name="myListener" type="System.Diagnostics.TextWriterTraceListener" initializeData="d:\VSTestHost.log" />
            </listeners>
        </trace>
        <switches>
            <!-- You must use integral values for "value":
                    0 = off,
                    1 = error,
                    2 = warn,
                    3 = info,
                    4 = verbose. -->
            <add name="EqtTraceLevel" value="4" />
        </switches>
    </system.diagnostics>
    ```

4. ファイルを保存します。

5. コントローラー サービスを開始します。 コマンド プロンプトで、「`net start vsttcontroller`」と入力します。

これは、テスト コントローラー、テスト エージェント サービス、およびテスト エージェントの各プロセスに当てはまります。 問題を診断する場合は、この 3 つのプロセスすべてのログを有効にすることが役立ちます。 ログ レベルの設定手順は、3 つのプロセスすべてにおいて、前に示したテスト コントローラーの場合と同じです。 テスト エージェント サービスとエージェント プロセスのログ レベルを設定するには、次の構成ファイルを使用します。

- *QTController.exe.config*: コントローラー サービス

- *QTAgentService.exe.config*: エージェント サービス

- *QTDCAgent(32).exe.config*: 32 ビット アーキテクチャ用のエージェント データ アダプター プロセス

- *QTDCAgent(64).exe.config*: 64 ビット アーキテクチャ用のエージェント データ アダプター プロセス

- *QTAgent(32).exe.config* 32 ビット アーキテクチャ用のエージェント テスト プロセス

- *QTAgent(64).exe.config* 64 ビット アーキテクチャ用のエージェント テスト プロセス

## <a name="bind-a-test-controller-to-a-network-adapter"></a>テスト コントローラーをネットワーク アダプターにバインドする

テスト エージェントをセットアップするときに、次のエラーが表示されることがあります。

**エラー 8110: 指定されたコントローラー コンピューターに接続できないか、コントローラー オブジェクトにアクセスできません**

このエラーは、ネットワーク アダプターが複数あるコンピューターにテスト コントローラーをインストールしたことが原因で発生する場合があります。

> [!NOTE]
> テスト エージェントのインストールには成功しており、テストを実行するまで問題が発覚しなかったということも考えられます。

このエラーを解消するには、テスト コントローラーをネットワーク アダプターのいずれかにバインドする必要があります。 まずテスト コントローラーの `BindTo` プロパティを設定し、次にテスト コントローラーの参照に名前ではなく IP アドレスを使用するようにテスト エージェントを変更する必要があります。 この手順について、次に説明します。

### <a name="to-obtain-the-ip-address-of-the-network-adapter"></a>ネットワーク アダプターの IP アドレスを取得するには

1. **[スタート]** を選択し、 **[ファイル名を指定して実行]** を選択します。

     **[実行]** ダイアログ ボックスが表示されます。

2. 「`cmd`」と入力し、 **[OK]** をクリックします。

     コマンド プロンプトが開きます。

3. 「`ipconfig /all`」と入力します。

     ネットワーク アダプターの IP アドレスが表示されます。 コントローラーをバインドするネットワーク アダプターの IP アドレスを控えておきます。

### <a name="to-bind-a-test-controller-to-a-network-adapter"></a>テスト コントローラーをネットワーク アダプターにバインドするには

1. テスト コントローラー サービスを停止します。 コマンド プロンプトで、「`net stop vsttcontroller`」と入力します。

2. *QTController.exe.config* というファイルを開きます。ファイルは、 *%ProgramFiles(x86)%\Microsoft Visual Studio\2017\Enterprise\Common7\IDE* にあります。

3. `BindTo` プロパティのエントリをアプリケーション設定に追加します。 コントローラーにバインドするネットワーク アダプターの IP アドレスを指定します。 コードは次のようになります。

    ```xml
    <appSettings>
        <add key="LogSizeLimitInMegs" value="20" />
        <add key="AgentSyncTimeoutInSeconds" value="120" />
        <add key="ControllerServicePort" value="6901" />
        <add key="ControllerUsersGroup" value="TeamTestControllerUsers" />
        <add key="ControllerAdminsGroup" value="TeamTestControllerAdmins" />
        <add key="CreateTraceListener" value="no" />
        <add key="BindTo" value="<YOUR IP ADDRESS>" />
    </appSettings>
    ```

4. ファイルを保存します。

5. テスト コントローラー サービスを開始します。 コマンド プロンプトで、「`net start vsttcontroller`」と入力します。

### <a name="to-connect-a-test-agent-to-a-bound-controller"></a>バインドされたコントローラーにテスト エージェントを接続するには

- テスト エージェントのインストールを再実行します。 ここで、テスト コントローラー名ではなく、テスト コントローラーの IP アドレスを指定します。

これは、テスト コントローラー、テスト エージェント サービス、およびテスト エージェントの各プロセスに当てはまります。 ネットワーク アダプターが複数あるコンピューターで実行する各プロセスについて、`BindTo` プロパティを設定する必要があります。 `BindTo` プロパティの設定手順は、3 つのプロセスすべてにおいて、前に示したテスト コントローラーの場合と同じです。 テスト エージェント サービスとテスト エージェント プロセスのログ レベルを設定するには、「[テスト コントローラー コンピューターのログ レベルの設定](#set-the-logging-level-on-a-test-controller-computer)」で示した構成ファイルを使用します。

## <a name="see-also"></a>関連項目

- [テスト コントローラーとテスト エージェント](../test/configure-test-agents-and-controllers-for-load-tests.md)
