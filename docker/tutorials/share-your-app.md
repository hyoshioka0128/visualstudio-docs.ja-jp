---
title: 'Docker チュートリアル-パート 3: アプリを共有する'
description: Docker Hub レジストリを使用して Docker イメージを共有する方法について説明します。
ms.date: 08/04/2020
author: nebuk89
ms.author: ghogen
manager: jillfra
ms.technology: vs-azure
ms.topic: conceptual
ms.workload:
- azure
ms.openlocfilehash: d5bd7a2d79bf6da710fd0f5803c2415781160143
ms.sourcegitcommit: c4212f40df1a16baca1247cac2580ae699f97e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89176747"
---
# <a name="share-your-app"></a>アプリを共有する

イメージを作成したので、共有しましょう。 Docker イメージを共有するには、Docker レジストリを使用する必要があります。 既定のレジストリは Docker Hub であり、使用していたすべてのイメージが含まれています。

## <a name="create-a-repo"></a>リポジトリを作成する

イメージをプッシュするには、まず、Docker Hub でリポジトリを作成する必要があります。

1. [Docker Hub](https://hub.docker.com)にアクセスし、必要に応じてログインします。

1. [ **リポジトリの作成** ] ボタンをクリックします。

1. リポジトリ名には、を使用 `getting-started` します。 可視性がであることを確認し `Public` ます。

1. [ **作成** ] ボタンをクリックします。

ページの右側を見ると、 **Docker コマンド**という名前のセクションが表示されます。 これにより、このリポジトリにプッシュするために実行する必要があるコマンドの例が示されます。

![プッシュを使用した Docker コマンドの例](media/push-command.png)

## <a name="push-the-image"></a>イメージをプッシュする

1. コマンドラインで、Docker Hub に表示されるプッシュコマンドを実行します。 コマンドは、"docker" ではなく、名前空間を使用することに注意してください。

    ```plaintext
    $ docker push docker/getting-started
    The push refers to repository [docker.io/docker/getting-started]
    An image does not exist locally with the tag: docker/getting-started
    ```

    なぜ失敗したのでしょうか。 プッシュコマンドは、docker/はじめにという名前のイメージを探していましたが、見つかりませんでした。 を実行すると `docker image ls` 、どちらも表示されません。

    この問題を解決するには、別の名前を付けるために作成した既存のイメージを "タグ付けする" 必要があります。

1. コマンドを使用して、Docker Hub にサインインし `docker login -u <username>` ます。

1. コマンドを使用して、 `docker tag` `getting-started` イメージに新しい名前を付けます。 必ず `<username>` DOCKER ID でお試しください。

    ```bash
    docker tag getting-started <username>/getting-started
    ```

1. 次に、プッシュコマンドを再試行します。 Docker Hub から値をコピーする場合は、 `tagname` イメージ名にタグを追加していないので、部分を削除できます。 タグを指定しない場合、Docker はというタグを使用し `latest` ます。

    ```bash
    docker push <username>/getting-started
    ```

## <a name="run-the-image-on-a-new-instance"></a>新しいインスタンスでイメージを実行する

イメージがビルドされ、レジストリにプッシュされたので、このコンテナーイメージを見たことがない新しいインスタンスでアプリを実行してみてください。 これを行うには、[Docker で再生] を使用します。

1. ブラウザーを開いて [Docker で再生](http://play-with-docker.com)します。

1. Docker Hub アカウントを使用してサインインします。

1. ログインしたら、左側のバーにある [+ 新しいインスタンスの追加] リンクをクリックします。 (表示されない場合は、ブラウザーを少し広くしてください)。数秒後に、ターミナルウィンドウがブラウザーで開きます。

    ![Docker add new instance で再生する](media/pwd-add-new-instance.png)

1. ターミナルで、新しくプッシュされたアプリを起動します。

    ```bash
    docker run -dp 3000:3000 <username>/getting-started
    ```

    イメージがプルダウンされ、最終的に起動します。

1. 3000バッジが表示されたら、それをクリックすると、変更内容を含むアプリが表示されます。 バンザイ! 3000バッジが表示されない場合は、[ポートを **開く** ] ボタンをクリックし、「3000」と入力します。

## <a name="recap"></a>まとめ

このセクションでは、イメージをレジストリにプッシュして共有する方法を学習しました。 次に、新しいインスタンスに移動し、新たにプッシュされたイメージを実行できました。 これは CI パイプラインでよく見られます。パイプラインでは、イメージを作成してレジストリにプッシュした後、実稼働環境で最新バージョンのイメージを使用できます。

これで理解できました。最後のセクションの最後に、アプリを再起動すると、すべての todo リスト項目が失われたことを思い出してください。 これは、ユーザーエクスペリエンスが優れているわけではないので、次に、再起動の間にデータを保持する方法について学習します。

## <a name="next-steps"></a>次の手順

チュートリアルを続行します。

> [!div class="nextstepaction"]
> [データベースの永続化](persist-your-data.md)