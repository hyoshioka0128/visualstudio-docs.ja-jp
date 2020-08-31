---
title: Docker チュートリアル-次の内容
description: クラウドネイティブコンピューティングファンデーションプロジェクトを使用して、オーケストレーションで Docker アプリを拡張するためのオプションについて説明します。
ms.date: 08/04/2020
author: nebuk89
ms.author: ghogen
manager: jillfra
ms.technology: vs-azure
ms.topic: conceptual
ms.workload:
- azure
ms.openlocfilehash: f93185641a0814797b66eae90714e04cac83f7e5
ms.sourcegitcommit: c4212f40df1a16baca1247cac2580ae699f97e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89176723"
---
# <a name="whats-next"></a>次の内容

チュートリアルは完了しましたが、コンテナーについて学習することはまだたくさんあります。
ここでは詳しく説明しませんが、その他のいくつかの領域は次のようになります。

## <a name="container-orchestration"></a>コンテナーのオーケストレーション

運用環境でコンテナーを実行することは困難です。 コンピューターにログインして、単にまたはを実行する必要はありません `docker run` `docker-compose up` 。 なぜでしょうか。 コンテナーが死んだ場合はどうなるのでしょうか。 複数のコンピューター間でどのようにスケールを設定しますか。 コンテナーオーケストレーションはこの問題を解決します。 Kubernetes、群れ、Nomad、AKS などのツールはすべてこの問題を解決するのに役立ちますが、すべての方法が若干異なります。

一般的な考え方としては、想定される **状態**を受け取る "マネージャー" があります。 この状態は、"web アプリの2つのインスタンスを実行し、ポート80を公開する必要がある" と考えられます。 マネージャーは、クラスター内のすべてのコンピューターを確認し、作業を "ワーカー" ノードに委任します。 マネージャーは、変更 (コンテナーの終了など) を監視し、 **実際の状態** を反映するために期待される状態を反映します。

## <a name="cloud-native-computing-foundation-projects"></a>クラウドネイティブコンピューティングファンデーションプロジェクト

CNCF は、Kubernetes、Prometheus、エンボイ、Linkerd、NAT などのさまざまなオープンソースプロジェクトに対して、ベンダー中立のホームです。 ここでは、 [段階的および incubated プロジェクト](https://www.cncf.io/projects/) と、 [cncf ランドスケープ](https://landscape.cncf.io/)全体を表示できます。 監視、ログ記録、セキュリティ、イメージレジストリ、メッセージングなどに関する問題の解決に役立つプロジェクトは多数あります。

そのため、コンテナーランドスケープとクラウドネイティブアプリケーションの開発に慣れていない場合は、始めましょう。 コミュニティに接続して質問し、学習を続けることができるようになりました。 お待ちしております。

## <a name="working-with-docker-in-vs-code"></a>VS Code での Docker の使用

VS Code Docker 拡張機能の使用方法の詳細については、次を参照してください。

- [VS Code Docker 拡張機能の概要](https://code.visualstudio.com/docs/containers/overview)
- [Node.jsを使ってみる ](https://code.visualstudio.com/docs/containers/quickstart-node)
- [Python を使い始める](https://code.visualstudio.com/docs/containers/quickstart-python)
- [.NET Core の概要](https://code.visualstudio.com/docs/containers/quickstart-aspnet-core)
- [コンテナー化されたアプリのデバッグ](https://code.visualstudio.com/docs/containers/debug-common)
