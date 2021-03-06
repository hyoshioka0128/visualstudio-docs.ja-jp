---
title: リソース監視のパフォーマンス規則 | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f0f77faf-0a05-4718-a2c5-47934be40868
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 258cb329adac23ea1bd463e22a0fd6ada7b526bc
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/16/2018
ms.locfileid: "51745618"
---
# <a name="resource-monitoring-performance-rules"></a>リソース監視のパフォーマンス規則
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

リソース監視カテゴリのパフォーマンス メッセージでは、アプリケーションのパフォーマンスに関する追加データが提供されます。 このデータを使用してパフォーマンスの問題を分析できます。 これらの規則は情報を提供するためのものであり、プロファイル実行ごとに報告されます。  
  
|||  
|-|-|  
|[DA0501: プロセスによる平均 CPU 使用量をプロファイリングしています。](../profiling/da0501-average-cpu-consumption-by-the-process-being-profiled.md)|このメッセージにより、アプリケーションの命令の実行中にプロセッサがビジー状態になった時間がパーセントで報告されます。 プロファイリング中のプロセスがアクティブな状態にあるすべての測定間隔を通じて取得された値の平均値が、このメッセージによって報告されます。|  
|[DA0502: プロセスによる最大 CPU 使用量をプロファイリングしています](../profiling/da0502-maximum-cpu-consumption-by-the-process-being-profiled.md)|このメッセージにより、アプリケーションの命令の実行中にプロセッサがビジー状態になった最大時間がパーセントで報告されます。 プロファイリング中のプロセスがアクティブな状態にあるすべての測定間隔を通じて取得された値のうち、最も大きな値がこのメッセージによって報告されます。|  
|[DA0503: プロセスのワーキング セット平均バイト数がプロファイリングされています](../profiling/da0503-average-working-set-in-bytes-for-the-process-being-profiled.md)|このメッセージにより、プロファイルがアクティブな状態にあったときにプロセスが使用していた物理メモリ量の平均がバイト単位で報告されます。 この物理メモリの大きさはワーキング セットと呼ばれます。|  
|[DA0504: プロセスのワーキング セット最大バイト数がプロファイリングされています](../profiling/da0504-maximum-working-set-in-bytes-for-the-process-being-profiled.md)|このメッセージにより、プロファイルがアクティブな状態にあったときにプロセスが使用していた物理メモリの最大量がバイト単位で報告されます。|  
|[DA0505: プロセスに割り当てられた平均プライベート バイト数がプロファイリングされています](../profiling/da0505-average-private-bytes-allocated-for-the-process-being-profiled.md)|このメッセージにより、プロファイルがアクティブな状態にあったときにプロセスによって割り当てられた仮想メモリ量の平均がバイト単位で報告されます。 この仮想メモリの大きさは*プライベート バイト*と呼ばれます。 プライベート バイトは、プロセス内部で実行中のスレッドからのみアクセスできるプロセスによって割り当てられた仮想メモリの位置を表します。|  
|[DA0506: プロセスに割り当てられた最大プライベート バイト数がプロファイリングされています](../profiling/da0506-maximum-private-bytes-allocated-for-the-process-being-profiled.md)|このメッセージにより、プロファイルがアクティブな状態にあったときにプロセスによって割り当てられた仮想メモリの最大量がプライベート バイト単位で報告されます。|



