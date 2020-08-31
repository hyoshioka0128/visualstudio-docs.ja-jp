---
title: 'Docker チュートリアル-パート 7: Docker Compose の使用'
description: Docker Compose をインストールして使用する方法について説明します。
ms.date: 08/04/2020
author: nebuk89
ms.author: ghogen
manager: jillfra
ms.technology: vs-azure
ms.topic: conceptual
ms.workload:
- azure
ms.openlocfilehash: 81f70612b05920ea58c752a878831f1d6de34098
ms.sourcegitcommit: c4212f40df1a16baca1247cac2580ae699f97e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89176725"
---
# <a name="use-docker-compose"></a>Docker Compose の使用

[Docker Compose](https://docs.docker.com/compose/) は、複数コンテナーアプリケーションを定義して共有するために開発されたツールです。 構成を使用すると、YAML ファイルを作成してサービスを定義できます。また、1つのコマンドを使用して、すべてをスピンアップまたは破棄することができます。

構成を使用する *大きな* 利点は、ファイルでアプリケーションスタックを定義し、プロジェクトリポジトリのルート (現在はバージョン管理) に保持し、他のユーザーが簡単にプロジェクトに投稿できるようにすることです。 リポジトリを複製して作成アプリを開始する必要があるのは、だれかだけです。 実際、ここでは、GitHub/GitLab にいくつかのプロジェクトが表示されます。

では、どのように開始するのでしょうか。

## <a name="install-docker-compose"></a>Docker Compose をインストールする

Windows または Mac 用の Docker Desktop をインストールした場合は、既に Docker Compose があります。 Play-Docker インスタンスにも既に Docker Compose がインストールされています。 Linux マシンを使用している場合は、 [こちらの手順に](https://docs.docker.com/compose/install/)従って Docker Compose をインストールする必要があります。

インストールが完了すると、次のものを実行してバージョン情報を確認できるようになります。

```bash
docker-compose version
```

## <a name="create-the-compose-file"></a>作成ファイルを作成する

1. アプリプロジェクトのルートに、という名前のファイルを作成 `docker-compose.yml` します。

1. 作成ファイルでは、最初にスキーマのバージョンを定義します。 ほとんどの場合、サポートされている最新バージョンを使用することをお勧めします。 現在のスキーマのバージョンと互換性のマトリックスについては、「 [ファイルの作成](https://docs.docker.com/compose/compose-file/) 」を参照してください。

    ```yaml
    version: "3.7"
    ```

1. 次に、アプリケーションの一部として実行するサービス (またはコンテナー) の一覧を定義します。

    ```yaml hl_lines="3"
    version: "3.7"

    services:
    ```

ここで、サービスを一度に1つの作成ファイルに移行します。

## <a name="define-the-app-service"></a>App Service を定義する

これは、アプリコンテナーを定義するために使用したコマンドであることを思い出してください ( ` \ ` Windows PowerShell では文字をに置き換えてい `` ` `` ます)。

```bash
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

1. まず、コンテナーのサービスエントリとイメージを定義します。 サービスの任意の名前を選択できます。 名前は自動的にネットワークエイリアスになります。これは、MySQL サービスを定義するときに便利です。

    ```yaml hl_lines="4 5"
    version: "3.7"

    services:
      app:
        image: node:12-alpine
    ```

1. 通常、コマンドは定義の近くに表示されますが、 `image` 順序付けに関する要件はありません。 では、ファイルに移動してみましょう。

    ```yaml hl_lines="6"
    version: "3.7"

    services:
      app:
        image: node:12-alpine
        command: sh -c "yarn install && yarn run dev"
    ```

1. サービスのを `-p 3000:3000` 定義して、コマンドの一部を移行し `ports` ます。 ここでは [短い構文](https://docs.docker.com/compose/compose-file/#short-syntax-1) を使用しますが、さらに詳細な [長い構文](https://docs.docker.com/compose/compose-file/#long-syntax-1) も使用できます。

    ```yaml hl_lines="7 8"
    version: "3.7"

    services:
      app:
        image: node:12-alpine
        command: sh -c "yarn install && yarn run dev"
        ports:
          - 3000:3000
    ```

1. 次に、との定義を使用して、作業ディレクトリ ( `-w /app` ) とボリュームマッピング () の両方を移行し `-v ${PWD}:/app` `working_dir` `volumes` ます。 ボリュームには、 [短い](https://docs.docker.com/compose/compose-file/#short-syntax-3) 構文と [長い](https://docs.docker.com/compose/compose-file/#long-syntax-3) 構文もあります。

   Docker Compose ボリューム定義の利点の1つは、現在のディレクトリから相対パスを使用できることです。

    ```yaml hl_lines="9 10 11"
    version: "3.7"

    services:
      app:
        image: node:12-alpine
        command: sh -c "yarn install && yarn run dev"
        ports:
          - 3000:3000
        working_dir: /app
        volumes:
          - ./:/app
    ```

1. 最後に、キーを使用して環境変数の定義を移行し `environment` ます。

    ```yaml hl_lines="12 13 14 15 16"
    version: "3.7"

    services:
      app:
        image: node:12-alpine
        command: sh -c "yarn install && yarn run dev"
        ports:
          - 3000:3000
        working_dir: /app
        volumes:
          - ./:/app
        environment:
          MYSQL_HOST: mysql
          MYSQL_USER: root
          MYSQL_PASSWORD: secret
          MYSQL_DB: todos
    ```

### <a name="define-the-mysql-service"></a>MySQL サービスを定義する

次に、MySQL サービスを定義します。 そのコンテナーに使用したコマンドは、次のようになりました ( ` \ ` Windows PowerShell では、文字をに置き換えて `` ` `` ください)。

```bash
docker run -d \
  --network todo-app --network-alias mysql \
  -v todo-mysql-data:/var/lib/mysql \
  -e MYSQL_ROOT_PASSWORD=secret \
  -e MYSQL_DATABASE=todos \
  mysql:5.7
```

1. まず、新しいサービスを定義し、 `mysql` ネットワークエイリアスを自動的に取得するように名前を指定します。 使用するイメージも指定します。

    ```yaml hl_lines="6 7"
    version: "3.7"

    services:
      app:
        # The app service definition
      mysql:
        image: mysql:5.7
    ```

1. 次に、ボリュームマッピングを定義します。 でコンテナーを実行すると `docker run` 、名前付きボリュームが自動的に作成されます。 ただし、これは、を作成して実行する場合には発生しません。 最上位のセクションでボリュームを定義 `volumes:` し、サービス構成でマウントポイントを指定する必要があります。ボリューム名だけを指定するだけで、既定のオプションが使用されます。 ただし、 [他](https://docs.docker.com/compose/compose-file/#volume-configuration-reference) にも多くのオプションが用意されています。

    ```yaml hl_lines="8 9 10 11 12"
    version: "3.7"

    services:
      app:
        # The app service definition
      mysql:
        image: mysql:5.7
        volumes:
          - todo-mysql-data:/var/lib/mysql
    
    volumes:
      todo-mysql-data:
    ```

1. 最後に、必要なのは環境変数を指定することだけです。

    ```yaml hl_lines="10 11 12"
    version: "3.7"

    services:
      app:
        # The app service definition
      mysql:
        image: mysql:5.7
        volumes:
          - todo-mysql-data:/var/lib/mysql
        environment: 
          MYSQL_ROOT_PASSWORD: secret
          MYSQL_DATABASE: todos
    
    volumes:
      todo-mysql-data:
    ```

この時点で、完全は次のようになり `docker-compose.yml` ます。

```yaml
version: "3.7"

services:
  app:
    image: node:12-alpine
    command: sh -c "yarn install && yarn run dev"
    ports:
      - 3000:3000
    working_dir: /app
    volumes:
      - ./:/app
    environment:
      MYSQL_HOST: mysql
      MYSQL_USER: root
      MYSQL_PASSWORD: secret
      MYSQL_DB: todos

  mysql:
    image: mysql:5.7
    volumes:
      - todo-mysql-data:/var/lib/mysql
    environment: 
      MYSQL_ROOT_PASSWORD: secret
      MYSQL_DATABASE: todos

volumes:
  todo-mysql-data:
```

## <a name="run-the-application-stack"></a>アプリケーションスタックを実行する

これでファイルが完成しました `docker-compose.yml` 。開始することができます。

1. まず、アプリとデータベースの他のコピー (および) が実行されていないことを確認し `docker ps` `docker rm -f <ids>` ます。

1. コマンドを使用して、アプリケーションスタックを起動し `docker-compose up` ます。 `-d`すべてをバックグラウンドで実行するフラグを追加します。 または、作成ファイルを右クリックし、VS Code サイドバーの [ **作成** ] オプションを選択します。 

    ```bash
    docker-compose up -d
    ```

    これを実行すると、次のような出力が表示できます。

    ```plaintext
    Creating network "app_default" with the default driver
    Creating volume "app_todo-mysql-data" with default driver
    Creating app_app_1   ... done
    Creating app_mysql_1 ... done
    ```

    ボリュームもネットワーク上に作成されていることがわかります。 既定では、Docker Compose によって、アプリケーションスタック専用のネットワークが自動的に作成されます (作成ファイルで定義していない理由があります)。

1. コマンドを使用してログを確認し `docker-compose logs -f` ます。 各サービスのログが1つのストリームにインターリーブされます。 これは、タイミングに関連する問題を監視する場合に非常に便利です。 `-f`このフラグはログに従っているため、生成されるライブ出力が得られます。

    まだ表示されていない場合は、次のような出力が表示されます。

    ```plaintext
    mysql_1  | 2019-10-03T03:07:16.083639Z 0 [Note] mysqld: ready for connections.
    mysql_1  | Version: '5.7.27'  socket: '/var/run/mysqld/mysqld.sock'  port: 3306  MySQL Community Server (GPL)
    app_1    | Connected to mysql db at host mysql
    app_1    | Listening on port 3000
    ```

    サービス名は、メッセージを区別するために、(多くの場合は色付きの) 行の先頭に表示されます。 特定のサービスのログを表示する場合は、ログコマンドの末尾にサービス名 (たとえば、) を追加し `docker-compose logs -f app` ます。

    > [!TIP]
    > **アプリを起動する前に DB を待機し** ていますアプリが起動すると、実際には、MySQL が起動して準備が整うまで待機してから、別のコンテナーを起動する前に、別のコンテナーが完全に起動され、実行されて、準備が整うのを待機するためのサポートが組み込まれていないことを it.Docます。 ノードベースのプロジェクトでは、 [待機ポート](https://github.com/dwmkerr/wait-port) の依存関係を使用できます。 類似のプロジェクトは、他の言語/フレームワークにも存在します。

1. この時点で、アプリを開いて、実行中であることを確認できます。 こんにちは。 1つのコマンドを実行しています。

## <a name="see-the-app-stack-in-the-docker-extension"></a>Docker 拡張機能のアプリスタックを表示する

Docker 拡張機能を確認する場合は、"歯車" と "group by" を使用してグループ化オプションを変更できます。 このインスタンスでは、次のように、構成プロジェクト名でグループ化されたコンテナーを表示します。

![VS 拡張機能と作成](media/vs-app-project-collapsed.png)

ネットワークを回転させると、作成した2つのコンテナーが作成ファイルに表示されます。

![構成が展開された VS 拡張機能](media/vs-app-project-expanded.png)

## <a name="tear-it-all-down"></a>すべてを破棄する

すべてを停止する準備ができたら、を実行する `docker-compose down` か、VS Code Docker 拡張機能のコンテナーの一覧でアプリケーションを右クリックし、[構成] [ **下へ**] を選択します。 コンテナーが停止し、ネットワークが削除されます。

> [!WARNING]
> **ボリュームの削除** 既定では、作成ファイル内の名前付きボリュームは、の実行時に削除されません `docker-compose down` 。 ボリュームを削除する場合は、フラグを追加する必要があり `--volumes` ます。

いったん破棄されると、別のプロジェクトに切り替え `docker-compose up` て実行し、そのプロジェクトに貢献する準備ができます。 それほど簡単ではありません。

## <a name="recap"></a>まとめ

このセクションでは、Docker Compose について説明したうえで、マルチサービスアプリケーションの定義と共有を大幅に簡略化する方法について説明しました。 使用していたコマンドを適切な作成形式に変換することによって、作成ファイルを作成しました。

この時点で、チュートリアルを終了します。 ただし、使用している Dockerfile には大きな問題があるため、イメージの作成に関するベストプラクティスがいくつかあります。 では、見てみましょう。

## <a name="next-steps"></a>次の手順

チュートリアルを続行します。

> [!div class="nextstepaction"]
> [イメージ作成のベストプラクティス](image-building-best-practices.md)
