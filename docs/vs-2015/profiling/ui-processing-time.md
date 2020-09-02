---
title: UI 処理時間 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.cv.threads.timeline.uiprocessing
helpviewer_keywords:
- Concurrency Visualizer, UI Processing Time
ms.assetid: 0ddb05a3-8c6b-448b-8488-2751c1e5abcc
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 4bbed9d8c4725b6bd497377d4a9dee22f2f8573d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68145481"
---
# <a name="ui-processing-time"></a>UI 処理時間
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

タイムライン内のこれらのセグメントは、UI 処理として分類されるブロック時間と関連付けられています。 これは、スレッドが Windows メッセージをポンプしているか、他のユーザー インターフェイス (UI) の作業を実行していることを意味します。 この期間中、コンカレンシー ビジュアライザーが UI 処理としてカウントしている API で、スレッドがブロックされています。 `GetMessage()` や `MsgWaitForMultipleObjects()` などの API がこのグループになります。  
  
 定義済みのブロッキング API が識別されない場合、呼び出し履歴とプロファイル レポートを確認して、遅延の根本的な原因を判断します。  
  
 UI 処理カテゴリは、GUI アプリケーションの応答性を理解するのに重要であり、UI の応答性に依存するアプリケーションにはこのカテゴリが適しています。 たとえば、アプリケーション内の UI スレッドが UI 処理で 100% の時間を達成した場合、非常に応答性が高いと思われます。 ただし、UI スレッドが他のカテゴリで長時間を費やしている場合は、根本的な原因を見つけて、そのスレッドでの UI 以外のカテゴリを減らすためのオプションを検討してください。  
  
## <a name="see-also"></a>参照  
 [スレッド ビュー](../profiling/threads-view-parallel-performance.md)
