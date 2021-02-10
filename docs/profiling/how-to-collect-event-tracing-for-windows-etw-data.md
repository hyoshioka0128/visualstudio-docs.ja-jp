---
title: ETW (Event Tracing for Windows) データを収集する | Microsoft Docs
description: Event Trace for Windows (ETW) を使用して、アプリケーションでパフォーマンスの問題が発生している場所を特定する方法について学習します。 VSPerfReport.exe を使用してデータを表示します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.performance.property.events
helpviewer_keywords:
- event trace providers, performance tools
- profiling tools, event trace providers
- performance tools, enabling event trace providers
author: mikejo5000
ms.author: mikejo
manager: jmartens
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 77ddd22450786091c5240f26213633a7935c03dd
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99886289"
---
# <a name="how-to-collect-event-tracing-for-windows-etw-data"></a>方法: ETW (Event Tracing for Windows) データを収集する

Event Tracing for Windows (ETW) は、プロファイラー ログ カーネルやアプリケーション定義イベントを有効にする、効率的なカーネル レベルのトレース機能です。 イベント プロバイダーから収集したデータは、[VSPerfReport](../profiling/vsperfreport.md) コマンド ライン ツールの /**Summary:ETW** オプションを使用した場合のみ表示されます。 このレポートを使用すると、アプリケーション内でパフォーマンスの問題が発生した場所を特定できます。

> [!NOTE]
> Windows 8 および Windows Server 2012 の強化されたセキュリティ機能によって、Visual Studio プロファイラーがこれらのプラットフォームでデータを収集する方法に大幅な変更が必要になりました。 UWP アプリにも新しい収集手法が必要です。 「[Windows 8 および Windows Server 2012 アプリケーションのパフォーマンス ツール](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)」を参照してください。

## <a name="to-enable-event-trace-providers"></a>イベント トレース プロバイダーを有効にするには

1. **パフォーマンス エクスプローラー** で、パフォーマンス セッションを右クリックして、 **[プロパティ]** をクリックします。

2. **[プロパティ ページ]** で、 **[Windows イベント]** プロパティをクリックします。

3. **[Select event trace provider to collect data from]** (データを収集するイベント トレース プロバイダーを選択する) 一覧で、アプリケーションのプロファイリングに使用するイベント プロバイダーを選択します。

## <a name="see-also"></a>関連項目

[パフォーマンス セッションの構成](../profiling/configuring-performance-sessions.md)
