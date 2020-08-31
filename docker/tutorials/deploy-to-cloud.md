---
title: 'Docker チュートリアル-パート 9: クラウドへのデプロイ'
description: ホスティング用のクラウドサービスに docker アプリをデプロイします。
ms.date: 08/04/2020
author: nebuk89
ms.author: ghogen
manager: jillfra
ms.technology: vs-azure
ms.topic: conceptual
ms.workload:
- azure
ms.openlocfilehash: 661f9f6833b5ac5d42aacde7f228b042bef00bb0
ms.sourcegitcommit: c4212f40df1a16baca1247cac2580ae699f97e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89176767"
---
# <a name="deploy-to-the-cloud"></a>クラウドにデプロイする

アプリをローカルで実行したので、他のユーザーがアクセスして使用できるように、クラウドでの実行について考えることができます。 これを行うには、Docker コンテキストを使用します。 コンテキストとは、現在コンテナーを操作している場所です。 現時点では、"既定の" コンテキストがあるだけなので、クラウド one を追加し、アプリをデプロイする必要があります。

## <a name="create-your-cloud-context"></a>クラウドコンテキストを作成する

1. 開始するには、Docker パネルのコンテキストセクションを参照して、どのようなコンテキストを表示するかを確認します。

   ![既定のコンテキストのみを表示します](media/defaultcontext.png)

ローカル作業の既定のコンテキストのみが表示できます。

1. クラウドにデプロイするには、新しい ACI コンテキストを作成する必要がありますが、そのためには、まず azure アカウント拡張機能を Azure で認証する必要があります。

   ![Azure 拡張機能を追加しています](media/addazureextension.png)

まだ Azure アカウントを持っていない場合は、設定する必要があります。

1. これで、新しい ACI コンテキストを作成できるようになりました。 これを行うには、Docker ビューの **コンテキスト** セクションでプラスボタンをクリックします。

   ![ACI コンテキストの作成](media/createnewcontext.png)

これにより、これらのコンテナーを実行するリソースグループが表示されます。 方向キーを使用して既存のグループを選択するか、既定のオプションを使用して新しいグループを使用します。

![リソースグループの選択](media/selectresourcegroup.png)

これで、ACI のコンテキストが表示されるようになりました。これを右クリックして、現在のフォーカスまたは使用状況のコンテキストにすることができます。

![新しい ACI コンテキストを選択できます](media/listofcontexts.png)

## <a name="run-containers-in-the-cloud"></a>クラウドでコンテナーを実行する

1. ここで、ACI コンテキストを使用し、コンテナーを実行します。

   ```bash
   docker context use myacicontext
   docker run  -dp 3000:3000 <username>/getting-started
   ```

1. これを実行すると、コンテキスト内のコンテナーが表示されるようになります。

   ![ACI コンテキストで実行されているコンテナー](media/contextcontainer.png)

1. すべて正常に動作していることを確認するには、実行中のコンテナーを右クリックし、[ **ブラウザーで表示**] を選択します。

   ![パブリック IP を使用した ACI 内のコンテナー](media/containerinaci.png)

また、コンテナーがパブリック IP で実行され、正常に動作していることがわかります。

1. これで、実行中のコンテナーを見て、どのように動作しているかを確認できます。 まず、コンテナーのログを確認します。
 
 ```bash
   docker logs distracted-jackson
   ```

1. ローカルコンテナーの場合と同じように、コンテナーに対してを実行することもできます。
 
 ```bash
   docker exec -it distracted-jackson sh
   ```

1. 最後に、作業領域をクリーンアップし、テストコンテナーの実行を続行するために課金されないようにするには、実行中のコンテナーを右クリックし、[ **削除**] を選択します。

## <a name="recap"></a>まとめ

これで、ワークロードを取得し、初めてクラウドにデプロイしました。 これは、を使用して ACI コンテキスト内から、またはを使用して `docker run` 複数コンテナーアプリケーションを実行することで、コマンドラインからも実行でき `docker compose up` ます。 クラウドでのコンテナーの実行の詳細については、 [ACI の使用に](https://docs.docker.com/engine/context/aci-integration/)関する拡張ドキュメントを参照してください。

## <a name="next-steps"></a>次の手順

チュートリアルを続行します。

> [!div class="nextstepaction"]
> [次の内容](whats-next.md)
