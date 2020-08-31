---
title: 'Docker チュートリアル-パート 5: バインドマウントの使用'
description: バインドマウントを使用してホスト上のマウントポイントを制御する方法について説明します。
ms.date: 08/04/2020
author: nebuk89
ms.author: ghogen
manager: jillfra
ms.technology: vs-azure
ms.topic: conceptual
ms.workload:
- azure
ms.openlocfilehash: 6474179a0714f2407ac37e724b997139206a91fb
ms.sourcegitcommit: c4212f40df1a16baca1247cac2580ae699f97e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89176740"
---
# <a name="use-bind-mounts"></a>バインドマウントを使用する

前の章では、データベースのデータを永続化するために、 **名前付きボリューム** について説明し、使用しました。 名前付きボリュームは、データの格納 *場所* を気にする必要がないため、単にデータを格納する場合に適しています。

**バインドマウント**では、ホスト上の正確なマウントポイントを制御します。 これを使用してデータを永続化することができますが、多くの場合、コンテナーに追加データを提供するために使用されます。 アプリケーションで作業している場合は、バインドマウントを使用してソースコードをコンテナーにマウントし、コードの変更を確認して応答し、変更をすぐに確認できるようにすることができます。

ノードベースのアプリケーションの場合、 [nodemon](https://npmjs.com/package/nodemon) はファイルの変更を監視し、アプリケーションを再起動するための優れたツールです。 他のほとんどの言語やフレームワークにも同等のツールがあります。

## <a name="quick-volume-type-comparisons"></a>クイックボリュームの種類の比較

バインドマウントと名前付きボリュームは、Docker エンジンに付属する2つの主な種類のボリュームです。 ただし、その他のユースケース ([SFTP](https://github.com/vieux/docker-volume-sshfs)、 [ceph](https://ceph.com/geen-categorie/getting-started-with-the-docker-rbd-volume-plugin/)、 [NetApp](https://netappdvp.readthedocs.io/en/stable/)、 [S3](https://github.com/elementar/docker-s3-volume)など) をサポートするために、追加のボリュームドライバーを使用できます。

| プロパティ | 名前付きボリューム | バインド マウント |
| -------- | ------------- | ----------- |
| ホストの場所 | Docker の選択 | 制御 |
| Mount の例 (を使用 `-v` ) | マイボリューム:/usr/local/data | /path/to/data:/usr/local/data |
| コンテナーの内容を新しいボリュームに設定します | はい | いいえ |
| ボリュームドライバーのサポート | はい | いいえ |

## <a name="start-a-dev-mode-container"></a>開発モードのコンテナーを開始する

開発ワークフローをサポートするためにコンテナーを実行するには、次の操作を行います。

- ソースコードをコンテナーにマウントする
- "Dev" 依存関係を含め、すべての依存関係をインストールします。
- Nodemon を開始して、ファイルシステムの変更を監視します

1. 以前のコンテナーが実行されていないことを確認し `getting-started` ます。

1. 次のコマンドを実行し ` \ ` ます (Windows PowerShell では、文字をに置き換え `` ` `` ます)。 後で何が起こっているかを学習します。

    ```bash
    docker run -dp 3000:3000 \
        -w /app -v ${PWD}:/app \
        node:12-alpine \
        sh -c "yarn install && yarn run dev"
    ```

    - `-dp 3000:3000` -以前と同じです。 デタッチ (バックグラウンド) モードで実行し、ポートマッピングを作成する
    - `-w /app` -"作業ディレクトリ" またはコマンドが実行される現在のディレクトリを設定します。
    - `-v ${PWD}:/app`-コンテナー内のホストから現在のディレクトリをディレクトリにマウントします。 `/app`
    - `node:12-alpine` -使用するイメージ。 これは、Dockerfile からのアプリの基本イメージであることに注意してください。
    - `sh -c "yarn install && yarn run dev"` -コマンド。 (Alpine ではなく) を使用してシェルを開始 `sh` `bash` し、 `yarn install` *すべて* の依存関係をインストールして実行するために実行してい `yarn run dev` ます。 を見ると `package.json` 、 `dev` スクリプトが開始されていることがわかり `nodemon` ます。

1. ログは、を使用して監視でき `docker logs -f <container-id>` ます。 次のような画面が表示されます。

    ```bash
    docker logs -f <container-id>
    $ nodemon src/index.js
    [nodemon] 1.19.2
    [nodemon] to restart at any time, enter `rs`
    [nodemon] watching dir(s): *.*
    [nodemon] starting `node src/index.js`
    Using sqlite database at /etc/todos/todo.db
    Listening on port 3000
    ```

    ログの監視が完了したら、を終了し `Ctrl` + `C` ます。

1. 次に、アプリに変更を加えます。 ファイルで [ `src/static/js/app.js` **項目の追加** ] ボタンを [ **追加**] に変更します。 この変更は109行目に表示されます。

    ```diff
    -                         {submitting ? 'Adding...' : 'Add Item'}
    +                         {submitting ? 'Adding...' : 'Add'}
    ```

1. ページを更新 (または開く) するだけで、変更がブラウザーに反映されたことがすぐに表示されます。 ノードサーバーが再起動されるまで数秒かかる場合があるため、エラーが発生した場合は、数秒後に更新を試してください。

    ![[追加] ボタンの更新されたラベルのスクリーンショット](media/updated-add-button.png)

1. その他の変更は自由に行うことができます。 完了したら、コンテナーを停止し、を使用して新しいイメージを作成し `docker build -t getting-started .` ます。

バインドマウントの使用は、ローカル開発のセットアップでは *非常に* 一般的です。 利点は、開発用コンピューターにすべてのビルドツールと環境がインストールされている必要がないことです。 1つのコマンドを使用すると、 `docker run` 開発環境が引き出され、準備ができます。 Docker Compose については、後の手順で説明します。これにより、コマンドの簡略化に役立ちます (既に多数のフラグが取得されています)。

## <a name="recap"></a>まとめ

この時点で、データベースを永続化し、投資家と創業時のニーズと要求に迅速に対応することができます。 バンザイ! でも、どうでしょうか。 すばらしいニュースを受け取りました。

**プロジェクトは今後の開発のために選択されています。**

運用環境を準備するには、SQLite での作業からデータベースを簡単に拡張できるものに移行する必要があります。 わかりやすくするために、リレーショナルデータベースを使用して、MySQL を使用するようにアプリケーションを切り替えることができます。 MySQL を実行するにはどうすればよいでしょうか。 コンテナーが相互に通信できるようにするにはどうすればよいですか。 次のことについて説明します。

## <a name="next-steps"></a>次の手順

チュートリアルを続行します。

> [!div class="nextstepaction"]
> [複数コンテナー アプリ](multi-container-apps.md)