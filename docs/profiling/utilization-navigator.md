---
title: 使用状況ナビゲーター | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.cv.performance.utilizationnavigator
ms.assetid: 522a981a-37ef-4cdd-a04c-f1e7525a2aab
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 94e2562e86af36d935679916c2bfb9669be1758d
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "62823487"
---
# <a name="utilization-navigator"></a>使用状況ナビゲーター
コンカレンシー ビジュアライザーの使用状況ナビゲーターを使用して、トレースでの時間間隔を選択できます。 コンカレンシー ビジュアライザーは、一定期間内におけるターゲット プロセスによる CPU コアの使用率を表示します。 これにより、CPU 使用率パターンの調査が容易になり、使用状況データとその他のビュー内のデータを比較することもできます。 使用状況ナビゲーターは、コンカレンシー ビジュアライザーのすべてのビューの上部に表示されます。 次の図は、使用状況ナビゲーターを示しています。

 ![選択された期間を示す使用状況ナビゲーター](../profiling/media/cvutilizationnavigator.png "CVUtilizationNavigator") 使用状況ナビゲーターおよび選択された期間

 この図では、選択された期間は *Thumb* と呼ばれる赤い長方形で示されています。

 使用状況ナビゲーターを使用して、表示された時間範囲を操作する方法を次に示します。

- 左側または右側に Thumb をドラッグしてパンできます。 (キーボード:Thumb に焦点を合わせて、左矢印キーまたは右矢印キーを押します。)

- 間隔の範囲を変更するには、ハンドルのいずれかをドラッグします。 (キーボード:ハンドルに焦点を合わせて、右矢印キーまたは左矢印キーを押します。)

  別のコンカレンシー ビジュアライザー ズーム コントロールを使用して間隔を変更すると、変更を反映するために使用状況ナビゲーターが更新されます。