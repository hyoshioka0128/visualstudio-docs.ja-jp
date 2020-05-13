---
title: チャネルの管理 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.cv.threads.tools.managechannels
helpviewer_keywords:
- Concurrency Visualizer, Manage Channels
ms.assetid: 507b06e9-bb56-4a72-8fd5-f91f958da6fc
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0b1480bab2f52383a8ca3a5b0ac22fd56acb5e01
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "64779243"
---
# <a name="manage-channels"></a>チャネルの管理
コンカレンシー ビジュアライザーの**スレッド ビュー**では、プロセスのチャネルを整理して、特定のパターンを調べることができます。 チャネルを並べ替えしたり、上下に移動したり、非表示/表示を切り替えることができます。

## <a name="sort-by"></a>並べ替え
 [並べ替え] コントロールを使用して、現在のズーム レベルに基づいて、異なる基準でスレッドを並べ替えることができます。 これは、特定のパターンを探しているときに特に便利です。 次のような条件で並べ替えることができます。

|条件|定義|
|--------------|----------------|
|Start Time|開始時刻でスレッドを並べ替えます。 これが既定の並べ替え順序です。|
|終了時刻|終了時刻でスレッドを並べ替えます。|
|実行|実行に費やした時間の割合でスレッドを並べ替えます。|
|Synchronization|同期に費やした時間の割合でスレッドを並べ替えます。|
|I/O|入出力 (データの読み取りと書き込み) に費やした時間の割合でスレッドを並べ替えます。|
|Sleep|スリープに費やした時間の割合でスレッドを並べ替えます。|
|Paging|ページングに費やした時間の割合でスレッドを並べ替えます。|
|優先|優先処理に費やした時間の割合でスレッドを並べ替えます。|
|UI 処理|ユーザー インターフェイス処理に費やした時間の割合でスレッドを並べ替えます。|

## <a name="move-selected-channel-up-or-down"></a>選択したチャネルを上下に移動
 これらのコントロールを使用して、一覧でチャネルを上または下に移動できます。 たとえば、関連するチャネルを隣同士に配置すると、特定のパターンまたはスレッド間の関係を確認する助けになります。

## <a name="move-selected-channel-to-top-or-bottom"></a>選択したチャネルを一番上または一番下に移動
 選択したチャネルを一覧の一番上または一番下に移動することにより、特定のパターンを確認することができ、他のチャネルを確認できたときに一部のチャネルを除外することができます。

## <a name="hide-selected-channels"></a>選択したチャネルを非表示にする
 チャネルを非表示にするには、このコントロールを選択します。 たとえば、あるスレッドがマネージド プロセスの有効期間中に 100% の同期を示している場合は、他のスレッドを分析するときにはそれを非表示にすることができます。

> [!NOTE]
> スレッドを非表示にすると、アクティブな凡例およびプロファイル レポートに示される計算時間からも除外されます。

## <a name="show-all-channels"></a>すべてのチャネルを表示
 1 つまたは複数のチャネルが表示されていないときに、このコントロールはアクティブになります。 これを選択すると、すべての非表示の要素が表示され、時間の計算に再び含められます。

## <a name="move-markers-to-top"></a>マーカーを先頭へ移動
 トレースにマーカー イベントが含まれている場合は、このコマンドを使用して、マーカーのチャネルをタイムラインの先頭に移動することができます。 それらの相対順序は保持されます。

## <a name="group-markers-by-thread"></a>スレッド別にマーカーをグループ化
 トレースにマーカー イベントが含まれている場合は、このコマンドを使用して、それらのマーカー イベントを生成したスレッドの下にマーカーのチャネルをグループ化することができます。  ディスクのチャネルはチャネルの一覧の先頭に移動し、GPU チャネルは、一番下に移動します。

## <a name="see-also"></a>参照
- [ズーム コントロール (スレッド ビュー)](../profiling/zoom-control-threads-view.md)
- [測定モード オン/オフ](../profiling/measure-mode-on-off.md)
- [スレッド ビュー](../profiling/threads-view-parallel-performance.md)