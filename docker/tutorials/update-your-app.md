---
title: 'Docker チュートリアル-パート 2: アプリを更新する'
description: Docker アプリを更新する方法について説明します。
ms.date: 08/04/2020
author: nebuk89
ms.author: ghogen
manager: jillfra
ms.technology: vs-azure
ms.topic: conceptual
ms.workload:
- azure
ms.openlocfilehash: 4a1cba71481608803522336ad5c0f6b6354bca32
ms.sourcegitcommit: c4212f40df1a16baca1247cac2580ae699f97e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89176751"
---
# <a name="update-the-app"></a>アプリの更新

小さな機能の要求として、todo リスト項目がない場合に、製品チームから "空のテキスト" を変更するように求められました。 次のように移行します。

> Todo 項目がまだありません。 上に1を追加します。

とても単純ですね。 変更を加えてみましょう。

## <a name="update-the-source-code"></a>ソース コードを更新する

1. ファイルで `src/static/js/app.js` 、56行目を更新して、新しい空のテキストを使用します。

    ```diff
    -                <p className="text-center">No items yet! Add one above!</p>
    +                <p className="text-center">You have no todo items yet! Add one above!</p>
    ```

1. 前に使用したのと同じコマンドを使用して、更新されたバージョンのイメージをビルドします。

    ```bash
    docker build -t getting-started .
    ```

1. 更新されたコードを使用して、新しいコンテナーを開始します。

    ```bash
    docker run -dp 3000:3000 getting-started
    ```

**しかし、** 次のようなエラーが表示される可能性があります (Id は異なります)。

```bash
docker: Error response from daemon: driver failed programming external connectivity on endpoint laughing_burnell 
(bb242b2ca4d67eba76e79474fb36bb5125708ebdabd7f45c8eaf16caaabde9dd): Bind for 0.0.0.0:3000 failed: port is already allocated.
```

では、何が起こったのでしょうか。 古いコンテナーがまだ実行されているため、新しいコンテナーを開始できませんでした。 これが問題になるのは、コンテナーがホストのポート3000を使用していて、コンピューター (コンテナーに含まれる) で特定のポートをリッスンできるプロセスが1つだけであるためです。 この問題を解決するには、古いコンテナーを削除します。

## <a name="replace-the-old-container"></a>古いコンテナーを置き換える

コンテナーを削除するには、まず、コンテナーを停止する必要があります。 停止したら、削除できます。 古いコンテナーを削除する方法は2つあります。 最も使いやすいパスを自由に選択できます。

### <a name="remove-a-container-using-the-cli"></a>CLI を使用してコンテナーを削除する

1. コマンドを使用して、コンテナーの ID を取得し `docker ps` ます。

    ```bash
    docker ps
    ```

1. コンテナーを `docker stop` 停止するには、コマンドを使用します。

    ```bash
    # Swap out <the-container-id> with the ID from docker ps
    docker stop <the-container-id>
    ```

1. コンテナーが停止したら、コマンドを使用して削除でき `docker rm` ます。

    ```bash
    docker rm <the-container-id>
    ```

> [!TIP]
> コマンドに "force" フラグを追加することで、1つのコマンドでコンテナーを停止および削除でき `docker rm` ます。 例: `docker rm -f <the-container-id>`

### <a name="remove-a-container-using-the-docker-dashboard"></a>Docker ダッシュボードを使用してコンテナーを削除する

VS Code 拡張機能を開いた場合は、2回のクリックでコンテナーを削除することができます。 コンテナー ID を検索して削除するよりも、はるかに簡単です。

1. 拡張機能を開いた状態で、コンテナーに移動して右クリックします。

1. [ **削除** ] オプションをクリックします。

1. 削除が完了したことを確認してください。

![Docker ダッシュボード-コンテナーの削除](media/vs-removing-container.png)

### <a name="start-the-updated-app-container"></a>更新されたアプリコンテナーを開始する

1. 次に、更新されたアプリを開始します。

    ```bash
    docker run -dp 3000:3000 getting-started
    ```

1. ブラウザーを更新 [http://localhost:3000](http://localhost:3000) すると、更新されたヘルプテキストが表示されます。

![空のテキストが更新されたアプリケーションを更新しました](media/todo-list-updated-empty-text.png)

## <a name="recap"></a>まとめ

更新プログラムを作成できましたが、次の2つの点に注意する必要がありました。

- Todo リスト内の既存の項目はすべて失われています。 これは非常に優れたアプリではありません。 これについては、すぐに説明します。
- このような小さな変更には、 *多数* の手順が必要でした。 今後のセクションでは、変更を行うたびに新しいコンテナーを再構築して開始することなく、コードの更新を確認する方法について説明します。

永続化について学習する前に、これらのイメージを他のユーザーと共有する方法を簡単に説明します。

## <a name="next-steps"></a>次の手順

チュートリアルを続行します。

> [!div class="nextstepaction"]
> [アプリの共有](share-your-app.md)
