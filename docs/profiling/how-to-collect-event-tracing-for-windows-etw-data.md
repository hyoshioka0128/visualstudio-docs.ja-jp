---
title: '方法: ETW (Event Tracing for Windows) データを収集する | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.performance.property.events
helpviewer_keywords:
- event trace providers, performance tools
- profiling tools, event trace providers
- performance tools, enabling event trace providers
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 2fa0547682351d1a7ba4efe4ce3b4350b906462c
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "74779026"
---
# <a name="how-to-collect-event-tracing-for-windows-etw-data"></a>方法: ETW (Event Tracing for Windows) データを収集する

Event Tracing for Windows (ETW) は、プロファイラー ログ カーネルやアプリケーション定義イベントを有効にする、効率的なカーネル レベルのトレース機能です。 イベント プロバイダーから収集したデータは、**VSPerfReport** コマンド ライン ツールの /[Summary:ETW](../profiling/vsperfreport.md) オプションを使用した場合のみ表示されます。 このレポートを使用すると、アプリケーション内でパフォーマンスの問題が発生した場所を特定できます。

> [!NOTE]
> Windows 8 および Windows Server 2012 の強化されたセキュリティ機能によって、Visual Studio プロファイラーがこれらのプラットフォームでデータを収集する方法に大幅な変更が必要になりました。 UWP アプリにも新しい収集手法が必要です。 ｢[Windows 8 および Windows Server 2012 アプリケーションのパフォーマンス ツール](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)」を参照してください。

## <a name="to-enable-event-trace-providers"></a>イベント トレース プロバイダーを有効にするには

1. **パフォーマンス エクスプローラー**で、パフォーマンス セッションを右クリックして、 **[プロパティ]** をクリックします。

2. **[プロパティ ページ]** で、 **[Windows イベント]** プロパティをクリックします。

3. **[Select event trace provider to collect data from]** (データを収集するイベント トレース プロバイダーを選択する) 一覧で、アプリケーションのプロファイリングに使用するイベント プロバイダーを選択します。

## <a name="see-also"></a>参照

[パフォーマンス セッションの構成](../profiling/configuring-performance-sessions.md)
