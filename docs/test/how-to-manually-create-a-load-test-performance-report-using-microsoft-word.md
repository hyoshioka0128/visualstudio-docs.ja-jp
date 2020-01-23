---
title: Microsoft Word を使用してロード テスト パフォーマンス レポートを作成する
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- load tests, reporting
- load tests, creating Word reports
ms.assetid: 3b864c75-2699-48c1-a2b4-9651f108c267
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: c3deee8d35f06e50dbe22001e8a2fa81b41563e0
ms.sourcegitcommit: f3f668ecaf11b4c2738ebc91923c6b5e38e74670
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/16/2020
ms.locfileid: "76113441"
---
# <a name="how-to-manually-create-a-load-test-performance-report-using-microsoft-word"></a>方法: Microsoft Word を使用してロード テスト パフォーマンス レポートを手動で作成する

ロード テスト結果の概要ビューとグラフ ビューのデータをコピーして貼り付けることにより、Microsoft Word ロード テスト レポートを手動で作成できます。 概要ビューとグラフ ビューに表示されるデータは、コピーするときに HTML 形式で適用されます。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

> [!TIP]
> テーブル ビューのプレーン テキストや詳細ビューのスクリーンショットは Microsoft Word にコピーできますが、HTML 形式で適用されないので、さらに書式設定や編集が必要となります。

> [!TIP]
> また、編成された Microsoft Excel レポートを自動的に生成することもできます。 詳細については、[Microsoft Excel を使用してロード テスト パフォーマンス レポートを作成する](../test/how-to-create-load-test-performance-reports-using-microsoft-excel.md)。

## <a name="copy-summary-view-data"></a>概要ビューのデータのコピー

1. **ロード テスト結果**で、概要ビューが現在表示されていない場合に、ツール バーの **[概要]** をクリックします。

2. 概要ビューで右クリックし、 **[すべて選択]** を選択します。

3. 概要ビューで右クリックし、 **[コピー]** を選択します。 これにより、概要ビュー データは HTML 形式でクリップボードに表示されます。

4. Microsoft Word で、概要ビュー データを目的の場所に貼り付けます。

5. これで、レポートのニーズに応じて、コピーした内容の要素の変更、書式設定、および削除を行うことができます。

## <a name="copy-graph-view-data"></a>グラフ ビューのデータのコピー

1. **ロード テスト結果**で、グラフ ビューが現在表示されていない場合に、ツールバーの **[グラフ]** を選択します。

2. (省略可能) 次の図に示すように、Microsoft Word ドキュメントにコピーする特定のグラフを拡大します。 詳細については、[グラフの領域にズーム インする](../test/how-to-zoom-in-on-a-region-of-the-graph-in-load-test-results.md)」を参照してください。

     ![グラフ ビューのズーム コントロール](../test/media/ltest_zoomcontrol.png)

3. Microsoft Word 文書にコピーするグラフで右クリックし、 **[コピー]** を選択します。

4. Microsoft Word で、グラフおよび関連したテーブル データを目的の場所に貼り付けます。

    > [!WARNING]
    > リモート デスクトップのグラフをコピーして別のコンピューターに貼り付けることはできません。これは、グラフに関連付けられたテーブル情報のみがコピーされ、グラフの画像はコピーされないためです。 グラフの画像は、コピー元のコンピューターの一時ディレクトリに保存されます。2 つ目のコンピューターはそのディレクトリを逆参照できません。

## <a name="see-also"></a>関連項目

- [テストの比較または傾向分析のためにロード テストの結果レポートを作成する](../test/compare-load-test-results.md)
- [方法: Microsoft Excel を使用してロード テスト パフォーマンス レポートを作成する](../test/how-to-create-load-test-performance-reports-using-microsoft-excel.md)
