---
title: '方法 : インストルメンテーションで短い関数を除外または含める | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- profiling tools, instrument events
- profiling tools, include short functions
- profiling tools, exclude short functions
ms.assetid: eaeead79-aafe-4490-86ff-6ed4cad9c15f
caps.latest.revision: 18
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: c8bb49e650f2395bac8a3b5eb1d0f52e2e168731
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68146112"
---
# <a name="how-to-exclude-or-include-short-functions-from-instrumentation"></a>方法 : インストルメンテーションで短い関数を除外または含める
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

既定では、プロファイリング ツールは*小規模関数*をインストルメンテーションから除外します。 小規模関数とは、関数の呼び出しを行わない短い関数のことです。 小規模関数を除外すると、インストルメンテーション オーバーヘッドが軽減するため、インストルメンテーションの速度が向上します。 また、小規模関数の除外によりパフォーマンス プロファイル データ ファイル (.vsp) のサイズが小さくなるため、分析に要する時間が短縮されます。 小規模関数が除外されると、その親関数の排他時間と包括時間に対して、小規模関数に費やされる時間が除外されます。 次に、インストルメンテーションで小規模関数を除外または含める手順について説明します。  
  
### <a name="to-exclude-or-include-short-functions-from-instrumentation"></a>インストルメンテーションで短い関数を除外または含めるには  
  
1. **パフォーマンス エクスプローラー**で、**パフォーマンス セッション**を選択します。次に、右クリックして **[プロパティ]** を選択します。  
  
     **[プロパティ ページ]** ダイアログ ボックスが表示されます。  
  
2. **[プロパティ ページ]** で、 **[インストルメンテーション]** プロパティをクリックします。  
  
3. インストルメンテーションから短い関数を除外するには、 **[短い関数をインストルメンテーションから除外]** をオンにします。 これが既定の設定です。  
  
     または  
  
     インストルメンテーションに短い関数を含めるには、 **[短い関数をインストルメンテーションから除外]** をオフにします。  
  
4. **[OK]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [データコレクションの制御](../profiling/controlling-data-collection.md)   
 [パフォーマンスセッションのプロパティ](../profiling/performance-session-properties.md)
