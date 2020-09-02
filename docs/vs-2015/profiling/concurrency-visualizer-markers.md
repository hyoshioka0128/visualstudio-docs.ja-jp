---
title: コンカレンシー ビジュアライザー マーカー | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.cv.markersui
ms.assetid: c4692d17-6cd2-4ad1-8590-d7275c771c70
caps.latest.revision: 17
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 43b6115c45f9583b90711ef030834da662106f08
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65704351"
---
# <a name="concurrency-visualizer-markers"></a>コンカレンシー ビジュアライザー マーカー
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

コンカレンシー ビジュアライザーのマーカーはアプリ内のイベントを表すアイコンです。  通常、アプリはこれらのイベントを生成して、アプリケーションでのフェーズまたは出現回数を指定します。  アプリ、またはアプリで使用するライブラリとランタイムでイベントを生成することができます。  
  
## <a name="kinds-of-markers"></a>マーカーの種類  
 コンカレンシー ビジュアライザーでは、アプリケーション イベントを表す 3 種類のマーカー (フラグ、メッセージ、スパン) が使用されます。  
  
1. アプリの特定の時点を示す場合は、*フラグ*を使用します。  たとえば、変数値が特定のしきい値に達したことや、例外がスローされたことを表す場合はフラグを使用できます。  
  
2. *メッセージ*も一定の時点をマークしますが、ログ スタイルのトレースで使用できます。  たとえば、ログ ファイルにダンプされている場合、メッセージ呼び出しでラップできるため、コンカレンシー ビジュアライザーでトレースおよび表示することができます。 また、コンカレンシー ビジュアライザーを使用して、このデータを CSV ファイルにエクスポートすることもできます。  
  
3. *スパン*は、いずれかのフェーズなど、アプリにおける時間間隔を表します。  
  
## <a name="marker-linkage-to-threads"></a>スレッドへのマーカー リンケージ  
 マーカーを生成するスレッドにはそれぞれ別のタイムライン チャネルがあります。  マーカー イベントを生成するスレッドの ID は、マーカー チャネルの説明の横に表示されます。  マーカー チャネルの左側に表示される ID は、現在のプロセス内の別のスレッドの ID と一致します。  
  
## <a name="marker-importance"></a>マーカーの重要度  
 マーカーでは、4 つの重要度レベル (低、通常、高、重大) のいずれかを設定できます。  重要度レベルに基づいて、マーカーのソースをフィルター処理することができます。  たとえば、重要度が通常または重大である特定のソースのみのマーカーを表示する場合、[[詳細設定]](../profiling/advanced-settings-dialog-box-concurrency-visualizer.md) ダイアログ ボックスでフィルターを構成することができます。マーカーの重要度はそのヒント、および [[マーカー レポート]](../profiling/markers-report.md) に表示されます。  
  
## <a name="marker-category"></a>マーカーのカテゴリ  
 マーカーのカテゴリは、同じソースからのマーカー イベントのグループを示します。  コンカレンシー ビジュアライザーでは色を使用して、さまざまなカテゴリのフラグとスパンを区別します。 特定のイベント プロバイダーからのマーカー イベントをフィルター処理するために、カテゴリを使用するようにコンカレンシー ビジュアライザーを構成することができます。  フィルターを構成するには、[[詳細設定]](../profiling/advanced-settings-dialog-box-concurrency-visualizer.md) ダイアログ ボックスを使用します。  
  
## <a name="known-sources-of-markers"></a>マーカーの既知のソース  
 ETW プロバイダーは、特定の制約に準拠している限り、マーカーを生成できます。 マーカーの追加のイベント ソースをリッスンするようにコンカレンシー ビジュアライザーを構成することができます。 既定では、以下のイベント ソースをリッスンします。  
  
- [コンカレンシー ビジュアライザー SDK](../profiling/concurrency-visualizer-sdk.md)  
  
- [タスク並列ライブラリ (TPL)](https://msdn.microsoft.com/library/b8f99f43-9104-45fd-9bff-385a20488a23)  
  
- [データフロー](https://msdn.microsoft.com/library/643575d0-d26d-4c35-8de7-a9c403e97dd6)  
  
- [Parallel LINQ (PLINQ)](https://msdn.microsoft.com/library/3d4d0cd3-bde4-490b-99e7-f4e41be96455)  
  
- [コンカレンシー ランタイム](https://msdn.microsoft.com/library/874bc58f-8dce-483e-a3a1-4dcc9e52ed2c)  
  
- [シナリオ マーカーのサポート](https://msdn.microsoft.com/e3b55bc2-b451-4214-ae00-0c7f5a5baec8)  
  
- [C++ AMP (C++ Accelerated Massive Parallelism)](https://msdn.microsoft.com/library/e27824cb-3167-409b-8c3f-a0e476d8f349)  
  
  [[詳細設定]](../profiling/advanced-settings-dialog-box-concurrency-visualizer.md) ダイアログ ボックスの [マーカー] タブを使用して、コンカレンシー ビジュアライザーでさまざまなソースからのマーカーを表示するかどうかを制御できます。また、重要度とカテゴリに基づいて、マーカーをフィルター処理することができます。  
  
## <a name="markers-from-eventsource"></a>EventSource からのマーカー  
 コンカレンシー ビジュアライザーでは、EventSource イベントも表示できます。  詳細については、「[マーカーとしての EventSource イベントの視覚化](../profiling/visualizing-eventsource-events-as-markers.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [フラグマーカー](../profiling/flag-markers.md)   
 [メッセージマーカー](../profiling/message-markers.md)   
 [スパンマーカー](../profiling/span-markers.md)   
 [マーカーとしての EventSource イベントの視覚化](../profiling/visualizing-eventsource-events-as-markers.md)
