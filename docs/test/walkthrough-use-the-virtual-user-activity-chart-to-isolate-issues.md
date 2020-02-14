---
title: ロード テストに仮想ユーザー アクティビティ チャートを使用する
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- load tests, virtual user activity chart
- virtual user activity chart, isolating performance issues
ms.assetid: d1c10fb9-cfeb-4e7f-9991-2d1e1103699e
author: jillre
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: a437da5d95b758b908f1f1d4f7b76c50b6488a3c
ms.sourcegitcommit: 00ba14d9c20224319a5e93dfc1e0d48d643a5fcd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2020
ms.locfileid: "77091848"
---
# <a name="walkthrough-using-the-virtual-user-activity-chart-to-isolate-issues"></a>チュートリアル: 仮想ユーザー アクティビティ チャートを使用した問題の特定

このチュートリアルでは、仮想ユーザー アクティビティ チャートを使用して、ロード テストを実行した個々の仮想ユーザーで発生したエラーを特定する方法について説明します。

仮想ユーザー アクティビティ チャートを使用すると、ロード テストに関連付けられた仮想ユーザー アクティビティを視覚化できます。 チャートの各行は、個別の仮想ユーザーを表します。 仮想ユーザー アクティビティ チャートには、各仮想ユーザーがテスト中に実行した処理が詳しく表示されます。 これにより、ユーザー アクティビティのパターンを確認することによってパフォーマンスの問題を特定できるほか、パターンの読み込み、失敗したテストまたは実行速度の遅いテストの関連付け、他の仮想ユーザー アクティビティによる要求の表示を実行できます。 仮想ユーザー アクティビティ チャートは、ロード テストの実行が完了した後にのみ使用できます。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="prerequisites"></a>必須コンポーネント

- Visual Studio Enterprise

- これらの手順を完了します。

  - [Web パフォーマンス テストの記録と実行](/azure/devops/test/load-test/run-performance-tests-app-before-release#recordtests)

  - [ロード テストの作成および実行](/azure/devops/test/load-test/run-performance-tests-app-before-release#create-a-load-test)

## <a name="open-the-colorwebapp-solution-created-in-the-previous-walkthroughs"></a>前のチュートリアルで作成した ColorWebApp ソリューションを開く

1. Visual Studio を開きます。

2. *LoadTest1.loadtest* を含む **ColorWebApp** ソリューションを開きます。 これは、このトピックの最初の必要条件セクションにリストされている 3 つのチュートリアルの手順を実行して作成したロード テストです。

     このチュートリアルの残りの手順は、ColorWebApp という名前の Web アプリケーション、*ColorWebAppTest.webtest* という名前の Web パフォーマンス テスト、および *LoadTest1.loadtest* という名前のロード テストを前提としています。

## <a name="run-the-load-test"></a>ロード テストを実行する

ロード テストを実行して仮想ユーザー アクティビティ データを収集します。

- **ロード テスト エディター**で、ツール バーの **[実行]** を選択します。 LoadTest1 の実行が開始されます。

## <a name="isolate-issues-in-the-virtual-user-activity-chart"></a>仮想ユーザー アクティビティ チャートでの問題の特定

ロード テストを実行して仮想ユーザー アクティビティ データを収集した後、**仮想ユーザー アクティビティ チャート**で**ロード テスト アナライザー**の詳細ビューを使用して、ロード テスト結果のデータを確認できます。 さらに、**仮想ユーザー アクティビティ チャート**を使用して、ロード テストにおけるパフォーマンスの問題を特定できます。

### <a name="to-use-the-virtual-user-activity-chart-in-your-load-test-results"></a>ロード テスト結果で仮想ユーザー アクティビティ チャートを使用するには

1. ロード テストの実行が完了した後、ロード テスト結果の**概要**ページが**ロード テスト アナライザー**に表示されます。 ツール バーの **[グラフ]** を選択します。

     グラフ ビューが表示されます。

2. **[ページ応答時間]** グラフのいずれかのしきい値違反アイコンに近い場所で右クリックし、 **[ユーザーの詳細に移動]** を選択します。

    > [!NOTE]
    > ユーザー アクティビティ チャートは、**ロード テスト エディター**のツール バーの **[詳細]** ボタンを使用して開くこともできます。 ただし、 **[ユーザーの詳細に移動]** オプションを使用した場合、**仮想ユーザー アクティビティ チャート**は、グラフ内で右クリックしたテストの部分に自動的にズームします。

     しきい値違反が発生したときの期間にフォーカスが置かれた**仮想ユーザー アクティビティ チャート**と共に、詳細ビューが表示されます。

     y 軸上の水平プロットは、個々の仮想ユーザーを示します。 x 軸は、ロード テストの実行のタイム ラインを示します。

3. **仮想ユーザー アクティビティ チャート**の下にある **[期間にズーム]** ツールで、左右のスライダーを調整してしきい値違反アイコンに近づけます。 この操作を行うと、**仮想ユーザー アクティビティ チャート**のタイム スケールが変更されます。

4. **[詳細の凡例]** で、 **[(エラーの強調表示)]** のチェック ボックスをオンにします。 しきい値違反が発生した仮想ユーザーが強調表示されます。

5. **[フィルター結果]** パネルで、 **[成功した結果の表示]** チェック ボックスと **[HTTP エラー]** チェック ボックスをオフにし、 **[検証規則エラー]** チェック ボックスはオンのままにします。

     **仮想ユーザー アクティビティ チャート**に、前のチュートリアルで構成したしきい値違反に指定された 3 秒を超える時間を *Red.aspx* ページで費やした仮想ユーザーのみが表示されます。

6. しきい値違反の検証規則エラーが発生した仮想ユーザーを示す水平線の上にマウス ポインターを置きます。

7. ツール ヒントに次の情報が表示されます。

    - **ユーザー ID**

    - **シナリオ**

    - **テスト**

    - **Outcome**

    - **Network**

    - **開始時刻**

    - **期間**

    - **エージェント**

    - **テスト ログ**

8. **テスト ログ**はリンクになっています。 **[テスト ログ]** リンクを選択します。

9. **Web パフォーマンス テスト結果ビューアー**に、ログと関連付けられた ColorWebTest Web パフォーマンス テストが表示されます。 これにより、しきい値違反がどこで発生したかを特定できます。

     さまざまな設定を **[詳細の凡例]** パネルと **[フィルター結果]** パネルの両方で使用して、ロード テストにおけるパフォーマンスの問題やエラーを特定できます。 これらの設定および **[期間にズーム]** ツールを使用して、**仮想ユーザー アクティビティ チャート**で仮想ユーザー データがどのように表示されるかを確認してください。

## <a name="see-also"></a>関連項目

- [詳細ビューでの仮想ユーザー アクティビティの分析](../test/analyze-load-test-virtual-user-activity-in-the-details-view.md)
- [テスト コントローラーとテスト エージェント](configure-test-agents-and-controllers-for-load-tests.md)
- [方法: 配布されたロード テストのテスト設定を作成する](../test/how-to-create-a-test-setting-for-a-distributed-load-test.md)
- [テスト エージェントをインストールして構成する](../test/lab-management/install-configure-test-agents.md)
- [テスト設定を使用して診断情報を収集する](../test/collect-diagnostic-information-using-test-settings.md)
