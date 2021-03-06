---
title: スナップショット デバッガーの開始ページ
ms.date: 07/14/2018
robots: noindex, nofollow
ms.technology: vs-ide-debug
ms.topic: reference
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: c7b5b48aeeb0cfcaeed72a06bfb6709892c58de7
ms.sourcegitcommit: e2373d40ca9829cee63519152a97172763471e21
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/05/2018
ms.locfileid: "39310114"
---
# <a name="getting-started-with-the-snapshot-debugger"></a>スナップショット デバッガーの概要

Visual Studio Snapshot Debugger は、サービスに接続されているようになりましたし、デバッグに役立てるため、スナップショットの収集を開始することができます。

スナップショット デバッガーを使用するには、コードにいくつかのスナップ ポイントを設定、スナップショットの収集を開始するボタンをクリックし、シナリオを実行し、します。 ときに、コードの実行を設定すると、スナップ ポイントで、アプリケーションのスナップショットが作成されます。 次に Visual studio 診断ツール ウィンドウでクリックして、スナップショットを開きます。 ローカルだと同様、サービスからスナップショットをデバッグできます。 詳細な手順についてを読んでをしてください。

## <a name="collect-and-view-snapshots"></a>収集し、スナップショットの表示

スナップショット デバッガーは、アプリケーションからのスナップショットを収集します。 スナップショットは、時間の時点で、appication の画像のようです。 コードで、スナップ ポイントを設定してスナップショットを収集するタイミングと場所は、Visual Studio に指示します。 スナップ ポイントを調査している問題のスナップショットを取得するかどうかを確認する必要がある条件を設定します。

### <a name="set-a-snappoint"></a>設定、スナップ ポイント

1. コード エディターで、スナップ ポイントを設定する対象のコード行の横にある左側の余白をクリックします。 これはコードを実行することがわかっていることを確認します。 

    ![エディターで、スナップ ポイントの設定](../media/snapshot-startpage-set-snappoint.png)

    紫の六角形は、左側でクリックする場所が表示されます。

2. クリックして**コレクションの開始**スナップ ポイントを有効にします。

### <a name="open-a-snapshot"></a>スナップショットを開く

1. スナップ ポイントをヒットすると、右側の [診断ツール] ウィンドウで、スナップショットが表示されます。 ウィンドウが開かない場合を選択して開くことができます**デバッグ** > **Windows** > **診断ツールの表示**します。 

    ![[診断ツール] ウィンドウのスナップショット](../media/snapshot-startpage-diagsession-window.png)

2. 開くスナップショットをダブルクリックします。

### <a name="inspect-snapshot-data"></a>スナップショット データを検査します。

データヒントを表示、ローカル、ウォッチを使用して、呼び出しの変数をポイントすると、このビューから、windows のスタックし、も式を評価します。

Web サイト自体はまだ存在していると、エンドユーザーに影響はありません。 既定では、スナップ ポイントあたり 1 つだけスナップショットがキャプチャされます。 つまり、スナップショットがキャプチャされた後、スナップ ポイントはオフにします。 場合は、スナップ ポイントにある別のスナップショットをキャプチャするを再度有効にできます、スナップ ポイントをクリックして**コレクションの更新**します。

### <a name="set-a-logpoint"></a>ログポイントを設定します。

1. スナップ ポイント (紫色の六角形) アイコンを右クリックし、選択**設定**します。

2. **スナップ ポイント設定**ウィンドウで、**アクション**します。

    ![スナップ ポイント条件](../media/snapshot-startpage-logpoint.png)

3. **メッセージ**フィールドに、ログに記録するログ メッセージを入力します。 中かっこ内に配置することによってログ メッセージに変数を評価することもできます。

    選択した場合**出力ウィンドウに送る**、ログポイントがヒットしたときに、診断ツール ウィンドウで、メッセージが表示されます。 

    選択した場合**アプリケーション ログに送信**、メッセージの表示を任意の場所からのメッセージを確認できます`System.Diagnostics.Trace`(または`ILogger`で .NET Core)、ログポイントがヒットしたときに、App Insights など。

## <a name="learn-more"></a>詳細

スナップショット デバッガーの詳細についてのについて、 [docs ページ](../debug-live-azure-applications.md)します。 バグを発見しやすく条件を設定する方法について詳しく説明します。

## <a name="dont-show-me-this-again"></a>しない ' このメッセージを表示

決してスナップショット デバッガーの開始 ページを再び表示するスナップショット デバッガーを接続する場合、変更、**セッションの開始時に"Getting Started"のページを表示**オプション**ツール** >  **オプション** > **スナップショット デバッガー**します。 

![スナップショット デバッガー ツール オプション ページ](../media/snapshot-startpage-tools-options.png)
