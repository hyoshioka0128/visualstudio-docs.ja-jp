---
title: CPU カウンター データを収集する | Microsoft Docs
description: CPU (ハードウェア) イベント カウンターを使用してハードウェア固有のパフォーマンス データを収集する方法について学習します。 この記事では、さまざまな種類のイベントを示します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.performance.property.cpucounters
helpviewer_keywords:
- profiling tools, using portable CPU counters
- performance tools, portable CPU counters
author: mikejo5000
ms.author: mikejo
manager: jmartens
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 0a085f732263e0d2eb3d7e1f211c54fac46fbc6e
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99876902"
---
# <a name="how-to-collect-cpu-counter-data"></a>方法: CPU カウンター データを収集する

CPU イベント カウンターはハードウェア固有のパフォーマンス データの収集に使用します。 この記事では、インストルメンテーション プロファイリング方式を使用した場合の、イベント カウンター データを収集する方法を示します。

2 種類の CPU カウンター イベントが発生します。

- ポータブル イベント - 特定の CPU に関係なく、収集可能な CPU イベントです。

- プラットフォーム イベント - 特定の CPU に関連付けられた CPU イベントです。

ポータブル イベントには、Instructions Retired や Non Halted Cycles などの一般的なイベント、CPU バッファー イベント、分岐イベント、L2 キャッシュ イベントなどがあります。 使用できるプラットフォーム イベント カウンターはプロセッサの製造元によって決まります。

イベントのカテゴリは、ポータブル カウンターとプラットフォーム カウンターの間で共有できます。 たとえば、次のデータのカテゴリは、両方のタイプで一般的に共通するものです。

- メモリ イベント。

- フロントエンド イベント。

- 分岐イベント。

プロファイラーでは、次の 2 つの方法でパフォーマンス カウンター データを収集できます。

- インストルメンテーションによってプロファイリングする場合は、1 つ以上のカウンターからデータを収集します。

- サンプリングによってプロファイリングする場合は、サンプリング間隔としてカウンター イベントを指定します。 詳細については、「[方法:サンプリング イベントを選択する](../profiling/how-to-choose-sampling-events.md)」を参照してください。

## <a name="to-collect-cpu-performance-counter-data-when-you-profile-by-instrumentation"></a>インストルメンテーションによってプロファイリングする場合に、CPU パフォーマンス カウンター データを収集するには

1. パフォーマンス セッションの **[プロパティ ページ]** で **[CPU カウンター]** をクリックします。

2. **[CPU カウンターの収集]** チェック ボックスをオンにします。

3. 収集するサンプル イベントが見つかるまで、 **[使用可能なパフォーマンス カウンター]** ツリーを展開します。

4. 収集するそれぞれのイベントについて、イベントを選択して右矢印をクリックし、そのイベントを **[選択されたカウンター]** 一覧に追加します。

    > [!NOTE]
    > **[使用可能なパフォーマンス カウンター]** は、 **[CPU カウンターの収集]** チェック ボックスがオンになっている場合のみ有効です。

## <a name="see-also"></a>関連項目

[パフォーマンス セッションの構成](../profiling/configuring-performance-sessions.md)
[パフォーマンス セッションのプロパティ](../profiling/performance-session-properties.md)
[CPU カウンターと Windows カウンター](../profiling/cpu-and-windows-counters.md)
[方法: サンプリング イベントを選択する](../profiling/how-to-choose-sampling-events.md)
