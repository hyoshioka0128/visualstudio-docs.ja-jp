---
title: 'Docker チュートリアル-パート 6: 複数コンテナーアプリ'
description: コンテナー間のネットワークを設定する方法と、MySQL データベースのコンテナーを追加する方法について説明します。
ms.date: 08/04/2020
author: nebuk89
ms.author: ghogen
manager: jillfra
ms.technology: vs-azure
ms.topic: conceptual
ms.workload:
- azure
ms.openlocfilehash: 9513a3414a38aa02f6a4607a8c95bbf02c0e1cf6
ms.sourcegitcommit: c4212f40df1a16baca1247cac2580ae699f97e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89176727"
---
# <a name="multi-container-apps"></a>複数コンテナー アプリ

この時点で、単一コンテナーアプリを使用しています。 しかし、ここでは MySQL をアプリケーションスタックに追加します。 次の質問は多くの場合、「MySQL はどこで実行されるのでしょうか。 同じコンテナーにインストールするか、個別に実行しますか? " 一般に、 **各コンテナーは1つの処理を行い、適切に実行する必要があります。** いくつかの理由があります。

- Api とフロントエンドのスケーリングは、データベースとは異なる方法で行うことをお勧めします。
- 個別のコンテナーを使用してバージョンを分離し、バージョンを更新できます
- データベースのコンテナーをローカルで使用することもできますが、運用環境でデータベースに管理されたサービスを使用することができます。 アプリケーションを使用してデータベースエンジンを配布する必要はありません。
- 複数のプロセスを実行するには、プロセスマネージャーが必要です (コンテナーは1つのプロセスのみを開始します)。これにより、コンテナーの起動/シャットダウンの複雑さが増します。

その理由は他にもあります。 そのため、次のように動作するようにアプリケーションを更新します。

![Todo アプリが MySQL コンテナーに接続されました](media/multi-app-architecture.png)

## <a name="container-networking"></a>コンテナー ネットワーク

既定では、コンテナーは分離して実行され、同じコンピューター上の他のプロセスまたはコンテナーについては何も知らないことに注意してください。 では、どのようにして1つのコンテナーが別のコンテナーと通信できるようにするのでしょうか。 答えは **ネットワーク**です。 ここでは、ネットワークエンジニア (バンザイ!) である必要はありません。 このルールを覚えてください...

> [!NOTE]
> 2つのコンテナーが同じネットワーク上にある場合は、互いに通信できます。 そうでない場合は、できません。

## <a name="start-mysql"></a>MySQL を開始します。

ネットワーク上にコンテナーを配置する方法は2つあります。最初にコンテナーを割り当てるか、既存のコンテナーを接続します。 ここでは、最初にネットワークを作成し、起動時に MySQL コンテナーをアタッチします。

1. ネットワークを作成します。

    ```bash
    docker network create todo-app
    ```

1. MySQL コンテナーを起動し、ネットワークに接続します。 また、データベースを初期化するためにデータベースが使用する環境変数をいくつか定義します ( [MySQL Docker Hub の一覧](https://hub.docker.com/_/mysql/)の「環境変数」セクションを参照してください) ( ` \ ` Windows PowerShell では、文字をに置き換えてください `` ` `` )。

    ```bash
    docker run -d \
        --network todo-app --network-alias mysql \
        -v todo-mysql-data:/var/lib/mysql \
        -e MYSQL_ROOT_PASSWORD=secret \
        -e MYSQL_DATABASE=todos \
        mysql:5.7
    ```

    また、フラグが指定されていることがわかり `--network-alias` ます。 これについては、すぐに説明します。

    > [!TIP]
    > ここでボリューム名を使用していることがわかります `todo-mysql-data` 。ここで `/var/lib/mysql` 、MySQL はデータを格納します。 ただし、コマンドを実行したことはありません `docker volume create` 。 Docker は、名前付きボリュームを使用することを認識し、自動的に作成します。

1. データベースが稼働していることを確認するには、データベースに接続し、データベースが接続されていることを確認します。

    ```bash
    docker exec -it <mysql-container-id> mysql -p
    ```

    パスワードの入力を求めるメッセージが表示されたら、「 **secret**」と入力します。 MySQL シェルで、データベースを一覧表示し、データベースが表示されていることを確認し `todos` ます。

    ```cli
    mysql> SHOW DATABASES;
    ```

    出力は次のようになります。

    ```plaintext
    +--------------------+
    | Database           |
    +--------------------+
    | information_schema |
    | mysql              |
    | performance_schema |
    | sys                |
    | todos              |
    +--------------------+
    5 rows in set (0.00 sec)
    ```

    バンザイ! データベースがあり、使用する準備ができました `todos` 。

## <a name="connect-to-mysql"></a>MySQL への接続

MySQL が稼働していることがわかったので、それを使用してみましょう。 しかし、質問は...どう。 同じネットワーク上で別のコンテナーを実行する場合、コンテナーを検索する方法はありますか (各コンテナーに独自の IP アドレスがあることを思い出してください)。

これを理解するために、 [nicolaka/netshoot](https://github.com/nicolaka/netshoot) コンテナーを使用します。これには、トラブルシューティングやネットワークの問題のデバッグに役立つ *多数* のツールが付属しています。

1. イメージを使用して新しいコンテナーを開始し `nicolaka/netshoot` ます。 必ず同じネットワークに接続してください。

    ```bash
    docker run -it --network todo-app nicolaka/netshoot
    ```

1. コンテナー内で、 `dig` コマンドを使用します。これは便利な DNS ツールです。 ホスト名の IP アドレスを参照し `mysql` ます。

    ```bash
    dig mysql
    ```

    次のような出力が表示されます。

    ```text
    ; <<>> DiG 9.14.1 <<>> mysql
    ;; global options: +cmd
    ;; Got answer:
    ;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 32162
    ;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 0

    ;; QUESTION SECTION:
    ;mysql.             IN  A

    ;; ANSWER SECTION:
    mysql.          600 IN  A   172.23.0.2

    ;; Query time: 0 msec
    ;; SERVER: 127.0.0.11#53(127.0.0.11)
    ;; WHEN: Tue Oct 01 23:47:24 UTC 2019
    ;; MSG SIZE  rcvd: 44
    ```

    "回答" セクションには、 `A` に解決されるのレコードが表示され `mysql` `172.23.0.2` ます (IP アドレスの値が異なる可能性が最も高くなります)。 `mysql`は、通常、有効なホスト名ではありませんが、Docker はそのネットワークエイリアスを持つコンテナーの IP アドレスに解決できました ( `--network-alias` 前に使用したフラグを記憶しています)。

    これは次のことを意味します。アプリは、という名前のホストに接続するだけ `mysql` で、データベースと通信します。 それほど簡単ではありません。

## <a name="run-your-app-with-mysql"></a>MySQL を使用してアプリを実行する

Todo アプリは、MySQL 接続設定を指定するために、いくつかの環境変数の設定をサポートしています。 それらは次のとおりです。

- `MYSQL_HOST` -実行中の MySQL サーバーのホスト名
- `MYSQL_USER` -接続に使用するユーザー名
- `MYSQL_PASSWORD` -接続に使用するパスワード
- `MYSQL_DB` -接続後に使用するデータベース

> [!WARNING]
> **環境変数を使用した接続設定の設定** 環境変数を使用して接続設定を設定することは、通常、開発には適していますが、運用環境でアプリケーションを実行する場合はお勧めしません。 理由を理解するには、 [シークレットデータに対して環境変数を使用](https://diogomonica.com/2017/03/27/why-you-shouldnt-use-env-variables-for-secret-data/)しない理由を確認してください。
> より安全なメカニズムは、コンテナーオーケストレーションフレームワークによって提供されるシークレットサポートを使用することです。 ほとんどの場合、これらのシークレットは、実行中のコンテナーにファイルとしてマウントされます。 多くのアプリ (MySQL イメージや todo アプリを含む) も、 `_FILE` ファイルを含むファイルを指すサフィックスを持つ env 変数をサポートしています。
> たとえば、変数を設定すると、 `MYSQL_PASSWORD_FILE` アプリケーションは参照されたファイルの内容を接続パスワードとして使用します。 Docker は、これらの env 変数をサポートするために何も行いません。 アプリで変数を検索し、ファイルの内容を取得する必要があります。

そのすべてを説明したので、開発準備ができているコンテナーを開始します。

1. 上の各環境変数を指定し、コンテナーをアプリネットワークに接続し ` \ ` ます (Windows PowerShell では、文字をに置き換え `` ` `` ます)。

    ```bash hl_lines="3 4 5 6 7"
    docker run -dp 3000:3000 \
      -w /app -v ${PWD}:/app \
      --network todo-app \
      -e MYSQL_HOST=mysql \
      -e MYSQL_USER=root \
      -e MYSQL_PASSWORD=secret \
      -e MYSQL_DB=todos \
      node:12-alpine \
      sh -c "yarn install && yarn run dev"
    ```

1. コンテナーのログ () を見ると `docker logs <container-id>` 、MySQL データベースを使用していることを示すメッセージが表示されます。

    ```plaintext hl_lines="7"
    # Previous log messages omitted
    $ nodemon src/index.js
    [nodemon] 1.19.2
    [nodemon] to restart at any time, enter `rs`
    [nodemon] watching dir(s): *.*
    [nodemon] starting `node src/index.js`
    Connected to mysql db at host mysql
    Listening on port 3000
    ```

1. ブラウザーでアプリを開き、todo リストにいくつかの項目を追加します。

1. MySQL データベースに接続し、アイテムがデータベースに書き込まれていることを証明します。 パスワードは **シークレット**であることに注意してください。

    ```bash
    docker exec -ti <mysql-container-id> mysql -p todos
    ```

    MySQL シェルで、次のように実行します。

    ```plaintext
    mysql> select * from todo_items;
    +--------------------------------------+--------------------+-----------+
    | id                                   | name               | completed |
    +--------------------------------------+--------------------+-----------+
    | c906ff08-60e6-44e6-8f49-ed56a0853e85 | Do amazing things! |         0 |
    | 2912a79e-8486-4bc3-a4c5-460793a575ab | Be awesome!        |         0 |
    +--------------------------------------+--------------------+-----------+
    ```

    もちろん、テーブルには項目が含まれているので、テーブルは異なるように見えます。 しかし、そこに格納されていることがわかります。

Docker 拡張機能を簡単に確認すると、2つのアプリコンテナーが実行されていることがわかります。 しかし、1つのアプリでグループ化されていることは実際にはわかりません。 すぐにこれを実現する方法をご紹介します。

![2つのグループ化されていないアプリコンテナーを示す Docker 拡張機能](media/vs-multi-container-app.png)

## <a name="recap"></a>まとめ

この時点で、別のコンテナーで実行されている外部データベースにデータを格納するアプリケーションが完成しました。 コンテナーネットワークについて少し説明し、DNS を使用してサービス検出を実行する方法について説明しました。

しかし、このアプリケーションを起動するために必要なすべてのことが、少し大きな問題になる可能性があります。 ネットワークを作成し、コンテナーを起動し、すべての環境変数を指定し、ポートを公開する必要があります。 覚えておくことはたくさんありますが、他の人に渡すことが難しくなります。

次のセクションでは、Docker Compose について説明します。 Docker Compose を使用すると、アプリケーションスタックをはるかに簡単に共有し、他のユーザーが1つの (および単純な) コマンドでスピンアップできるようになります。

## <a name="next-steps"></a>次の手順

チュートリアルを続行します。

> [!div class="nextstepaction"]
> [Docker Compose の使用](use-docker-compose.md)
