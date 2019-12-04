---
title: 概要ビュー - インストルメンテーション データ | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Summary view
ms.assetid: 0a3b3a1f-e22b-4ac8-b46e-71694e9b2cf1
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 2f52f80cad4ce7678a832a7b76a75d8f2fd4460e
ms.sourcegitcommit: 00b71889bd72b6a566586885bdb982cfe807cf54
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2019
ms.locfileid: "74778220"
---
# <a name="summary-view---instrumentation-data"></a>概要ビュー - インストルメンテーション データ
概要ビューでは、プロファイリング実行で最もパフォーマンス負荷の高い関数についての情報を表示します。 通知リンクとレポート リストの説明など詳細については、「[概要ビュー](../profiling/summary-view.md)」をご覧ください。

## <a name="timeline-graph"></a>タイムライン グラフ
 概要ビューのタイムライン グラフには、プロファイリングが行われた期間のプロファイリングされたアプリケーション別にプロセッサ (CPU) 使用率が表示されます。 タイムライン グラフを使用すると、選択した期間に対してフィルター処理した結果を表示できます。 詳細については、[概要ビューのタイムラインからレポート ビューをフィルター処理する](../profiling/how-to-filter-report-views-from-the-summary-timeline.md)」を参照してください。

## <a name="hot-path"></a>ホット パス
 **[ホット パス]** には、最も時間のかかった実行パスが表示されます。 関数をクリックすると、その関数の [関数の詳細] ビューが表示されます。 関数のその他のビューを表示するには、関数を右クリックし、一覧からビューをクリックします。

 **[ホット パス]** には、関数ごとに次のデータが含まれています。

|Column|説明|
|------------|-----------------|
|**Name**|関数の名前。|
|**包括経過時間 %**|プロファイル データのすべての時間に対する、その関数が関数本体と呼び出した関数でコードの実行に費やした時間の割合。|
|**排他経過時間 %**|プロファイル データのすべての時間に対する、その関数が関数本体でコードの実行に費やした時間の割合。 関数が呼び出した関数で費やされた時間は含まれません。|

## <a name="functions-with-most-individual-work"></a>個別作業が一番多い関数
 呼び出した関数ではなく、関数の本体でコードの実行に最も時間を消費した関数の一覧。

 **[個別作業が一番多い関数]** には、関数ごとに次のデータが含まれています。

|列|説明|
|------------|-----------------|
|**Name**|関数の名前。|
|**排他時間 %**|プロファイル データのすべての時間に対する、その関数が関数本体でコードの実行に費やした時間の割合。 関数が呼び出した関数で費やされた時間は含まれません。|

## <a name="see-also"></a>関連項目
- [概要ビュー - サンプリング データ](../profiling/summary-view-sampling-data.md)
- [概要ビュー - .NET メモリ データ](../profiling/summary-view-dotnet-memory-data.md)
