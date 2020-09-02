---
title: メッセージ マーカー | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.cv.markers.message
ms.assetid: 721f40ca-5af2-4a01-b8b6-2b90f6cb7f89
caps.latest.revision: 18
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 84c7a173bf0b7f5b3dc2187c0c8574819b2317a9
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68176905"
---
# <a name="message-markers"></a>メッセージ マーカー
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

メッセージ マーカーは、ログ出力を表します。 メッセージは、特定のスレッドによって特定の時間に発行される文字列です。 メッセージは、その他のツールで使用するためにテキスト ファイルにエクスポートできます。 メッセージ文字列を確認するには、コンカレンシー ビジュアライザーで、メッセージにポインターを置くことができます。 そして、[マーカー レポート](../profiling/markers-report.md)で、すべてのメッセージ マーカーを確認できます。  次の図は、メッセージ マーカーを示しています。  
  
## <a name="message-aggregation-markers"></a>メッセージの集約マーカー  
 コンカレンシー ビジュアライザーで、複数のメッセージが相互に近接しすぎて、個別に描画できないことがあります。 そのような場合には、基になるメッセージを表す*メッセージ集約マーカー*が表示されます。 それらのアイコンのいずれかにポインターを置くと、表現されている、基になるメッセージの数がツールヒントに表示されます。 メッセージを表示するには、ズームインします。  限界までズームインしてもなお集約マーカーが表示される場合には、基になるメッセージを[マーカー レポート](../profiling/markers-report.md)で確認できます。  
  
## <a name="see-also"></a>参照  
 [同時実行ビジュアライザーマーカー](../profiling/concurrency-visualizer-markers.md)   
 [コンカレンシー ビジュアライザー SDK](../profiling/concurrency-visualizer-sdk.md)
