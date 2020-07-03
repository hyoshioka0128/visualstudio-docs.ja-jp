---
title: 方法 - サンプリング イベントを選択する | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.performance.property.sampling
helpviewer_keywords:
- clock cycles sample event
- sample events, choosing
- profiling tools, sample events
- page faults sample event
- system calls sample event
- performance counter sample event
- performance tools, sample events
ms.assetid: ce7cb734-80ac-4930-a4ef-e24395e1cc07
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 8473ca1f5829faa2a76b5560132c7aada152dc3a
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/24/2020
ms.locfileid: "85329285"
---
# <a name="how-to-choose-sampling-events"></a>方法: サンプリング イベントを選択する
既定では、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] プロファイリング ツールは、プロファイリングされるプロセスによって使用されるプロセッサ サイクルの数として指定された間隔でパフォーマンス データを収集します。 既定の間隔のサイクル数は 10,000,000 です。これは、1 GHz のコンピューターで約 0.01 秒に相当します。 間隔のサイクル数とサンプル イベントは変更できます。 次のサンプル イベントを使用できます。

- クロック サイクル - CPU バインドの問題用。

- ページ フォールト - メモリ関連の問題用。

- システム コール - I/O 関連の問題用。

- パフォーマンス カウンター - 低レベルのパフォーマンスの問題用の CPU カウンター。

> [!IMPORTANT]
> サンプリング方法を使用して .NET メモリ データ (割り当てかオブジェクトの有効期間、またはその両方) を収集する場合、ユーザーが指定したサンプリング イベントはすべて無視され、適切なメモリの割り当てイベントかガベージ コレクション イベント、またはその両方を使用してデータが収集されます。

### <a name="to-select-a-sample-event"></a>サンプル イベントを選択するには

1. **パフォーマンス エクスプローラー**で、パフォーマンス セッションを右クリックして、 **[プロパティ]** をクリックします。

2. **[プロパティ ページ]** で、 **[サンプリング]** プロパティをクリックします。

3. **[サンプル イベント]** ドロップダウン リストで、アプリケーションのプロファイリングに使用するサンプル イベントを選択します。

    > [!NOTE]
    > **[利用可能なパフォーマンス カウンター]** は、 **[サンプル イベント]** ドロップダウン リストの **[パフォーマンス カウンター]** を選択した場合のみ有効です。

4. **[パフォーマンス カウンター]** を選択した場合、 **[使用可能なパフォーマンス カウンター]** ツリー ビュー コントロールから、特定の CPU カウンターを選択します。

    - **[Portable Events]** ノードのカウンターは、すべての種類のプロセッサで使用できます。

    - **[Platform Events]** ノードのカウンターは、現在のコンピューター上のプロセッサに固有であるため、他の種類のプロセッサでは使用できない場合があります。

5. サンプル イベントを選択すると、 **[サンプリング間隔]** テキスト ボックスに既定のサンプリング間隔の値が表示されます。 必要に応じて、テキスト ボックスに希望の値を入力できます。

## <a name="see-also"></a>関連項目
- [パフォーマンス セッションの構成](../profiling/configuring-performance-sessions.md)
- [方法: 収集方法を選択する](../profiling/how-to-choose-collection-methods.md)
- [CPU カウンターと Windows カウンター](../profiling/cpu-and-windows-counters.md)
- [サンプリング データ値について](../profiling/understanding-sampling-data-values.md)
- [コマンド ラインからのプロファイリング](../profiling/using-the-profiling-tools-from-the-command-line.md)
