---
title: R のリモート ワークスペース
description: リモート R ワークスペースを設定し、Visual Studio から接続する方法を説明します。
ms.date: 12/04/2017
ms.topic: conceptual
author: kraigb
ms.author: kraigb
manager: jmartens
ms.workload:
- data-science
ms.openlocfilehash: 96078d1b2fdb5a54c912cbf214024726ce102e4e
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99851843"
---
# <a name="set-up-remote-workspaces"></a>リモート ワークスペースの設定

この記事では、SSL と適切な R サービスでリモート サーバーを構成する方法について説明します。 これにより、R Tools for Visual Studio (RTVS) はそのサーバー上のリモート ワークスペースに接続できます。

## <a name="remote-computer-requirements"></a>リモート コンピューターの要件

- Windows 10、Windows Server 2016、または Windows Server 2012 R2。 RTVS には以下も必要です。
- [.NET Framework 4.6.1](https://www.microsoft.com/download/details.aspx?id=49981) 以降

## <a name="install-an-ssl-certificate"></a>SSL 証明書のインストール

RTVS を使用するには、リモート サーバーとのすべての通信を HTTP 上で行う必要があります。また、サーバー上に SSL 証明書が必要です。 信頼できる証明機関が署名した証明書を使用する (推奨) か、自己署名証明書を使用できます (接続時に自己署名証明書のために RTVS で警告が発生します)。いずれの場合でも、コンピューター上に証明書をインストールし、その秘密キーにアクセスできるようにする必要があります。

### <a name="obtain-a-trusted-certificate"></a>信頼できる証明書の取得

信頼できる証明書は、証明機関から発行されます (背景については、[Wikipedia の証明機関のページ](https://en.wikipedia.org/wiki/Certificate_authority)を参照してください)。 公的な身分証明書を入手する場合と同様に、信頼できる証明書の発行には多くのプロセスが必要で、料金がかかる可能性もありますが、要求と要求元の信頼性が検証されます。

証明書に含める必要がある重要なフィールドは、R サーバー コンピューターの完全修飾ドメイン名です。 証明機関に対して、サーバーが属するドメインに新しいサーバーを作成する権限を持っていることを証明する必要があります。

詳細な背景については、[Wikipedia の公開鍵証明書のページ](https://en.wikipedia.org/wiki/Public_key_certificate)を参照してください。

## <a name="install-an-ssl-certificate-on-windows"></a>Windows での SSL 証明書のインストール

SSL 証明書は、Windows に手動でインストールする必要があります。 以下の手順に従って、SSL 証明書をインストールします。

### <a name="obtain-a-self-signed-certificate-windows"></a>自己署名証明書の取得 (Windows)

信頼された証明書がある場合は、このセクションはスキップしてください。 信頼できる証明機関の証明書と比較すると、自己署名証明書は自分の身分証明書を作成するようなものです。 当然ながら、信頼できる証明機関の場合よりも作業は非常に単純ですが、強力な認証がありません。つまり、攻撃者が自分の証明書で未署名の証明書を上書きして、クライアントとサーバー間のすべてのトラフィックをキャプチャすることができます。 したがって、"*そのため、自己署名証明書は、信頼できるネットワーク上で、テスト シナリオの場合に限定して使用し、運用環境には使用しないことが推奨されます*"。

この理由から、自己署名証明書を使用してサーバーに接続しようとすると、RTVS からは常に次の警告が発行されます。

![自己署名証明書の警告ダイアログ](media/workspaces-remote-self-signed-certificate-warning.png)

自己署名証明書を発行するには:

1. 管理者アカウントを使用して R サーバー コンピューターにログオンします。
1. 新しい管理者用 PowerShell コマンド プロンプトを開き、次のコマンドを発行します。その際に、`"remote-machine-name"` は実際のサーバー コンピューターの完全修飾ドメイン名で置き換えます。

    ```ps
    New-SelfSignedCertificate -CertStoreLocation Cert:\LocalMachine\My -DnsName "remote-machine-name"
    ```

1. R サーバー コンピューター上でまだ PowerShell を実行したことがない場合は、次のコマンドを実行して、コマンドの実行を明示的に有効にします。

    ```ps
    Set-ExecutionPolicy -ExecutionPolicy RemoteSigned
    ```

背景については、[Wikipedia の自己署名証明書のページ](https://en.wikipedia.org/wiki/Self-signed_certificate)を参照してください。

### <a name="install-the-certificate"></a>証明書をインストールする

リモート コンピューターに証明書をインストールするには、コマンド プロンプトから *certlm.msc* (証明書マネージャー) を実行します。 **[個人]** フォルダーを右クリックし、 **[すべてのタスク]**  >  **[インポート]** コマンドの順に選択します。

![証明書のインポート コマンド](media/workspaces-remote-certificate-import.png)

### <a name="grant-permissions-to-read-the-ssl-certificates-private-key"></a>SSL 証明書の秘密キーを読み取るアクセス許可の付与

証明書をインポートしたら、以下の手順で説明するように秘密キーを読み取るアクセス許可を `NETWORK SERVICE` アカウントに付与します。 `NETWORK_SERVICE` は、R Services ブローカーの実行に使用されるアカウントです。R Services ブローカーは、サーバー コンピューターに対する受信 SSL 接続を終了するサービスです。

1. 管理者のコマンド プロンプトから *certlm.msc* (証明書マネージャー) を実行します。
1. **[個人]**  >  **[証明書]** を展開し、証明書を右クリックし、 **[すべてのタスク]**  >  **[秘密キーの管理]** の順に選択します。
1. 証明書を右クリックし、 **[すべてのタスク]** の **[秘密キーの管理]** コマンドを選択します。
1. 表示されるダイアログで **[追加]** を選択し、アカウント名として「`NETWORK SERVICE`」と入力します。

    ![[秘密キーの管理] ダイアログ、NETWORK_SERVICE の追加](media/workspaces-remote-manage-private-key-dialog.png)

1. **[OK]** を 2 回選択してダイアログを閉じて変更を確定します。

## <a name="install-an-ssl-certificate-on-ubuntu"></a>Ubuntu での SSL 証明書のインストール

`rtvs-daemon` パッケージは、インストールの一部として自己署名証明書を既定でインストールします。

### <a name="obtain-a-self-signed-certificate-ubuntu"></a>自己署名証明書の取得 (Ubuntu)

自己署名証明書を使用する利点とリスクは、Windows の説明を参照してください。 `rtvs-daemon` パッケージはインストール時に自己署名証明書を生成および構成します。 これは、自動生成された自己署名証明書を置換する場合にのみ行う必要があります。

自己署名証明書を発行するには、次の手順を実行します。

1. SSH または Linux コンピューターにログインします。
2. `ssl-cert` パッケージをインストールします。

    ```sh
    sudo apt-get install ssl-cert
    ```

3. `make-ssl-cert` を実行して既定の自己署名 SSL 証明書を生成します。

    ```sh
    sudo make-ssl-cert generate-default-snakeoil --force-overwrite
    ```

4. 生成されたキーと PEM ファイルを PFX に変換します。 生成された PFX はホーム フォルダーにあります。

    ```sh
    openssl pkcs12 -export -out ~/ssl-cert-snakeoil.pfx -inkey /etc/ssl/private/ssl-cert-snakeoil.key -in /etc/ssl/certs/ssl-cert-snakeoil.pem -password pass:SnakeOil
    ```

### <a name="configure-rtvs-daemon"></a>RTVS デーモンの構成

SSL 証明書ファイルのパス (PFX へのパス) を */etc/rtvs/rtvsd.config.json* で設定する必要があります。 `X509CertificateFile` と `X509CertificatePassword` をファイル パスとパスワードでそれぞれ更新します。

```json
{
  "logging": { "logFolder": "/tmp" },
  "security": {
    "allowedGroup": "",
    "X509CertificateFile": "/etc/rtvs/ssl-cert-snakeoil.pfx",
    "X509CertificatePassword": "SnakeOil"
  },
  "startup": { "name": "rtvsd" },
  "urls": "https://0.0.0.0:5444"
}
```

ファイルを保存し、デーモン `sudo systemctl restart rtvsd` を再起動します。

## <a name="install-r-services-on-windows"></a>Windows での R Services のインストール

R コードを実行するには、次のようにリモート コンピューターに R インタープリターがインストールされている必要があります。

1. 次のいずれかをダウンロードしてインストールします。

   - [Microsoft R Open](https://mran.microsoft.com/open/)
   - [CRAN R for Windows](https://cran.r-project.org/bin/windows/base/)

     いずれも機能は同じですが、Microsoft R Open の場合、さらにハードウェア アクセラレータによる [Intel Math Kernel Library](https://software.intel.com/intel-mkl) の線形代数ライブラリの提供を利用できます。

2. [R Services インストーラー](https://github.com/Microsoft/RTVS/blob/master/doc/rtvsd/rtvs-remote-downloads.md)を実行し、プロンプトが表示された場合は再起動します。 インストーラーは次の処理を行います。

    - *%PROGRAMFILES%\R Tools for Visual Studio\1.0\\* でフォルダーを作成し、すべての必要なバイナリをコピーします。
    - `RHostBrokerService` と `RUserProfileService` をインストールし、自動起動するように構成します。
    - 自動起動するように `seclogon` サービスを構成します。
    - *Microsoft.R.Host.exe* と *Microsoft.R.Host.Broker.exe* を既定のポート 5444 上のファイアウォールの受信規則に追加します。

コンピューターを再起動すると、R Services は自動的に起動します。

- **R Host Broker Service** は、Visual Studio と、コンピューター上で R コードが実行されるプロセス間のすべての HTTPS トラフィックを処理します。
- **R User Profile Service** は、Windows ユーザー プロファイルの作成を処理する特権を持つコンポーネントです。 このサービスは、新しいユーザーが R サーバー コンピューターに初めてログオンしたときに呼び出されます。

これらのサービスは、サービス管理コンソール (*compmgmt.msc*) で確認できます。

## <a name="install-r-services-on-linux"></a>Linux での R Services のインストール

R コードを実行するには、次のようにリモート コンピューターに R インタープリターがインストールされている必要があります。

1. 次のいずれかをダウンロードしてインストールします。

   - [Microsoft R Open](https://mran.microsoft.com/open/)
   - [CRAN R for Windows](https://cran.r-project.org/bin/linux/ubuntu/)

     いずれも機能は同じですが、Microsoft R Open の場合、さらにハードウェア アクセラレータによる [Intel Math Kernel Library](https://software.intel.com/intel-mkl) の線形代数ライブラリの提供を利用できます。

2. Ubuntu の物理コンピューター、Azure Ubuntu VM、Windows Subsystem for Linux (WSL)、Docker コンテナー (Azure Container Repository で実行されているものを含む) に関する、「[Remote R Service for Linux](setting-up-remote-r-service-on-linux.md)」 (Linux 用のリモート R サービス) の手順に従います。

## <a name="configure-r-services"></a>R Services の構成

リモート コンピューター上で R Services が実行されている場合、ユーザー アカウントを作成し、ファイアウォール規則を設定し、Azure ネットワークを構成し、SSL 証明書を構成する必要があります。

1. ユーザー アカウント:リモート コンピューターにアクセスする各ユーザーのアカウントを作成します。 標準の (特権のない) ローカル ユーザー アカウントを作成するか、R サーバー コンピューターをドメインに参加させて、適切なセキュリティ グループを `Users` セキュリティ グループに追加することができます。

1. ファイアウォール規則:`R Host Broker` の既定では、TCP ポート 5444 をリッスンしています。 そのため、受信トラフィックと送信トラフィックの両方に有効な Windows ファイアウォール規則があるようにします (送信は、パッケージのインストールなどのシナリオに必要です)。  組み込みの Windows ファイアウォールの場合、R Services インストーラーではこれらの規則が自動的に設定されます。 ただし、サードパーティのファイアウォールを使用している場合、`R Host Broker` 用のポート 5444 を手動で開きます。

1. Azure の構成:リモート コンピューターが Azure 上の仮想マシンの場合、Windows ファイアウォールとは独立している Azure ネットワーク内の受信トラフィック用にもポート 5444 を開きます。 詳細については、Azure ドキュメントの「[ネットワーク セキュリティ グループによるネットワーク トラフィックのフィルタリング](/azure/virtual-network/virtual-networks-nsg)」を参照してください。

1. 読み込む SSL 証明書を R Host Broker に指示します。イントラネット サーバーに証明書をインストールしている場合、サーバーの完全修飾ドメイン名は NETBIOS 名と同じ可能性があります。 この例では、読み込まれている既定の証明書なので、実行が必要なことはありません。

    ただし、インターネットに接続するサーバー (Azure VM など) に証明書をインストールしている場合、サーバーの完全修飾ドメイン名 (FQDN) を使用します。これは、インターネットに接続するサーバーの FQDN が NETBIOS 名と同じではなくなるためです。

    FQDN を使用するには、R Services がインストールされている場所 (既定では *%PROGRAM FILES%\R Remote Service for Visual Studio\1.0*) に移動し、テキスト エディターで *Microsoft.R.Host.Broker.Config.json* ファイルを開き、内容を次のように置き換え、CN をいずれかのサーバーの FQDN (`foo.westus.cloudapp.azure.com` など) に割り当てます。

    ```json
    {
      "server.urls": "https://0.0.0.0:5444",
      "security": {
        "X509CertificateName": "CN=your-server-fully-qualified-domain-name"
      }
    }
    ```

    ファイルを保存し、コンピューターを再起動して変更を適用します。

## <a name="troubleshooting"></a>トラブルシューティング

**Q.R サーバー コンピューターが応答していません。どうすればよいですか?**

コマンドラインからリモート コンピューターに ping を実行してみてください。`ping remote-machine-name` ping に失敗する場合、コンピューターが実行されていることを確認します。

**Q.[R インタラクティブ] ウィンドウにリモート コンピューターは起動中と表示されますが、サービスが実行されないのはなぜですか?**

考えられる理由は 3 つあります。

- [.NET Framework 4.6.1](https://www.microsoft.com/download/details.aspx?id=49981) 以降がコンピューターにインストールされていません。
- ポート 5444 上の受信接続と送信接続の両方について、`Microsoft.R.Host.Broker` と `Microsoft.R.Host` のファイアウォール規則が有効ではありません。
- `CN=<remote-machine-name>` の SSL 証明書がインストールされていませんでした。

上記の変更を行った後にコンピューターを再起動します。 次に、タスク マネージャー ([サービス] タブ) または *services.msc* で `RHostBrokerService` と `RUserProfileService` が実行されていることを確認します。

**Q.R サーバーに接続しているときに、[R インタラクティブ] ウィンドウに "401 アクセスは拒否されました" と表示されるのはなぜですか?**

考えられる理由は 2 つあります。

- 高い可能性で、`NETWORK SERVICE` アカウントが SSL 証明書の秘密キーへのアクセス権を持っていません。 前述の手順に従って、`NETWORK SERVICE` に秘密キーへのアクセス権を付与してください。
- `seclogon` サービスが実行されていることを確認します。 *services.msc* を使用して、`seclogon` が自動起動するように構成します。

**Q.R サーバーに接続しているときに、[R インタラクティブ] ウィンドウに "404 見つかりません" と表示されるのはなぜですか?**

おそらく、このエラーは Visual C++ 再頒布可能ライブラリが存在しないことが原因です。 [R インタラクティブ] ウィンドウで、ライブラリ (DLL) の不足に関するメッセージがあるかどうかを確認します。 次に、VS 2015 再頒布可能ファイルがインストールされ、R もインストールされていることを確認します。

**Q.[R インタラクティブ] ウィンドウからインターネット/リソースにアクセスできません。どうすればよいですか?**

`Microsoft.R.Host.Broker` と `Microsoft.R.Host` のファイアウォール規則で、ポート 5444 上の送信アクセスを許可します。 変更の適用後にコンピューターを再起動します。

**Q.上記の解決策をすべて試しても問題が解決しません。どうすればよいですか?**

*C:\Windows\ServiceProfiles\NetworkService\AppData\Local\Temp* でログ ファイルの場所を参照します。このフォルダーには、実行されていた R Broker Service のインスタンスごとに別のログ ファイルが含まれます。 サービスが再起動するたびに、新しいログ ファイルが作成されます。 最新のログ ファイルで誤りの手がかりを確認してください。
