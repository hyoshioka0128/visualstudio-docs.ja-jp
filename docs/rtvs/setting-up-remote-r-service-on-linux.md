---
title: Linux 上でのリモート R サービスの設定
description: Ubuntu および Windows Subsystem for Linux 上にリモート R サービスをセットアップする方法について説明します。
ms.date: 12/04/2017
ms.topic: conceptual
author: kraigb
ms.author: kraigb
ms.reviewer: karthiknadig
manager: jmartens
ms.workload:
- data-science
ms.openlocfilehash: 586f3038ff4bb091fb99160d7965ad927eda070a
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99851817"
---
# <a name="remote-r-service-for-linux"></a>Linux 用のリモート R サービス

Linux 用のリモート R サービスは現在、rtvs デーモンとしてパッケージ化されています。 デーモンは、Ubuntu 16.04/16.10 LTS のデスクトップ、サーバー、および Ubuntu を実行している Windows Subsystem for Linux でサポートされテストされています。 この記事の大部分は、このような各種システム上でリモート R サービスを設定するための手順説明となります。

リモート マシンの構成が完了したら、次の手順を実行して、R Tools for Visual Studio (RTVS) をそのサービスに接続します。

1. **[R Tools]**  >  **[ウィンドウ]**  >  **[ワークスペース]** の順に選択して、 **[ワークスペース]** ウィンドウを開きます。
1. **[接続の追加]** を選択します。
1. 接続に名前を付けて、その URL を入力します。たとえば、`https://localhost:5444` (Linux 用 Windows サブシステム) または `https://public-ip:5444` (Azure コンテナー) とします。 完了したら、 **[保存]** を選択します。
1. 接続アイコンを選択するか、接続項目をダブルクリックします。
1. ログイン資格情報を入力します。 ユーザー名には、`<<unix>>\ruser1` のように、プレフィックスとして `<<unix>>\` を付けます (必要な場合は、Linux リモート マシンへのすべての接続に対して)。
1. 自己署名証明書を使用している場合は、警告が表示される可能性があります。 メッセージには、警告を解決するための手順が示されています。

## <a name="set-up-remote-r-service"></a>リモート R サービスの設定

このセクションでは、次のオプションについて説明します。

- [物理的な Ubuntu コンピューター](#physical-ubuntu-computer)
- [Azure 上での Ubuntu Server VM またはデータ サイエンス VM](#ubuntu-server-vm-or-data-science-vm-on-azure)
- [ローカルまたはリモートの Docker コンテナー (クリーン ビルド)](#local-or-remote-docker-container-clean-build)
- [Azure Container Instances で実行されているコンテナー](#container-running-on-azure-container-instances)

各ケースでは、リモート マシンに次の R インタープリターのいずれか 1 つがインストールされている必要があります。

- [Microsoft R Open](https://mran.microsoft.com/open/)
- [CRAN R for Windows](https://cran.r-project.org/bin/linux/ubuntu/)

### <a name="physical-ubuntu-computer"></a>物理的な Ubuntu コンピューター

1. コンピューターにログインしたら、rtvs デーモン tarball をダウンロードします。

    ```bash
    wget -O rtvs-daemon.tar.gz https://aka.ms/r-remote-services-linux-binary-current
    tar -xvzf rtvs-daemon.tar.gz
    ```

1. 次のインストール スクリプトを実行します。

    ```bash
    sudo ./rtvs-install
    ```

    サイレント オートメーションの場合は、`sudo ./rtvs-install -s` を使用します。

1. サービスを有効にして開始します。

    ```bash
    sudo systemctl enable rtvsd
    sudo systemctl start rtvsd
    ```

1. SSL 証明書を構成します (運用環境で必要)。 既定では、rtvs デーモンは、`ssl-cert` パッケージによって生成された `ssl-cert-snakeoil.pem` と `ssl-cert-snakeoil.pem` を使用します。 インストール中に、それらは `ssl-cert-snakeoil.pfx` に結合されます。 運用環境では、管理者によって提供される SSL 証明書を使用します。 SSL 証明書を構成するには、*/etc/rtvs/rtvsd.config.json* 内に *.pfx* ファイルと省略可能なインポート パスワードを指定します。

1. (省略可能) サービスが実行されていることを確認します。

    ```bash
    ps -A -f | grep rtvsd
    ```

    ユーザー名 `rtvssvc` の下に実行されているプロセスが表示されない場合は、 次のコマンドを使用して、プロセスを開始します。

    ```bash
    sudo systemctl start rtvsd
    ```

1. rtvs デーモンをさらに構成するには、`man rtvsd` を参照してください。

### <a name="ubuntu-server-vm-or-data-science-vm-on-azure"></a>Azure 上での Ubuntu Server VM またはデータ サイエンス VM

#### <a name="create-a-vm"></a>VM を作成する

1. [Azure portal](https://portal.azure.com) にサインインする
1. Virtual Machines に移動し、 **[追加]** を選択します。
1. 利用可能な VM イメージの一覧で、次のいずれかを検索して選択します。
    - Ubuntu Server: `Ubuntu Server 16.04 LTS`
    - データ サイエンス VM: `Linux Data Science` (詳細については、「[データ サイエンスの Virtual Machines](https://azure.microsoft.com/services/virtual-machines/data-science-virtual-machines/)」を参照してください)
1. 展開モデルを `Resource manager` に設定し、 **[作成]** を選択します。
1. VM の名前を選択し、ユーザー名とパスワードを指定します (パスワードは必須、SSH 公開キーによるログインはサポートされていません)。
1. VM 構成に対して他に必要な変更があれば、それを行います。
1. VM サイズを選択し、構成を確認し、 **[作成]** を選択します。 VM が作成されたら、次のセクションに進みます。

#### <a name="configure-the-vm"></a>VM を構成する

1. VM の **[ネットワーク]** セクションで、許可された受信ポートとして 5444 を追加します。 別のポートを使用するには、RTVS デーモン構成ファイル ( */etc/rtvs/rtvsd.config.json*) 内の設定を変更します。
1. (省略可能) DNS の名前を設定します。IP アドレスを使用することもできます。
1. PuTTY for WIndows などの SSH クライアントを使用して VM に接続します。
1. 前述の[物理的な Ubuntu コンピューター](#physical-ubuntu-computer)に対する手順に従います。

### <a name="windows-subsystem-for-linux-wsl"></a>Windows Subsystem for Linux (WSL)

1. [Windows 10](/windows/wsl/install-win10#install-the-windows-subsystem-for-linux) または [Windows Server](/windows/wsl/install-on-server#enable-the-windows-subsystem-for-linux-wsl) 用の WSL インストール手順に従います。
1. Windows で bash を起動し、前述の[物理的な Ubuntu コンピューター](#physical-ubuntu-computer)の手順に従います。ただし、例外が 1 つあります。 手順 3 では、代わりに `rtvsd` コマンドを使用してサービスを開始します。これは、WSL が現時点で systemd/systemctl インターフェイスをサポートしていないためです。

### <a name="local-or-remote-docker-container-clean-build"></a>ローカルまたはリモートの Docker コンテナー (クリーン ビルド)

1. 以下の内容を含む Docker ファイルを作成して、リモート R サービスのデーモンと最新バージョンの R をインストールします。**注**: このスクリプトでは、パスワード "foobar" を使用する "ruser1" という名前のユーザーが作成されます。ユーザー名とパスワードは、必要に応じて最後の 2 つの `RUN` ステートメントで変更できます。

    ```docker
    FROM ubuntu:16.04

    ARG DEBIAN_FRONTEND=noninteractive

    RUN apt-get update \
     && apt-get install -y software-properties-common python-software-properties \
     && apt-get install -y apt-transport-https \
     && rm -rf /var/lib/apt/lists/*

    RUN sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list' \
     && apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893 \
     && sh -c 'echo "deb https://cran.revolutionanalytics.com/bin/linux/ubuntu xenial/" > /etc/apt/sources.list.d/cran-r.list' \
     && apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E084DAB9 \
     && rm -rf /var/lib/apt/lists/* \
     && apt-get clean

    RUN apt-get update --fix-missing && apt-get update \
     && apt-get install -y dotnet-dev-1.0.4 libexplain51 libzip4 libc6 git lshw ssl-cert wget \
     && rm -rf /var/lib/apt/lists/*

    # install R
    RUN apt-get update && apt-get install -y r-base-dev
    RUN apt upgrade -y

    # install rtvs-daemon
    RUN wget -O rtvs-daemon.tar.gz https://aka.ms/r-remote-services-linux-binary-current && tar -xvzf rtvs-daemon.tar.gz && ./rtvs-install -s

    RUN useradd --create-home ruser1
    RUN echo "ruser1:foobar" | chpasswd

    EXPOSE 5444
    ```

1. Docker ファイルをビルドして実行します。

    ```bash
    docker build -t myrimage .
    docker run -p 5444:5444 myrimage rtvsd
    ```

1. RTVS からコンテナーに接続するには、パス、ユーザー名 `<<unix>>\ruser1`、パスワード `foobar` として `https://localhost:5444` を使用します。 コンテナーがリモート マシンで実行されている場合は、代わりにパスとして `https://remote-host-name:5444` を使用します。 ポートを変更するには、 */etc/rtvs/rtvsd.config.json* を更新します。

### <a name="container-running-on-azure-container-instances"></a>Azure Container Instances で実行されているコンテナー

1. 「[ローカルまたはリモートの Docker コンテナー (クリーン ビルド)](#local-or-remote-docker-container-clean-build)」で説明した手順に従ってイメージを作成します。
1. コンテナーを Docker ハブまたは Azure コンテナー リポジトリにプッシュします。
1. Azure CLI を起動し、`az login` コマンドを使用してサインインします。
1. `az container create` コマンドを使用してコンテナーを作成します。`systemd` サービスとして `rtvsd` を実行するようにコンテナーを設定していない場合は、`--command-line "rtvsd"` を使用します。 次のコマンドでは、イメージが Docker ハブ上にあると想定しています。 また、Azure コンテナー リポジトリを使用することもできます。そのためには、コンテナー リポジトリ資格情報引数をコマンド ラインに追加します。

    ```bash
    az container create --image myimage:latest --name myaz-container --resource-group myaz-container-res --ip-address public --port 5444 --cpu 2 --memory 4 --command-line "rtvsd"
    ```

1. `az container list` コマンドを使用して、状態を確認します。 `provisioningState`: `Succeeded` を探してください。
1. プロビジョニングが成功すると、コンテナーに接続できるようになります。 `ipAddress` フィールドでパブリック IP アドレスを検索し、これを、Docker ファイル内の資格情報と一緒に使用して、RTVS からコンテナーに接続します。
