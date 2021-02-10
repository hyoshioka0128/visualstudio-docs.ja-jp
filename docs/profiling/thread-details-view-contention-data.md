---
title: スレッドの詳細ビュー - 競合データ | Microsoft Docs
description: スレッドの詳細ビューには、どのようにして、選択したプロファイリング実行スレッド内のブロック イベントがタイムライン グラフで表示されるかについて学習します。
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.performance.view.threaddetails
helpviewer_keywords:
- Thread Details view
ms.assetid: 874c3b1c-88d8-479a-bb35-1291d9aa8e67
author: mikejo5000
ms.author: mikejo
manager: jmartens
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 535b87a7bfd87a0d3932f33370cf31510787d7e5
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99949351"
---
# <a name="thread-details-view---contention-data"></a>スレッドの詳細ビュー - 競合データ
スレッドの詳細ビューには、リソースに対する競合によって発生した、選択したプロファイリング実行スレッド内のブロック イベントがタイムライン グラフで表示されます。 ブロック イベントは、あるリソースに対するアクセスを別のスレッドがロックしているために、スレッドが実行を中断されたときに発生します。

 このビューには、スレッドの実行タイムラインが横軸で、スレッドの横軸のタイムライン上にブロック イベントが縦棒で示されます。 必要に応じて、タイムラインのあるセクションを拡大して、個別のイベントを表示することもできます。 イベント到達するまでの関数の実行パスを表示するには、そのイベントの棒をクリックします。 関数が **[呼び出し履歴]** ウィンドウに表示されます。 関数のソース コードが使用可能な場合は、関数名をクリックして、Visual Studio IDE でソース ファイルを編集できます。

## <a name="navigate-the-timeline"></a>タイムライン内での移動

#### <a name="to-zoom-in-on-a-timeline-segment"></a>タイムライン セグメントを拡大するには

- マウス ポインターをクリックしてドラッグし、タイムラインの領域を選択します。

     マウスを離すと、選択した時間セグメントに合わせてビューが表示されます。 このプロセスを繰り返して、さらに詳細に拡大できます。 時間スクロール バーのスクロール ボックスには、ビューに表示されている時間セグメントの相対サイズが表示されます。

#### <a name="to-zoom-out-on-a-timeline"></a>タイムラインを縮小するには

- 前のズーム レベルに戻るには、**[縮小]** をクリックします。

- タイムライン全体をビューに表示するには、**[ズーム リセット]** をクリックします。

#### <a name="to-view-the-call-stack-of-an-event"></a>イベントの呼び出し履歴を表示するには

- タイムライン グラフで、イベントを表す縦棒をクリックします。

#### <a name="to-view-or-edit-the-source-code-of-a-function-in-the-call-stack"></a>呼び出し履歴内の関数のソース コードを表示または編集するには

- **[呼び出し履歴]** ウィンドウで関数名をクリックします。

  関数のソース コードは、現在のプロジェクトに含まれている必要があります。

#### <a name="to-view-the-contention-events-of-a-resource-in-all-threads-in-the-profiling-run"></a>プロファイリング実行内のすべてのスレッドでのリソースの競合イベントを表示するには

- タイムライン グラフで、リソースの名前または ID をクリックします。

     選択したリソースに対して[リソースの詳細ビュー](../profiling/resource-details-view-contention-data.md)が表示されます。

#### <a name="to-view-the-thread-contention-data-in-the-processes-window"></a>プロセス ウィンドウにスレッド競合データを表示するには

- タイムライン グラフで、**[合計]** をクリックします。

     選択したスレッドを表示する[プロセス ビュー](../profiling/process-view-contention-data.md)が表示されます。
