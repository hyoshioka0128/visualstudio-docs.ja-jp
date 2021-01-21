---
title: ロード テストの結果の分析
description: ロード テスト アナライザーを使用して自動的に、またはコマンド ラインからテストに対して手動で、ロード テストの結果にアクセスして分析する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 10/19/2016
ms.topic: how-to
helpviewer_keywords:
- results, load test
- load test results, accessing
- Load Test Viewer
- load tests, accessing
- load tests, analyzing
- load tests, results
- Load Test Viewer, viewing
ms.assetid: b0a3e694-2894-479b-b270-7e61e9fafacd
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 95108a5901a00582e708f6bf3660cb07d2126e0a
ms.sourcegitcommit: 02f14db142dce68d084dcb0a19ca41a16f5bccff
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2020
ms.locfileid: "95442600"
---
# <a name="how-to-access-load-test-results-for-analysis"></a>方法: ロード テストの結果にアクセスして分析する

ロード テスト エディターからロード テストを実行すると、ロード テストの結果が自動的に開き、実行中のロード テストが **ロード テスト アナライザー** に表示されます。 コマンド ラインからロード テストを実行するとき、ロード テストの結果に手動でアクセスする必要があります。

完了したロード テストの結果には、テスト対象コンピューターから定期的に収集されたパフォーマンス カウンター サンプルとエラー情報が含まれています。 パフォーマンス カウンター サンプルの多くは、ロード テストの実行中に収集されます。 収集されるパフォーマンス データの量は、テストの実行の長さ、サンプリング間隔、テスト対象コンピューターの数、収集されるカウンターの数、構成されているデータ コレクター、およびログ レベルによって異なります。 大規模なロード テストでは、収集されるパフォーマンス データ量が数ギガバイトになることも珍しくありません。 詳細については、「[テスト コントローラーとテスト エージェント](configure-test-agents-and-controllers-for-load-tests.md)」を参照してください。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="to-access-a-load-test-result"></a>ロード テストの結果にアクセスするには

1. Web パフォーマンスとロード テストのプロジェクトから、ロード テストを開きます。

2. ロード テスト エディターのツール バーの **[結果を開いて管理]** を選択します。

     **[結果を開いて管理]** ダイアログ ボックスが表示されます。

3. **[ロード テストの結果を検索するコントローラー名を入力]** でコントローラーを選択します。 ローカル コンピューターに保存された結果にアクセスする場合は、 **[\<local> - コントローラーなし]** を選択します。

4. **[次のロード テストの結果を表示]** で、結果を表示するロード テストを選択します。 すべてのテストの結果をすべて表示する場合は、 **[\<Show results for all tests>]** を選択します。

     ロード テストの結果が使用可能な場合は、 **[ロード テストの結果]** 一覧に表示されます。 この一覧の列は、 **[時間]** 、 **[期間]** 、 **[ユーザー]** 、 **[成果]** 、 **[テスト]** 、 **[説明]** です。 **[テスト]** にはテストの名前が表示され、 **[説明]** にはテストを実行する前に入力した説明が表示されます。

    > [!NOTE]
    > 結果が表示されます。一覧の先頭には最近の結果が表示されます。

5. **[ロード テストの結果]** ボックスの一覧で、分析するロード テストの結果を選択して **[開く]** をクリックします。

6. **ロード テスト アナライザー** が表示されます。 選択したロード テストの結果が概要ビューに表示されます。 詳細については、「[ロード テスト結果の概要](../test/load-test-results-summary-overview.md)」を参照してください。

     **[結果を開いて管理]** ダイアログ ボックスでは、ロード テストの結果の表示、インポート、エクスポート、削除など、ロード テストの結果のその他の要素を管理できます。 詳細については、「[ロード テストの結果リポジトリ内のロード テストの結果の管理](../test/manage-load-test-results-in-the-load-test-results-repository.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [ロード テストの結果の分析](../test/analyze-load-test-results-using-the-load-test-analyzer.md)
