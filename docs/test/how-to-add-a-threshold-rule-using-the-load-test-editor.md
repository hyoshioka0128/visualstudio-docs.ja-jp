---
title: ロード テスト用のしきい値規則を追加する
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- load tests, monitoring
- load tests, thresholds
- load tests, analyzing
- thresholds in load tests
ms.assetid: 3d8fac8f-426f-4155-9ced-f7cd4c79792c
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: d1389df0c307ad6ec65575fc7934e622928a0ca1
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75591633"
---
# <a name="how-to-add-a-threshold-rule-using-the-load-test-editor"></a>方法: ロード テスト エディターを使用してしきい値規則を追加する

ロード テストのしきい値規則は、パフォーマンス カウンターの値を定数値または別のパフォーマンス カウンターの値と比較します。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="to-add-a-threshold-rule"></a>しきい値規則を追加するには

1. ロード テストを開きます。

2. ロード テスト エディターで、 **[カウンター セット]** ノードを展開します。

3. [カウンター セット] のいずれかで、 **[カウンター カテゴリ]** のいずれかを展開します。 たとえば、 **[LoadTest:Scenario]** を選択します。 ノードを展開します。

4. カウンターのいずれか、たとえば **[LoadTest:Scenario]** の **[User Load]** を右クリックします。 **[しきい値規則の追加]** を選択します。

     **[しきい値規則の追加]** ダイアログ ボックスが表示されます。

5. 2 種類の規則、**定数の比較**と**カウンターの比較**のいずれかを選択できます。 適切な種類を選択し、値を設定します。

    > [!NOTE]
    > **[しきい値を超えたときに警告]** プロパティは、しきい値を上回ると問題であることを示す場合は **True** に、しきい値を下回ると問題であることを示す場合は **False** に設定します。

## <a name="see-also"></a>関連項目

- [しきい値規則違反](../test/analyze-threshold-rule-violations-in-load-tests.md)
- [ロード テストでのコンピューターのカウンター セットとしきい値規則の指定](../test/specify-counter-sets-and-threshold-rules-for-load-testing.md)
- [ロード テストの結果の分析](../test/analyze-load-test-results-using-the-load-test-analyzer.md)
