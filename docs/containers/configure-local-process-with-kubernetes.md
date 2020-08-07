---
title: Local Process with Kubernetes 向けの追加の構成に KubernetesLocalProcessConfig.yaml を使用する
services: azure-dev-spaces
ms.date: 07/28/2020
ms.topic: conceptual
description: KubernetesLocalProcessConfig.yaml を使用した Local Process with Kubernetes の追加の構成オプションについて説明します
keywords: Local Process with Kubernetes, Azure Dev Spaces, Dev Spaces, Docker, Kubernetes, Azure, AKS, Azure Kubernetes Service, コンテナー
monikerRange: '>=vs-2019'
author: ghogen
ms.author: ghogen
manager: jillfra
ms.openlocfilehash: 234eacedbc08007ede6bb5745a1a289aa838cccb
ms.sourcegitcommit: e359b93c93c6ca316c0d8b86c2b6e566171fd1ea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/01/2020
ms.locfileid: "87508313"
---
# <a name="configure-local-process-with-kubernetes"></a>Local Process with Kubernetes を構成する

`KubernetesLocalProcessConfig.yaml` ファイルを使用すると、AKS クラスター内のポッドからアクセスできる環境変数とマウントされたファイルをレプリケートすることができます。 `KubernetesLocalProcessConfig.yaml` ファイルでは、次のアクションを指定できます。

* ボリュームをダウンロードし、そのボリュームへのパスを環境変数として設定する。
* クラスター上で実行されているサービスを、開発用コンピューター上で実行されているプロセスで使用できるようにします。
* 定数値を指定した環境変数を作成します。

既定の `KubernetesLocalProcessConfig.yaml` ファイルは自動的には作成されません。プロジェクトのルートに手動でファイルを作成する必要があります。

## <a name="download-a-volume"></a>ボリュームをダウンロードする

ダウンロードするボリュームごとに、*env* で *name* と *value* を指定します。 *name* は、開発用コンピューターで使用される環境変数です。 *value* は、開発用コンピューター上のボリュームの名前とパスです。 *value* の値は、 *$(volumeMounts:VOLUME_NAME)/PATH/TO/FILES* の形式を受け取ります。

次に例を示します。

```yaml
version: 0.1
env:
  - name: ALLOW_LIST_PATH
    value: $(volumeMounts:allow-list)/allow-list
```

上の例では、コンテナーから *allow-list* ボリュームをダウンロードし、その場所と環境変数 *ALLOW_LIST_PATH* へのパスを設定しています。 既定の動作では、開発用コンピューター上の一時ディレクトリ以下の指定したパスにファイルがダウンロードされます。 上の例では、*ALLOW_LIST_PATH* は `/TEMPORARY_DIR/allow-list` に設定されています。 

> [!NOTE]
> ボリュームをダウンロードすると、設定したパスに関係なく、そのボリュームの内容全体がダウンロードされます。 このパスは、開発用コンピューターで使用する環境変数を設定するためにのみ使用されます。 トークンの末尾に */allow-list* または */path/to/files* を追加しても、ボリュームが永続化される場所には実際には影響しません。 環境変数は、そのボリューム内の特定のファイルへの参照がアプリに必要な場合に便利です。

一時ディレクトリを使用するのではなく、開発用コンピューターにボリューム マウントをダウンロードする場所を指定することもできます。 特定の場所ごとに、*volumeMounts* で *name* と *localPath* を指定します。 *name* は照合するボリューム名であり、*localPath* は開発用コンピューターの絶対パスです。 次に例を示します。

```yaml
version: 0.1
volumeMounts:
  - name: default-token-*
    localPath: /var/run/secrets/kubernetes.io/serviceaccount
env:
  - name: KUBERNETES_IN_CLUSTER_CONFIG_OVERRIDE
    value: $(volumeMounts:default-token-*)
```

上記の例では、*env* のエントリを使用して、*default-token-1111* や *default-token-1234-5678-90abcdef* などの *default-token-\** と一致するボリュームをダウンロードします。 複数のボリュームが一致する場合は、最初に一致したボリュームが使用されます。 すべてのファイルは、*volumeMounts* のエントリを使用して、開発用コンピューターの `/var/run/secrets/kubernetes.io/serviceaccount` にダウンロードされます。 *KUBERNETES_IN_CLUSTER_CONFIG_OVERRIDE* 環境変数は `/var/run/secrets/kubernetes.io/serviceaccount` に設定されています。

## <a name="make-a-service-available"></a>サービスを使用できるようにする

開発用コンピューターで使用できるようにするサービスごとに、*env* で *name* と *value* を指定します。 *name* は、開発用コンピューターで使用される環境変数です。 *value* は、クラスターのサービスの名前とパスです。 *value* の値は、 *$(services:SERVICE_NAME)/PATH* の形式を受け取ります。

次に例を示します。

```yaml
version: 0.1
env:
  - name: MYAPP1_SERVICE_HOST
    value: $(services:myapp1)/api/v1/
```

上の例では、*myapp1* サービスを開発用コンピューターで使用できるようにしています。また、*MYAPP1_SERVICE_HOST* 環境変数を *myapp1* サービスのローカル IP アドレスと `/api/v1` パス (つまり、`127.1.1.4/api/v1`) に設定しています。 *myapp1* サービスには、環境変数 *myapp1*、または *myapp1.svc.cluster.local* を使用してアクセスできます。

> [!NOTE]
> 開発用コンピューターでサービスを使用できるようにすると、設定したパスに関係なく、サービス全体を使用できるようになります。 このパスは、開発用コンピューターで使用する環境変数を設定するためにのみ使用されます。
また、 *$(services:SERVICE_NAME.NAMESPACE_NAME)* を使用して、特定の Kubernetes 名前空間のサービスを使用できるようにすることもできます。 次に例を示します。

```yaml
version: 0.1
env:
  - name: MYAPP2_SERVICE_HOST
    value: $(services:myapp2.mynamespace)
```

上の例では、*mynamespace* 名前空間の *myapp2* を開発用コンピューターで使用できるようにしています。また、*MYAPP2_SERVICE_HOST* 環境変数を *mynamespace* 名前空間の *myapp2* のローカル IP アドレスに設定しています。

## <a name="create-an-environment-variable-with-a-constant-value"></a>定数値を指定した環境変数を作成する

開発用コンピューターに作成する環境変数ごとに、*env* で *name* と *value* を指定します。 *name* は開発用コンピューターで使用される環境変数であり、*value* は値です。 次に例を示します。

```yaml
version: 0.1
env:
  - name: DEBUG_MODE
    value: "true"
```

上の例では、値が *true* の *DEBUG_MODE* という名前の環境変数を作成しています。

## <a name="example-kuberneteslocalprocessconfigyaml"></a>KubernetesLocalProcessConfig.yaml の例

完全な `KubernetesLocalProcessConfig.yaml` ファイルの例を次に示します。

```yaml
version: 0.1
volumeMounts:
  - name: default-token-*
    localPath: /var/run/secrets/kubernetes.io/serviceaccount
env:
  - name: KUBERNETES_IN_CLUSTER_CONFIG_OVERRIDE
    value: $(volumeMounts:default-token-*)
  - name: ALLOW_LIST_PATH
    value: $(volumeMounts:allow-list)/allow-list
  - name: MYAPP1_SERVICE_HOST
    value: $(services:myapp1)/api/v1/
  - name: MYAPP2_SERVICE_HOST
    value: $(services:myapp2.mynamespace)
  - name: DEBUG_MODE 
    value: "true"
```

## <a name="next-steps"></a>次の手順

Local Process with Kubernetes を使用してローカル環境の開発用コンピューターをクラスターに接続する方法については、「[Visual Studio Code を使用して Local Process with Kubernetes を利用する][local-process-kubernetes-vs-code]」および「[Visual Studio を使用して Local Process with Kubernetes を利用する][local-process-kubernetes-vs]」を参照してください。

[local-process-kubernetes-vs-code]: https://code.visualstudio.com/docs/containers/local-process-kubernetes
[local-process-kubernetes-vs]: local-process-kubernetes.md
