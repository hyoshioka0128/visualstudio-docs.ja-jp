---
title: UI 処理時間 | Microsoft Docs
description: タイムライン内のセグメントは、UI 処理として分類されるブロック時間と関連付けられていることについて学習します。
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.cv.threads.timeline.uiprocessing
helpviewer_keywords:
- Concurrency Visualizer, UI Processing Time
ms.assetid: 0ddb05a3-8c6b-448b-8488-2751c1e5abcc
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 809af327fc2bb608647a76575736bd0e2b00c5b2
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99922031"
---
# <a name="ui-processing-time"></a>UI 処理時間
タイムライン内のこれらのセグメントは、UI 処理として分類されるブロック時間と関連付けられています。 これは、スレッドが Windows メッセージをポンプしているか、他のユーザー インターフェイス (UI) の作業を実行していることを意味します。 この期間中、コンカレンシー ビジュアライザーが UI 処理としてカウントしている API で、スレッドがブロックされています。 `GetMessage()` や `MsgWaitForMultipleObjects()` などの API がこのグループになります。

 定義済みのブロッキング API が識別されない場合、呼び出し履歴とプロファイル レポートを確認して、遅延の根本的な原因を判断します。

 UI 処理カテゴリは、GUI アプリケーションの応答性を理解するのに役立ち、UI の応答性に依存するアプリケーションにはこのカテゴリが適しています。 たとえば、アプリケーション内の UI スレッドが UI 処理で 100% の時間を達成した場合、応答性が高いと思われます。 ただし、UI スレッドが他のカテゴリで長時間を費やしている場合は、根本的な原因を見つけて、そのスレッドでの UI 以外のカテゴリを減らすためのオプションを検討してください。

## <a name="see-also"></a>関連項目
- [スレッド ビュー](../profiling/threads-view-parallel-performance.md)