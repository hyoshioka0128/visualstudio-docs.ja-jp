---
title: パフォーマンス データ収集の一時停止と再開 | Microsoft Docs
description: プロファイル セッション ページ ウィンドウから、プロファイリング データの収集を対話形式で制御する方法について学習します。
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- profiling tools, remote profiling
ms.assetid: b8e76363-65cd-424d-8173-3e2b5f54203b
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 3e9cd58eb6563298a0ee38fbad0cbae5d85e57e9
ms.sourcegitcommit: 18729d7c99c999865cc2defb17d3d956eb3fe35c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2021
ms.locfileid: "98723349"
---
# <a name="how-to-pause-and-resume-performance-data-collection"></a>方法: パフォーマンス データ収集の一時停止と再開
プロファイル セッション ページ ウィンドウから、プロファイリング データの収集を対話形式で制御することができます。

 データ収集を制御することで、プロファイル データ ファイルのサイズを小さくし、対象とする操作のデータのみを収集することができます。 プロファイリングは、パフォーマンス セッション内で複数回一時停止および再開することができます。

 ![プロファイリング セッション ページ](../profiling/media/prof_profilingsessionpage.png "PROF_ProfilingSessionPage")

> [!NOTE]
> プロファイリングを一時停止した状態でパフォーマンス セッションを開始し、プログラム実行の後の時点でプロファイリングを再開することもできます。 プロファイリングを一時停止した状態でパフォーマンス セッションを開始するには、 **[デバッグ]** メニューの **[Start Performance Analysis with Profiling Paused]\(プロファイリングを一時停止してパフォーマンス分析を開始)** コマンドを選択します。

### <a name="to-pause--resume-or-stop-profiling"></a>プロファイリングを一時停止、再開、または停止するには

- プロファイル セッション ページで、次のように操作します。

  - データ コレクションを中断するには、 **[収集の一時停止]** を選択します。

  - データ コレクションを一時停止した後で再開するには、 **[収集の再開]** を選択します。

  - プロファイリング セッションを終了してレポートを生成するには、 **[プロファイリングの停止]** を選択します。

## <a name="see-also"></a>関連項目
- [データ収集の制御](../profiling/controlling-data-collection.md)
- [方法: パフォーマンス データの収集の開始と終了](../profiling/how-to-start-and-end-performance-data-collection.md)
