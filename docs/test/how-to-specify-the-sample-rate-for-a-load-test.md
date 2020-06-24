---
title: '方法: ロード テストの実行設定のサンプル速度を指定する'
ms.date: 10/19/2016
ms.topic: how-to
helpviewer_keywords:
- load tests, run settings
ms.assetid: 51cbe7d6-5dfd-4842-bca3-f7f8a665dc84
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: ab77354226028397d5875137ed331860a4b32925
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85287390"
---
# <a name="how-to-specify-the-sample-rate-for-a-load-test-run-setting"></a>方法: ロード テストの実行設定のサンプル速度を指定する

**新しいロード テスト ウィザード**でロード テストを作成した後で、**ロード テスト エディター**を使用して、プロパティをテストのニーズおよび目標に合わせて変更できます。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

**[プロパティ]** ウィンドウの実行設定の **[サンプル速度]** プロパティ値を編集するには、**ロード テスト エディター**を使用します。 実行設定の各プロパティとその説明の一覧については、「[ロード テストの実行設定のプロパティ](../test/load-test-run-settings-properties.md)」を参照してください。

ロード テストの長さに基づいて、ロード テストの実行設定の **[サンプル速度]** プロパティに適切な値を選択します。 既定値 (5 秒) のようにサンプル速度が小さいと、ロード テスト結果のデータベースに必要な容量が増えます。 長いロード テストでは、サンプル速度を増加すると、収集するデータ量を減らすことができます。 詳細については、「[方法: ロード テストの実行設定のサンプル速度を指定する](../test/how-to-specify-the-sample-rate-for-a-load-test.md)」を参照してください。

以下は、サンプル速度のガイドラインです。

|ロード テストの継続時間|推奨サンプル速度|
|-|-----------------------------|
|\< 1 時間|5 秒|
|1 ～ 8 時間|15 秒|
|8 ～ 24 時間|30 秒|
|> 24 時間|60 秒|

## <a name="to-specify-performance-counter-sampling-rate-in-a-run-setting"></a>実行設定のパフォーマンス カウンターのサンプル速度を指定するには

1. ロード テストを開きます。

     **ロード テスト エディター**が表示されます。 ロード テスト ツリーが表示されます。

2. ロード テスト ツリーの **[実行設定]** フォルダーで、サンプル速度を指定する実行設定を選択します。

3. **[表示]** メニューの **[プロパティ ウィンドウ]** をクリックします。

     **[プロパティ]** ウィンドウに、ロードの実行設定のカテゴリおよびプロパティが表示されます。

4. **[サンプル速度]** プロパティに、ロード テストによってパフォーマンス カウンターのデータが収集される頻度を示す時間の値を入力します。

5. プロパティを変更したら、 **[ファイル]** メニューの **[保存]** を選択します。 次に、新しい **[サンプル速度]** の値を使用して、ロード テストを実行します。

## <a name="see-also"></a>参照

- [ロード テストの実行設定の構成](../test/configure-load-test-run-settings.md)
- [ロード テスト シナリオのプロパティ](../test/load-test-scenario-properties.md)
