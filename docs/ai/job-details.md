---
title: 最近のジョブの表示
description: ジョブを送信した後に、ジョブの一覧を表示して、それらの状態や期間などを確認できることについて説明します。
ms.custom: SEO-VS-2020
author: jillre
ms.author: jillfra
manager: jmartens
monikerRange: vs-2017
ms.date: 11/13/2017
ms.topic: how-to
ms.workload:
- multiple
ms.openlocfilehash: 13d78913e0d5d708c5e75a80611ae9cc1c2f7366
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99841433"
---
# <a name="view-recent-job-performance-and-details"></a>最近のジョブのパフォーマンスと詳細を表示する

ジョブが送信されたら、ジョブの一覧を表示して、ジョブの状態やジョブの期間などを確認することができます。

1. **サーバー エクスプローラー** で、特定の計算コンテキストを展開します。
2. **[ジョブ]** をダブルクリックします。
3. その計算コンテキストに送信されたジョブの一覧が表示されます。
4. 一覧内で特定の **ジョブ** を選択して詳細を確認します。

![ジョブの監視](media/job-details/monitor-jobs.png)

> Linux VM に送信されたジョブ履歴は /tmp ディレクトリ内の VM に格納されます。 したがって、VM が再起動されるたびにジョブ履歴はクリアされます。 ジョブ履歴を永続的に記録する場合は、Azure Machine Learning 内の計算コンテキストとして VM を構成してから、ジョブを Azure Machine Learning に送信します (ご利用の VM を計算コンテキストとして選択)。
