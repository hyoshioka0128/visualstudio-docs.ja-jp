---
title: スパン マーカー | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.cv.markers.span
ms.assetid: 736b7765-9c71-44d7-85e5-79787d13d91c
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c69b48a5b1b551e2e29b9aa10e7f68ff0df0e379
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "62980973"
---
# <a name="span-markers"></a>スパン マーカー
スパン マーカーは、アプリケーションの意味のあるフェーズを表します。 たとえば、スパンを使用して、特定の作業項目を処理する時間間隔を表すことができます。 その長さは、対応するアプリケーション フェーズの期間を表します。 この図は、コンカレンシー ビジュアライザーのスパンを示しています。

 ![コンカレンシー ビジュアライザーのスパン マーカー](../profiling/media/cvmarkerspan.png "CVMarkerSpan") コンカレンシー ビジュアライザーのスパン マーカー

## <a name="span-category"></a>スパン カテゴリ
 スパン マーカーは、カテゴリに応じて 5 種類の色のいずれかで表示されます。 色が 6 種類以上ある場合、色は繰り返し使用されます。 カテゴリには任意の整数を指定できます。 この図では、使用される 5 つの色を示します。

 ![異なるカテゴリの 5 つの範囲](../profiling/media/cvmarkerspancategory.png "CVMarkerSpanCategory") 最初の 5 つのスパン カテゴリの色

## <a name="span-aggregation-markers"></a>スパンの集約マーカー
 コンカレンシー ビジュアライザーで、複数のスパン マーカーが相互に近接しすぎて、個別に描画できないことがあります。 そのような場合には、基になるスパンを表現する灰色の*スパン集約マーカー*が表示されます。 それらのアイコンのいずれかにポインターを置くと、表現されている、基になるスパンの数がツールヒントに表示されます。 スパンを表示するには、ズーム インします。 限界までズームインしてもなおスパン集約マーカーが表示される場合には、基になるスパン マーカーを[マーカー レポート](../profiling/markers-report.md)で確認できます。 次の図は、スパン集約マーカーを示しています。

 ![コンカレンシー ビジュアライザーの集約スパン マーカー](../profiling/media/cvmarkerspanaggregate.png "CVMarkerSpanAggregate") スパン集約マーカー

## <a name="see-also"></a>関連項目
- [コンカレンシー ビジュアライザー マーカー](../profiling/concurrency-visualizer-markers.md)
- [コンカレンシー ビジュアライザー SDK](../profiling/concurrency-visualizer-sdk.md)