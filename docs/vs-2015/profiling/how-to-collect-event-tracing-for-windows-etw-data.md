---
title: '方法: ETW (Event Tracing for Windows) データを収集する | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.performance.property.events
helpviewer_keywords:
- event trace providers, performance tools
- profiling tools, event trace providers
- performance tools, enabling event trace providers
ms.assetid: aa2261fe-d5f5-49fc-a171-d18842e1dc7d
caps.latest.revision: 31
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 9d113a32622c40c68a030fdbc670ec19c6038de2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841860"
---
# <a name="how-to-collect-event-tracing-for-windows-etw-data"></a>方法: ETW (Event Tracing for Windows) データを収集する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Event Tracing for Windows (ETW) は、プロファイラー ログ カーネルやアプリケーション定義イベントを有効にする、効率的なカーネル レベルのトレース機能です。 イベント プロバイダーから収集したデータは、[VSPerfReport](../profiling/vsperfreport.md) コマンド ライン ツールの /**Summary:ETW** オプションを使用した場合のみ表示されます。 このレポートを使用すると、アプリケーション内でパフォーマンスの問題が発生した場所を特定できます。  
  
 **必要条件**  
  
- [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)], [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)], [!INCLUDE[vsPro](../includes/vspro-md.md)]  
  
> [!NOTE]
> Windows 8 および Windows Server 2012 の強化されたセキュリティ機能によって、Visual Studio プロファイラーがこれらのプラットフォームでデータを収集する方法に大幅な変更が必要になりました。 Windows ストア アプリにも新しい収集手法が必要です。 「[Windows 8 および Windows Server 2012 アプリケーションのパフォーマンス ツール](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)」を参照してください。  
  
### <a name="to-enable-event-trace-providers"></a>イベント トレース プロバイダーを有効にするには  
  
1. **パフォーマンス エクスプローラー**で、パフォーマンス セッションを右クリックして、 **[プロパティ]** をクリックします。  
  
2. **[プロパティ ページ]** で、 **[Windows イベント]** プロパティをクリックします。  
  
3. **[Select event trace provider to collect data from]** (データを収集するイベント トレース プロバイダーを選択する) 一覧で、アプリケーションのプロファイリングに使用するイベント プロバイダーを選択します。  
  
## <a name="see-also"></a>参照  
 [パフォーマンスセッションの構成](../profiling/configuring-performance-sessions.md)
