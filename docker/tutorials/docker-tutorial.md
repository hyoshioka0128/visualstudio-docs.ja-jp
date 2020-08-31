---
title: Docker チュートリアル-Docker の概要
description: Visual Studio Code を使用した Docker の操作の基本について説明した、複数の手順から成るチュートリアルです。
ms.date: 08/04/2020
author: nebuk89
ms.author: ghogen
manager: jillfra
ms.technology: vs-azure
ms.topic: conceptual
ms.workload:
- azure
next_page: app.md
ms.openlocfilehash: 9961810ad408a384db46439235b0b7acab325062
ms.sourcegitcommit: c4212f40df1a16baca1247cac2580ae699f97e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89176748"
---
# <a name="tutorial-get-started-with-docker"></a>チュートリアル: Docker の概要

このチュートリアルでは、データベースと共に複数のコンテナーを使用し、Docker Compose を使用するなど、Docker アプリの作成とデプロイについて学習します。 また、コンテナー化されたアプリを Azure にデプロイします。

## <a name="start-the-tutorial"></a>チュートリアルを開始する

このチュートリアルを開始するためのコマンドを既に実行している場合は、おめでとうございます。  それ以外の場合は、コマンドプロンプトまたは bash ウィンドウを開き、次のコマンドを実行します。

```cli
docker run -d -p 80:80 docker/getting-started
```

いくつかのフラグが使用されていることがわかります。 詳細については、次の情報を参照してください。

- `-d` -デタッチモード (バックグラウンド) でコンテナーを実行します。
- `-p 80:80` -ホストのポート80をコンテナー内のポート80にマップします。
- `docker/getting-started` -使用するイメージ

> [!TIP]
> 単一の文字のフラグを組み合わせて、完全なコマンドを短縮することができます。
> 例として、上記のコマンドは次のように記述できます。
>
> ```cli
> docker run -dp 80:80 docker/getting-started
> ```

## <a name="the-vs-code-extension"></a>VS Code の拡張機能

ここでは、Docker VS Code 拡張機能について説明します。これにより、コンピューター上で実行されているコンテナーを簡単に確認できます。 コンテナーログにすばやくアクセスでき、コンテナー内のシェルを取得できます。これにより、コンテナーのライフサイクル (停止、削除など) を簡単に管理できます。

拡張機能にアクセスするには、 [こちら](https://code.visualstudio.com/docs/containers/overview)の手順に従ってください。 左側の Docker アイコンを使用して、Docker ビューを開きます。 拡張機能を開いた場合は、このチュートリアルが実行されていることがわかります。 コンテナー名 ( `angry_taussig` 以下) はランダムに作成された名前です。 そのため、ほとんどの場合、名前が異なる可能性があります。

![Docker 拡張機能で実行されているチュートリアルコンテナー](media/vs-tutorial-in-extension.png)

## <a name="what-is-a-container"></a>コンテナーとは

コンテナーを実行しました。コンテナーと *は* 何ですか。 単純に、コンテナーは、ホストコンピューター上の他のすべてのプロセスから分離された、コンピューター上の別のプロセスです。 この分離により、 [カーネルの名前空間と cgroups (](https://medium.com/@saschagrunert/demystifying-containers-part-i-kernel-space-2c53d6979504)が使用されます。 Linux にある機能は、長い間、機能します。 Docker は、これらの機能を使いやすく、使いやすいものにしました。

> [!NOTE]
> **コンテナーを最初から作成する** コンテナーが最初からどのように作成されているかを確認する場合は、Liz ライスの水色セキュリティにビデオがあります。このビデオでは、次のようにして、最初からコンテナーを作成します。
>
> [!VIDEO https://www.youtube-nocookie.com/embed/8fi7uSYlOdc]

## <a name="what-is-a-container-image"></a>コンテナーイメージとは

コンテナーを実行する場合は、分離されたファイルシステムを使用します。 このカスタムファイルシステムは、 **コンテナーイメージ**によって提供されます。 イメージにはコンテナーのファイルシステムが含まれているため、アプリケーションを実行するために必要なすべてのもの (すべての依存関係、構成、スクリプト、バイナリなど) が含まれている必要があります。 イメージには、環境変数、実行する既定のコマンド、その他のメタデータなど、コンテナーのその他の構成も含まれます。

後でイメージについて詳しく説明し、レイヤー、ベストプラクティスなどのトピックについて説明します。

> [!NOTE]
> に慣れている場合は `chroot` 、コンテナーをの拡張バージョンと考えて `chroot` ください。 ファイルシステムは単にイメージから取得されます。 しかし、コンテナーは、chroot を使用するだけでは使用できない分離を追加します。

## <a name="next-steps"></a>次の手順

チュートリアルを続行します。

> [!div class="nextstepaction"]
> [アプリケーション](your-application.md)
