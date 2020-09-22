---
title: '方法 : Windows カウンター データを収集する | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.performance.property.syscounter
- vs.performance.property.wincounter
helpviewer_keywords:
- windows counters
- performance tools, using windows counters
- profiling tools, using windows counters
ms.assetid: db4fbac2-bea5-4558-aa8b-160fcccf4b33
caps.latest.revision: 18
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 9743fa7defbbf3321636d2ba4799454713a647db
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90842277"
---
# <a name="how-to-collect-windows-counter-data"></a>方法 : Windows カウンター データを収集する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Windows カウンターは、プロファイル中に一定間隔で収集できるシステム パフォーマンス カウンターです。 プロファイリング ツール レポートのマーク ビューでは、データ収集の間隔ごとに **[AutoMark]** のラベルが行に付けられます。 この行には、その間隔でのパフォーマンス カウンター値を示す列が含まれます。 2 個の具体的なマーク間の時間を分析するには、マークを選択して右クリックし、ショートカット メニューの **[フィルター方法]**  ->   **[マーク]** を選択します。  
  
 **必要条件**  
  
- [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)], [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)], [!INCLUDE[vsPro](../includes/vspro-md.md)]  
  
> [!NOTE]
> Windows 8 および Windows Server 2012 の強化されたセキュリティ機能によって、Visual Studio プロファイラーがこれらのプラットフォームでデータを収集する方法に大幅な変更が必要になりました。 Windows ストア アプリにも新しい収集手法が必要です。 「[Windows 8 および Windows Server 2012 アプリケーションのパフォーマンス ツール](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)」を参照してください。  
  
### <a name="to-collect-windows-counter-data"></a>Windows カウンター データを収集するには  
  
1. パフォーマンス エクスプローラーで、Windows カウンターを構成するセッションを右クリックし、 **[プロパティ]** を選択します。  
  
2. **[プロパティ] ページ**で、 **[Windows カウンター]** をクリックします。  
  
3. **[Windows カウンターの収集]** チェックボックスをオンにします。  
  
4. **[収集間隔 (ミリ秒)]** ボックスに、間隔を入力します。  
  
5. **[カウンター カテゴリ]** ドロップダウン リストで、カテゴリを選択します。  
  
6. **[インスタンス]** ドロップダウン リストで、インスタンスを選択します。  
  
7. アプリケーションをプロファイルするときに使用するカウンターを選択します。  
  
8. **[適用]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [パフォーマンスセッションの構成](../profiling/configuring-performance-sessions.md)   
 [パフォーマンスセッションのプロパティ](../profiling/performance-session-properties.md)   
 [CPU カウンターと Windows カウンター](../profiling/cpu-and-windows-counters.md)
