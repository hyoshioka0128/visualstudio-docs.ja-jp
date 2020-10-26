---
title: 概要ビュー - インストルメンテーション データ | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- Summary view
ms.assetid: 0a3b3a1f-e22b-4ac8-b46e-71694e9b2cf1
caps.latest.revision: 16
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 5dc0b4195d33a7bf72d17681b6d71e78f1bacfe5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68157774"
---
# <a name="summary-view---instrumentation-data"></a>概要ビュー - インストルメンテーション データ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

概要ビューでは、プロファイリング実行で最もパフォーマンス負荷の高い関数についての情報を表示します。 通知リンクとレポート リストの説明など詳細については、「[Summary View](../profiling/summary-view.md) (概要ビュー)」をご覧ください。  
  
## <a name="timeline-graph"></a>タイムライン グラフ  
 概要ビューのタイムライン グラフには、プロファイリングが行われた期間のプロファイリングされたアプリケーション別にプロセッサ (CPU) 使用率が表示されます。 タイムライン グラフを使用すると、選択した期間に対してフィルター処理した結果を表示できます。 詳細については、「 [方法: 概要のタイムラインからレポートビューをフィルター処理する](../profiling/how-to-filter-report-views-from-the-summary-timeline.md)」を参照してください。  
  
## <a name="hot-path"></a>ホット パス  
 **[ホット パス]** には、最も時間のかかった実行パスが表示されます。 関数をクリックすると、その関数の [関数の詳細] ビューが表示されます。 関数のその他のビューを表示するには、関数を右クリックし、一覧からビューをクリックします。  
  
 **[ホット パス]** には、関数ごとに次のデータが含まれています。  
  
|Column|[説明]|  
|------------|-----------------|  
|**Name**|関数の名前です。|  
|**経過時間 % (子を含む)**|プロファイル データのすべての時間に対する、その関数が関数本体と呼び出した関数でコードの実行に費やした時間の割合。|  
|**経過時間 % (関数のみ)**|プロファイル データのすべての時間に対する、その関数が関数本体でコードの実行に費やした時間の割合。 関数が呼び出した関数で費やされた時間は含まれません。|  
  
## <a name="functions-with-most-individual-work"></a>個別作業が一番多い関数  
 呼び出した関数ではなく、関数の本体でコードの実行に最も時間を消費した関数の一覧。  
  
 **[個別作業が一番多い関数]** には、関数ごとに次のデータが含まれています。  
  
|Column|[説明]|  
|------------|-----------------|  
|**Name**|関数の名前です。|  
|**排他時間 %**|プロファイル データのすべての時間に対する、その関数が関数本体でコードの実行に費やした時間の割合。 関数が呼び出した関数で費やされた時間は含まれません。|  
  
## <a name="see-also"></a>参照  
 [概要ビュー](../profiling/summary-view-sampling-data.md)   
 [概要ビュー](../profiling/summary-view-dotnet-memory-data.md)
