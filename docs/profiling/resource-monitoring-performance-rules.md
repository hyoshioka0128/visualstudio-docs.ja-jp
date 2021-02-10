---
title: リソース監視のパフォーマンス規則 | Microsoft Docs
description: リソース監視カテゴリのパフォーマンス メッセージに用意されている、アプリケーションのパフォーマンスに関する追加データについて学習します。
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: f0f77faf-0a05-4718-a2c5-47934be40868
author: mikejo5000
ms.author: mikejo
manager: jmartens
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 1fc17bd86868a7b3e87c47ec44fd5caabf7a6cfd
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99950144"
---
# <a name="resource-monitoring-performance-rules"></a>リソース監視のパフォーマンス規則
リソース監視カテゴリのパフォーマンス メッセージでは、アプリケーションのパフォーマンスに関する追加データが提供されます。 このデータを使用してパフォーマンスの問題を分析できます。 これらの規則は情報を提供するためのものであり、プロファイル実行ごとに報告されます。

|ルール|説明|
|-|-|
|[DA0501: プロセスによる平均 CPU 使用量をプロファイリングしています。](../profiling/da0501-average-cpu-consumption-by-the-process-being-profiled.md)|このメッセージにより、アプリケーションの命令の実行中にプロセッサがビジー状態になった時間がパーセントで報告されます。 プロファイリング中のプロセスがアクティブな状態にあるすべての測定間隔を通じて取得された値の平均値が、このメッセージによって報告されます。|
|[DA0502: プロセスによる最大 CPU 使用量をプロファイリングしています](../profiling/da0502-maximum-cpu-consumption-by-the-process-being-profiled.md)|このメッセージにより、アプリケーションの命令の実行中にプロセッサがビジー状態になった最大時間がパーセントで報告されます。 プロファイリング中のプロセスがアクティブな状態にあるすべての測定間隔を通じて取得された値のうち、最も大きな値がこのメッセージによって報告されます。|
|[DA0503: プロセスのワーキング セット平均バイト数がプロファイリングされています](../profiling/da0503-average-working-set-in-bytes-for-the-process-being-profiled.md)|このメッセージにより、プロファイルがアクティブな状態にあったときにプロセスが使用していた物理メモリ量の平均がバイト単位で報告されます。 この物理メモリの大きさはワーキング セットと呼ばれます。|
|[DA0504: プロセスのワーキング セット最大バイト数がプロファイリングされています](../profiling/da0504-maximum-working-set-in-bytes-for-the-process-being-profiled.md)|このメッセージにより、プロファイルがアクティブな状態にあったときにプロセスが使用していた物理メモリの最大量がバイト単位で報告されます。|
|[DA0505: プロセスに割り当てられた平均プライベート バイト数がプロファイリングされています](../profiling/da0505-average-private-bytes-allocated-for-the-process-being-profiled.md)|このメッセージにより、プロファイルがアクティブな状態にあったときにプロセスによって割り当てられた仮想メモリ量の平均がバイト単位で報告されます。 この仮想メモリの大きさは *プライベート バイト* と呼ばれます。 プライベート バイトは、プロセス内部で実行中のスレッドからのみアクセスできるプロセスによって割り当てられた仮想メモリの位置を表します。|
|[DA0506: プロセスに割り当てられた最大プライベート バイト数がプロファイリングされています](../profiling/da0506-maximum-private-bytes-allocated-for-the-process-being-profiled.md)|このメッセージにより、プロファイルがアクティブな状態にあったときにプロセスによって割り当てられた仮想メモリの最大量がプライベート バイト単位で報告されます。|
