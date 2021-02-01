---
title: 使用状況ナビゲーター | Microsoft Docs
description: コンカレンシー ビジュアライザーの使用状況ナビゲーターを使用して、トレースでの時間間隔を選択する方法について学習します。
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
ms.openlocfilehash: 9f209098200333e91f0e5baf9c7a2b73b4a3202f
ms.sourcegitcommit: 18729d7c99c999865cc2defb17d3d956eb3fe35c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2021
ms.locfileid: "98723219"
---
# <a name="utilization-navigator"></a>使用状況ナビゲーター
コンカレンシー ビジュアライザーの使用状況ナビゲーターを使用して、トレースでの時間間隔を選択できます。 コンカレンシー ビジュアライザーは、一定期間内におけるターゲット プロセスによる CPU コアの使用率を表示します。 これにより、CPU 使用率パターンの調査が容易になり、使用状況データとその他のビュー内のデータを比較することもできます。 使用状況ナビゲーターは、コンカレンシー ビジュアライザーのすべてのビューの上部に表示されます。 次の図は、使用状況ナビゲーターを示しています。

 ![選択された期間を示す使用状況ナビゲーター](../profiling/media/cvutilizationnavigator.png "CVUtilizationNavigator") 使用状況ナビゲーターおよび選択された期間

 この図では、選択された期間は *Thumb* と呼ばれる赤い長方形で示されています。

 使用状況ナビゲーターを使用して、表示された時間範囲を操作する方法を次に示します。

- 左側または右側に Thumb をドラッグしてパンできます。 (キーボード: Thumb に焦点を合わせて、左矢印キーまたは右矢印キーを押します。)

- 間隔の範囲を変更するには、ハンドルのいずれかをドラッグします。 (キーボード: ハンドルに焦点を合わせて、右矢印キーまたは左矢印キーを押します。)

  別のコンカレンシー ビジュアライザー ズーム コントロールを使用して間隔を変更すると、変更を反映するために使用状況ナビゲーターが更新されます。