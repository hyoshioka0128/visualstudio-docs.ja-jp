---
title: '方法: ロード テスト結果をリポジトリから削除する'
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- results, load test
- load tests, deleting results
- load test results, removing
- Load Test Results Repository
- load tests, removing results
- load test results, deleting
ms.assetid: c2afe36b-d061-4f0e-9580-c18569ec08f9
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 26dc9750a2bf2eaf5d0ee5dd3d08485c458bb74a
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "75589059"
---
# <a name="how-to-delete-load-test-results-from-a-repository"></a>方法: ロード テスト結果をリポジトリから削除する

ロード テストを実行すると、実行中に収集された情報がロード テストの結果リポジトリに保存されます。 ロード テストの結果リポジトリには、パフォーマンス カウンター データとエラー情報が含まれています。 詳細については、「[ロード テストの結果リポジトリ内のロード テスト結果の管理](../test/manage-load-test-results-in-the-load-test-results-repository.md)」を参照してください。

ロード テストの結果をロード テスト エディターで管理するには、 **[ロード テストの結果を開いて管理]** ダイアログ ボックスを使用します。 このダイアログ ボックスでは、ロード テストの結果を表示、インポート、エクスポート、および削除できます。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="to-delete-results-from-a-repository"></a>結果をリポジトリから削除するには

1. Web パフォーマンスとロード テストのプロジェクトから、ロード テストを開きます。

2. 埋め込みツール バーの **[結果を開いて管理]** をクリックします。

     **[ロード テストの結果を開いて管理]** ダイアログ ボックスが表示されます。

3. **[ロード テストの結果を検索するコントローラー名を入力]** でコントローラーを選択します。 ローカル コンピューターに保存された結果にアクセスする場合は、 **[\<ローカル - コントローラーなし>]** を選択します。

4. **[次のロード テストの結果を表示]** で、結果を表示するロード テストを選択します。 すべてのテストの結果をすべて表示する場合は、 **[\<すべてのテストの結果を表示>]** を選択します。

     ロード テストの結果が使用可能な場合は、 **[ロード テストの結果]** 一覧に表示されます。 この一覧の列は、 **[時間]** 、 **[期間]** 、 **[ユーザー]** 、 **[成果]** 、 **[テスト]** 、 **[説明]** です。 **[テスト]** にはテストの名前が表示され、 **[説明]** にはテストを実行する前に入力した説明が表示されます。 **[説明]** 列には、テスト結果の **[分析コメント]** に入力された簡単な説明が表示されます。

5. **[ロード テストの結果]** ボックスの一覧で、いずれかの結果を選択します。 **Shift** キーまたは **Ctrl** キー、あるいはその両方を使用して、複数の結果を選択できます。

6. **[削除]** を選択します。

     結果がリポジトリから削除されます。

    > [!NOTE]
    > 結果が削除された後も **[ロード テストの結果を開いて管理]** ダイアログ ボックスは開いたままです。

## <a name="see-also"></a>参照

- [方法: ロード テスト結果をリポジトリからエクスポートする](../test/how-to-export-load-test-results-from-a-repository.md)
- [ロード テストの結果リポジトリ内のロード テスト結果の管理](../test/manage-load-test-results-in-the-load-test-results-repository.md)
- [ロード テストの結果の分析](../test/analyze-load-test-results-using-the-load-test-analyzer.md)
- [方法: ロード テスト結果をリポジトリにインポートする](../test/how-to-import-load-test-results-into-a-repository.md)
