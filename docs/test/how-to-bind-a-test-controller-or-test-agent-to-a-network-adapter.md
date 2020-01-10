---
title: ネットワーク アダプターにテスト コントローラーまたはテスト エージェントをバインドする
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- controllers, netwrok adapter
- agents, configuring
- agents, network adapter
- controllers, configuring
ms.assetid: 7eb9290a-f9f6-4e41-9caa-796fcfaf0610
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 6383d7a16839ba8934bb7f91664379e99da17a36
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75594787"
---
# <a name="how-to-bind-a-test-controller-or-test-agent-to-a-network-adapter"></a>方法: ネットワーク アダプターにテスト コントローラーまたはテスト エージェントをバインドする

テスト コントローラーまたはテスト エージェント ソフトウェアがインストールされているコンピューターに複数のネットワーク アダプターがある場合は、テスト コントローラーまたはテスト エージェントを識別するために、コンピューター名の代わりに IP アドレスを指定する必要があります。

> [!WARNING]
> テスト エージェントをセットアップするときに、次のエラーが表示されることがあります。
>
> **エラー 8110: 指定されたコントローラー コンピューターに接続できないか、コントローラー オブジェクトにアクセスできません**
>
> このエラーは、ネットワーク アダプターが複数あるコンピューターにテスト コントローラーをインストールしたことが原因で発生する場合があります。 エージェントのインストールには成功しており、テストを実行するまで問題が発覚しなかったということも考えられます。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="bind-a-test-controller-to-a-specific-network-adapter"></a>特定のネットワーク アダプターへのテスト コントローラーのバインド

### <a name="to-obtain-the-ip-addresses-of-the-network-adapters"></a>ネットワーク アダプターの IP アドレスを取得するには

1. Microsoft Windows の **[スタート]** ボタンをクリックし、 **[検索の開始]** ボックス内をクリックして「**cmd**」と入力し、**Enter** キーを押します。

2. 「**ipconfig /all**」と入力します。

     ネットワーク アダプターの IP アドレスが表示されます。 コントローラーをバインドするネットワーク アダプターの IP アドレスを控えておきます。

### <a name="to-bind-a-network-adapter-to-a-test-controller"></a>ネットワーク アダプターをテスト コントローラーにバインドするには

1. Microsoft Windows の **[スタート]** ボタンをクリックし、 **[検索の開始]** ボックス内をクリックして「**services.msc**」と入力し、**Enter** キーを押します。

     **[サービス]** ダイアログ ボックスが表示されます。

2. 結果ペインの **[名前]** 列で **[Visual Studio Test Controller]** サービスを右クリックし、 **[停止]** をクリックします。

     \- または -

     管理者特権でのコマンド プロンプトを開き、次のコマンドを実行します。

     `net stop vsttcontroller`

3. *%ProgramFiles(x86)%\Microsoft Visual Studio\2017\\\<edition>\Common7\IDE* に置かれた *QTCcontroller.exe.config* XML 構成ファイルを開きます。

4. `<appSettings>` タグを探します。

    ```xml
    <appSettings>
      <add key="LogSizeLimitInMegs" value="20"/>
      <add key="AgentConnectionTimeoutInSeconds" value="120"/>
      <add key="AgentSyncTimeoutInSeconds" value="300"/>
      <add key="ControllerServicePort" value="6901"/>
      <add key="ControllerUsersGroup" value="TeamTestControllerUsers"/>
      <add key="ControllerAdminsGroup" value="TeamTestControllerAdmins"/>
      <add key="CreateTraceListener" value="no"/>
    </appSettings>
    ```

5. `BindTo` セクションに `<appSettings>` キーを追加して、どのネットワーク アダプターを使用するかを指定します。

    ```xml
            <add key="BindTo" value="<YOUR IP ADDRESS>"/>
    </appSettings>
    ```

6. テスト コントローラー サービスを開始します。 そのためには、コマンド プロンプトで次のコマンドを実行します。

    `net start vsttcontroller`

    > [!WARNING]
    > テスト エージェントをコントローラーに接続するには、テスト エージェントのインストールを再実行する必要があります。 ここで、コントローラー名ではなく、コントローラーの IP アドレスを指定します。

     これは、コントローラー、エージェント サービス、およびエージェントの各プロセスに適用されます。 ネットワーク アダプターが複数あるコンピューターで実行する各プロセスについて、`BindTo` プロパティを設定する必要があります。 `BindTo` プロパティの設定手順は、3 つのプロセスすべてにおいて、このトピックで前に示したテスト コントローラーの場合と同じです。

### <a name="to-bind-a-network-interface-card-to-a-test-agent"></a>ネットワーク インターフェイス カードをテスト エージェントにバインドするには

1. Microsoft Windows の **[スタート]** ボタンをクリックし、 **[検索の開始]** ボックス内をクリックして「**services.msc**」と入力し、**Enter** キーを押します。

    **[サービス]** ダイアログ ボックスが表示されます。

2. 結果ウィンドウの **[名前]** 列で **[Visual Studio Test Agent]** サービスを右クリックし、 **[停止]** をクリックします。

     \- または -

     管理者特権でのコマンド プロンプトを開き、次のコマンドを実行します。

     **net stop vsttagent**

3. *%ProgramFiles(x86)%\Microsoft Visual Studio\2017\\\<edition>\Common7\IDE* に置かれた *QTAgentService.exe.config* XML 構成ファイルを開きます。

4. `<appSettings>` タグを探します。

    ```xml
    <appSettings>
      <appSettings>
      <add key="LogSizeLimitInMegs" value="20"/>
      <add key="AgentServicePort" value="6910"/>
      <add key="ControllerConnectionPeriodInSeconds" value="30"/>
      <add key="StopTestRunCallTimeoutInSeconds" value="120"/>
      <add key="CreateTraceListener" value="no"/>
      <add key="GetCollectorDataTimeout" value="300"/>
    </appSettings>  </appSettings>
    ```

5. `BindTo` セクションに `<appSettings>` キーを追加して、どのネットワーク アダプターを使用するかを指定します。

    ```xml
            <add key="BindTo" value="<YOUR IP ADDRESS>"/>
    </appSettings>
    ```

6. テスト エージェント サービスを開始します。 そのためには、コマンド プロンプトで次のコマンドを実行します。

    `net start vsttagent`

## <a name="see-also"></a>関連項目

- [テスト エージェントをインストールして構成する](../test/lab-management/install-configure-test-agents.md)
- [ロード テストのログ設定の変更](../test/modify-load-test-logging-settings.md)
- [テスト コントローラーおよびテスト エージェント用のポートの構成](../test/configure-ports-for-test-controllers-and-test-agents.md)
- [方法: テスト コントローラーおよびテスト エージェントのタイムアウト期限を指定する](../test/how-to-specify-timeout-periods-for-test-controllers-and-test-agents.md)
