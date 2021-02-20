---
title: '方法: ロード テスト結果でカスタム グラフを作成する'
description: ロード テストの実行中、または実行完了後に、ロード テストの結果に関する特定の情報を表示するグラフをデザインする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 10/19/2016
ms.topic: how-to
helpviewer_keywords:
- load test results graphs, creating
- load test results graphs
ms.assetid: 17fcafce-76f9-4411-9389-6e5376eab236
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.openlocfilehash: bcef8b73eaf4709e8e636d4719784606019bdcbf
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99937590"
---
# <a name="how-to-create-custom-graphs-in-load-test-results"></a>方法: ロード テスト結果でカスタム グラフを作成する

ロード テストの結果に関する特定の情報を表示するグラフをデザインできます。 カスタム グラフをデザインするには、グラフで表示するロード テストのカウンターを指定します。

以下の手順は、ロード テストの実行中でも、ロード テストの実行が終了した後でも、どちらでも実行できます。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="to-create-a-custom-load-test-results-graph"></a>カスタム ロード テスト結果グラフを作成するには

1. **ロード テスト** ツール バーで、 **[新しいグラフの追加]** を選択します。

     \- または

     **ロード テスト アナライザー** で、 **[カウンター]** パネルまたはグラフを右クリックし、 **[グラフの追加]** を選択します。

     **[グラフ名の入力]** ダイアログ ボックスが表示されます。

2. **[グラフ名]** にグラフの名前を入力し、**[OK]** を選択します。

     **ロード テスト アナライザー** に新しいグラフが表示されます。 グラフは、現在選択されているグラフ パネルに表示されます。そのパネルに表示されていたグラフが置き換えられます。

3. カウンターを追加して、新しいグラフをカスタマイズします。 詳細については、「[方法:ロード テスト結果のグラフにカウンターを追加および削除する](../test/how-to-add-and-delete-counters-on-graphs-in-load-test-results.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [グラフ ビューでのロード テスト結果の分析](../test/analyze-load-test-results-in-the-graphs-view.md)
- [方法: グラフにカウンターを追加および削除する](../test/how-to-add-and-delete-counters-on-graphs-in-load-test-results.md)
