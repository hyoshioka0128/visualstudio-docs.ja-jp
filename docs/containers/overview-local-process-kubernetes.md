---
title: Local Process with Kubernetes のしくみ
ms.technology: vs-azure
ms.date: 06/02/2020
ms.topic: conceptual
description: Local Process with Kubernetes を使用して開発用コンピューターを Kubernetes クラスターに接続するプロセスについて説明します
keywords: Local Process with Kubernetes, Docker, Kubernetes, Azure, コンテナー
monikerRange: '>=vs-2019'
ms.openlocfilehash: adde9d8ecab93bdb6f0aebbd74730ef60bd80cf6
ms.sourcegitcommit: 510a928153470e2f96ef28b808f1d038506cce0c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/17/2020
ms.locfileid: "86454375"
---
# <a name="how-local-process-with-kubernetes-works"></a>Local Process with Kubernetes のしくみ

Local Process with Kubernetes を使用すると、開発用のコンピューター上でコードの実行とデバッグを行いながら、残りのアプリケーションやサービスが置かれている Kubernetes クラスターとの接続を保つことができます。 たとえば、多数のサービスやデータベースが相互に依存している大規模なマイクロサービス アーキテクチャがある場合、開発用コンピューター上のそれらの依存関係をレプリケートするのは困難な場合があります。 さらに、内部ループの開発中にコードを変更するたびにコードをビルドして Kubernetes クラスターにデプロイすると、遅くなり、時間がかかり、デバッガーで使用するのが難しくなることがあります。

Local Process with Kubernetes を使用すると、代わりに開発用コンピューターとクラスターの間に直接接続が作成されることにより、コードをビルドしてクラスターにデプロイする必要がなくなります。 デバッグ中に開発用コンピューターをクラスターに接続すると、Docker または Kubernetes の構成を作成することなく、完全なアプリケーションのコンテキストで、サービスを迅速にテストおよび開発できます。

Local Process with Kubernetes では、接続された Kubernetes クラスターと開発用コンピューターの間でトラフィックがリダイレクトされます。 このトラフィックのリダイレクトにより、開発用コンピューター上のコードと、Kubernetes クラスターで実行されているサービスは、同じ Kubernetes クラスター内に存在するかのように通信できます。 Local Process with Kubernetes には、開発用コンピューターの Kubernetes クラスター内のポッドに利用できる環境変数とマウントされたボリュームをレプリケートする方法も用意されています。 開発用コンピューター上の環境変数およびマウントされたボリュームにアクセスできると、それらの依存関係を手動でレプリケートすることなく、コードの作業をすばやく行うことができます。

## <a name="using-local-process-with-kubernetes"></a>Local Process with Kubernetes の使用

Visual Studio で Local Process with Kubernetes を使用するには、*ASP.NET と Web 開発*ワークロードと [Local Process Kubernetes 拡張機能][lpk-extension]がインストールされている Windows 10 で実行されている [Visual Studio 2019][visual-studio] バージョン 16.7 Preview 4 以降が必要です。 Local Process with Kubernetes を使用して Kubernetes クラスターへの接続を確立するときに、クラスター内の既存のポッドとの間でやり取りされるすべてのトラフィックを開発用コンピューターにリダイレクトするかどうかを選択できます。

> [!NOTE]
> Local Process with Kubernetes を使用するときは、開発用コンピューターにリダイレクトするサービスの名前の指定を求められます。 このオプションを利用して、リダイレクト用のポッドを簡単に見分けることができます。 Kubernetes クラスターと開発用コンピューターの間のすべてのリダイレクトは、ポッドを対象としています。

クラスターへの接続が確立された Local Process with Kubernetes では、次のことが行われます。

* ユーザーは、クラスター上で置き換えるサービス、コードに使用する開発用コンピューター上のポート、1 回限りのアクションとしてのコードに対する起動タスクを構成するよう求められます。
* クラスター上のポッド内のコンテナーが、開発用コンピューターにトラフィックをリダイレクトするリモート エージェント コンテナーに置き換えられます。
* 開発用コンピューターからのトラフィックを、クラスター内で実行されるリモート エージェントに転送するために、開発用コンピューター上で [kubectl port-forward][kubectl-port-forward] を実行します。
* リモート エージェントを使用してクラスターから環境情報を収集します。 この環境情報には、環境変数、表示可能なサービス、ボリューム マウント、シークレット マウントが含まれます。
* 開発用コンピューター上のサービスが、クラスター上で実行されているかのように同じ変数にアクセスできるよう、Visual Studio の環境が設定されます。  
* クラスター上のサービスが開発用コンピューター上のローカル IP アドレスにマップされるように、hosts ファイルが更新されます。 開発用コンピューター上で実行されているコードは、これらの hosts ファイルのエントリを通じて、クラスター内で実行されている別のサービスに要求を送信できるようになります。 Local Process with Kubernetes がクラスターに接続するときに、hosts ファイルを更新できるよう、開発用コンピューター上の管理者アクセス権が求められます。
* 開発用コンピューター上でコードの実行とデバッグが開始されます。 必要な場合は、開発用コンピューターで必要なポートを現在使用しているサービスまたはプロセスが停止されて、ポートが解放されます。

クラスターへの接続が確立された後、ユーザーは、コンテナー化を使用せずに、コンピューター上でネイティブにコードを実行してデバッグすることができ、コードではクラスターの残りの部分と直接対話できます。 リモート エージェントが受信するネットワーク トラフィックは、ネイティブに実行されているコードがそのトラフィックを受け入れて処理できるよう、接続時に指定されたローカル ポートにリダイレクトされます。 ご利用のクラスターにある環境変数、ボリューム、シークレットは、開発用コンピューター上で実行されているコードから利用できるようになります。 また、Local Process with Kubernetes によって開発用コンピューターに追加された hosts ファイルのエントリとポート転送により、コードでは、クラスター側のサービス名を使用して、クラスター上で実行されているサービスにネットワーク トラフィックを送信することができます。そのトラフィックは、クラスターで実行されているサービスに転送されます。 接続されている間は常に、開発用コンピューターとクラスターの間でトラフィックがルーティングされます。

## <a name="diagnostics-and-logging"></a>診断とログ記録

Local Process with Kubernetes を使用してクラスターに接続しているときは、クラスターからの診断ログが、開発用コンピューターの[一時ディレクトリ][azds-tmp-dir]に記録されます。

## <a name="limitations"></a>制限事項

Local Process with Kubernetes には次の制限があります。

* Local Process with Kubernetes では、1 つのサービスのトラフィックが開発コンピューターにリダイレクトされます。 Local Process with Kubernetes を使用し、複数のサービスを同時にリダイレクトすることはできません。
* あるサービスに接続するには、そのサービスを 1 つのポッドでサポートする必要があります。 レプリカが含まれるサービスなど、1 つのサービスに複数のポッドで接続することはできません。
* Local Process with Kubernetes を正常に接続するために、1 つのポッドには、そのポッドで実行されているコンテナーが 1 つだけ与えられます。 Local Process with Kubernetes では、サービス メッシュによって挿入されたサイドカー コンテナーなど、追加のコンテナーが与えられたポッドを利用してサービスに接続できません。
* ホスト ファイルを編集する目的で開発コンピューターで実行するには、管理者特権が Local Process with Kubernetes に必要になります。

## <a name="next-steps"></a>次のステップ

Local Process with Kubernetes を使用してローカル環境の開発用コンピューターをクラスターに接続する方法については、[Local Process with Kubernetes の使用](local-process-kubernetes.md)に関するページを参照してください。

[azds-cli]: /azure/dev-spaces/how-to/install-dev-spaces#install-the-client-side-tools
[azds-tmp-dir]: /azure/dev-spaces/troubleshooting#before-you-begin
[azure-cli]: /cli/azure/install-azure-cli?view=azure-cli-latest
[local-process-kubernetes-vs]: local-process-kubernetes.md
[kubectl-port-forward]: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#port-forward
[visual-studio]: https://visualstudio.microsoft.com/downloads/
[lpk-extension]: https://marketplace.visualstudio.com/items?itemName=ms-azuretools.mindaro