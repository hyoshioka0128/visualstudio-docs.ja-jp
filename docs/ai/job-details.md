---
title: 最近のジョブの表示
author: lisawong19
ms.author: liwong
manager: routlaw
ms.date: 11/13/2017
ms.topic: conceptual
ms.workload:
- multiple
ms.openlocfilehash: 79b396946666077dcdedb3ee2a5ab891c2bb4fb8
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "72777392"
---
# <a name="view-recent-job-performance-and-details"></a>最近のジョブのパフォーマンスと詳細を表示する

ジョブが送信されたら、ジョブの一覧を表示して、ジョブの状態やジョブの期間などを確認することができます。

1. **サーバー エクスプローラー**で、特定の計算コンテキストを展開します。
2. **[ジョブ]** をダブルクリックします。
3. その計算コンテキストに送信されたジョブの一覧が表示されます。
4. 一覧内で特定の**ジョブ**を選択して詳細を確認します。

![ジョブの監視](media/job-details/monitor-jobs.png)

> Linux VM に送信されたジョブ履歴は /tmp ディレクトリ内の VM に格納されます。 したがって、VM が再起動されるたびにジョブ履歴はクリアされます。 ジョブ履歴を永続的に記録する場合は、Azure Machine Learning 内の計算コンテキストとして VM を構成してから、ジョブを Azure Machine Learning に送信します (ご利用の VM を計算コンテキストとして選択)。
