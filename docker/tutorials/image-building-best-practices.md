---
title: 'Docker チュートリアル-パート 8: イメージのレイヤー化'
description: Docker イメージのイメージレイヤーを確認および管理する方法。
ms.date: 08/04/2020
author: nebuk89
ms.author: ghogen
manager: jillfra
ms.technology: vs-azure
ms.topic: conceptual
ms.workload:
- azure
ms.openlocfilehash: eae21a729f30a0c77fa52e5774a2f5157286dab1
ms.sourcegitcommit: c4212f40df1a16baca1247cac2580ae699f97e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89176733"
---
# <a name="image-layering"></a>画像レイヤー

イメージの構成を確認できることがわかっていますか。 コマンドを使用して、 `docker image history` イメージ内の各レイヤーの作成に使用されたコマンドを確認できます。

1. チュートリアルの `docker image history` `getting-started` 前の手順で作成したイメージ内のレイヤーを表示するには、コマンドを使用します。

    ```bash
    docker image history getting-started
    ```

    次のような出力が表示されます (日付/Id は異なる場合があります)。

    ```plaintext
    IMAGE               CREATED             CREATED BY                                      SIZE                COMMENT
    a78a40cbf866        18 seconds ago      /bin/sh -c #(nop)  CMD ["node" "/app/src/ind…   0B                  
    f1d1808565d6        19 seconds ago      /bin/sh -c yarn install --production            85.4MB              
    a2c054d14948        36 seconds ago      /bin/sh -c #(nop) COPY dir:5dc710ad87c789593…   198kB               
    9577ae713121        37 seconds ago      /bin/sh -c #(nop) WORKDIR /app                  0B                  
    b95baba1cfdb        13 days ago         /bin/sh -c #(nop)  CMD ["node"]                 0B                  
    <missing>           13 days ago         /bin/sh -c #(nop)  ENTRYPOINT ["docker-entry…   0B                  
    <missing>           13 days ago         /bin/sh -c #(nop) COPY file:238737301d473041…   116B                
    <missing>           13 days ago         /bin/sh -c apk add --no-cache --virtual .bui…   5.35MB              
    <missing>           13 days ago         /bin/sh -c #(nop)  ENV YARN_VERSION=1.21.1      0B                  
    <missing>           13 days ago         /bin/sh -c addgroup -g 1000 node     && addu…   74.3MB              
    <missing>           13 days ago         /bin/sh -c #(nop)  ENV NODE_VERSION=12.14.1     0B                  
    <missing>           13 days ago         /bin/sh -c #(nop)  CMD ["/bin/sh"]              0B                  
    <missing>           13 days ago         /bin/sh -c #(nop) ADD file:e69d441d729412d24…   5.59MB   
    ```

    各線は、イメージ内のレイヤーを表します。 ここに表示されているのは、一番下の基本レイヤーが一番上に表示されます。 これを使用すると、各レイヤーのサイズをすばやく確認し、大きな画像の診断に役立てることもできます。

1. いくつかの行が切り捨てられていることがわかります。 フラグを追加すると `--no-trunc` 、完全な出力が得られます ([はい、切り捨てられたフラグを使用して、切り捨てられた出力を取得します)。

    ```bash
    docker image history --no-trunc getting-started
    ```

## <a name="layer-caching"></a>レイヤーキャッシュ

これで、レイヤーの動作がわかりました。次は、コンテナーイメージのビルド時間を短縮するための重要な教訓を示しています。

> レイヤーが変更されたら、すべてのダウンストリームレイヤーも再作成する必要があります。

もう一度使用していた Dockerfile を見てみましょう...

```dockerfile
FROM node:12-alpine
WORKDIR /app
COPY . .
RUN yarn install --production
CMD ["node", "/app/src/index.js"]
```

イメージ履歴出力に戻ると、Dockerfile の各コマンドがイメージの新しいレイヤーになります。 イメージに変更を加えた場合は、yarn の依存関係を再インストールする必要があることに注意してください。 これを修正する方法はありますか。 ビルドするたびに同じ依存関係を配布することはあまり意味がありません。

この問題を解決するには、依存関係のキャッシュをサポートするように、Dockerfile を再構築します。 ノードベースのアプリケーションでは、これらの依存関係はファイルで定義され `package.json` ます。 そのため、最初にそのファイルのみをコピーした場合は、依存関係をインストールして *から* 、他のすべてをコピーします。 次に、に変更があった場合にのみ、yarn 依存関係を再作成し `package.json` ます。 ご理解ください。

1. Dockerfile を更新して最初のファイルにコピーし `package.json` 、依存関係をインストールしてから、の他のすべてをコピーします。

    ```dockerfile hl_lines="3 4 5"
    FROM node:12-alpine
    WORKDIR /app
    COPY package.json yarn.lock ./
    RUN yarn install --production
    COPY . .
    CMD ["node", "/app/src/index.js"]
    ```

1. を使用して新しいイメージを作成し `docker build` ます。

    ```bash
    docker build -t getting-started .
    ```

    次のような出力が表示できます...

    ```plaintext
    Sending build context to Docker daemon  219.1kB
    Step 1/6 : FROM node:12-alpine
    ---> b0dc3a5e5e9e
    Step 2/6 : WORKDIR /app
    ---> Using cache
    ---> 9577ae713121
    Step 3/6 : COPY package* yarn.lock ./
    ---> bd5306f49fc8
    Step 4/6 : RUN yarn install --production
    ---> Running in d53a06c9e4c2
    yarn install v1.17.3
    [1/4] Resolving packages...
    [2/4] Fetching packages...
    info fsevents@1.2.9: The platform "linux" is incompatible with this module.
    info "fsevents@1.2.9" is an optional dependency and failed compatibility check. Excluding it from installation.
    [3/4] Linking dependencies...
    [4/4] Building fresh packages...
    Done in 10.89s.
    Removing intermediate container d53a06c9e4c2
    ---> 4e68fbc2d704
    Step 5/6 : COPY . .
    ---> a239a11f68d8
    Step 6/6 : CMD ["node", "/app/src/index.js"]
    ---> Running in 49999f68df8f
    Removing intermediate container 49999f68df8f
    ---> e709c03bc597
    Successfully built e709c03bc597
    Successfully tagged getting-started:latest
    ```

    すべてのレイヤーがリビルドされていることがわかります。 Dockerfile を大幅に変更したため、まったく問題ありません。

1. 次に、ファイルに変更を加え `src/static/index.html` ます (たとえば、 `<title>` 「すばらしい Todo アプリ」に変更します)。

1. をもう一度使用して Docker イメージをビルドし `docker build` ます。 今回の出力は少し異なります。

    ```plaintext hl_lines="5 8 11"
    Sending build context to Docker daemon  219.1kB
    Step 1/6 : FROM node:12-alpine
    ---> b0dc3a5e5e9e
    Step 2/6 : WORKDIR /app
    ---> Using cache
    ---> 9577ae713121
    Step 3/6 : COPY package* yarn.lock ./
    ---> Using cache
    ---> bd5306f49fc8
    Step 4/6 : RUN yarn install --production
    ---> Using cache
    ---> 4e68fbc2d704
    Step 5/6 : COPY . .
    ---> cccde25a3d9a
    Step 6/6 : CMD ["node", "/app/src/index.js"]
    ---> Running in 2be75662c150
    Removing intermediate container 2be75662c150
    ---> 458e5c6f080c
    Successfully built 458e5c6f080c
    Successfully tagged getting-started:latest
    ```

    まず、ビルドがはるかに高速であることがわかります。 また、手順1-4 のすべてが含まれていることがわかり `Using cache` ます。 では、バンザイ! ビルドキャッシュを使用しています。 このイメージをプッシュしてプルすると、このイメージの更新もはるかに高速になります。 バンザイ!

## <a name="multi-stage-builds"></a>複数段階のビルド

このチュートリアルではあまり詳しく説明しませんが、マルチステージビルドは、複数のステージを使用してイメージを作成するための非常に強力なツールです。 これらにはいくつかの利点があります。

- ランタイム依存関係からのビルド時依存関係の分離
- アプリの実行に必要なもの *のみ* を配布することで、イメージ全体のサイズを縮小します

### <a name="maventomcat-example"></a>Maven/Tomcat の例

Java ベースのアプリケーションをビルドする場合、ソースコードを Java バイトコードにコンパイルするには JDK が必要です。 ただし、その JDK は運用環境では必要ありません。 また、Maven や Gradle などのツールを使用して、アプリのビルドに役立てることもできます。
これらは、最終的なイメージでも必要ではありません。 複数ステージビルドのヘルプ。

```dockerfile
FROM maven AS build
WORKDIR /app
COPY . .
RUN mvn package

FROM tomcat
COPY --from=build /app/target/file.war /usr/local/tomcat/webapps 
```

この例では、1つのステージ (と呼ばれ `build` ます) を使用して、Maven を使用した実際の Java ビルドを実行します。 2番目の段階 (から開始) は、 `FROM tomcat` ステージからのファイルをコピーし `build` ます。 最終的なイメージは、作成される最後のステージ (フラグを使用してオーバーライドでき `--target` ます) のみです。

### <a name="react-example"></a>応答の例

アプリケーションの開発時には、JS コード (通常は JSX)、SASS スタイルシートなどを静的 HTML、JS、CSS にコンパイルするためのノード環境が必要です。 サーバー側のレンダリングを実行していない場合は、実稼働ビルド用のノード環境は必要ありません。 静的リソースが静的 nginx コンテナーに発送されないのはなぜですか。

```dockerfile
FROM node:12 AS build
WORKDIR /app
COPY package* yarn.lock ./
RUN yarn install
COPY public ./public
COPY src ./src
RUN yarn run build

FROM nginx:alpine
COPY --from=build /app/build /usr/share/nginx/html
```

ここでは、イメージを使用して `node:12` ビルド (レイヤーキャッシュの最大化) を実行し、その出力を nginx コンテナーにコピーします。 すばらしいですね。

## <a name="recap"></a>まとめ

イメージがどのように構造化されているかを理解することで、イメージを短時間で作成し、出荷する変更を減らすことができます。 また、複数ステージのビルドでは、ビルド時の依存関係をランタイム依存関係から分離することで、イメージ全体のサイズを縮小し、最終的なコンテナーのセキュリティを向上させることもできます。

## <a name="next-steps"></a>次の手順

チュートリアルを続行します。

> [!div class="nextstepaction"]
> [クラウドへのデプロイ](deploy-to-cloud.md)