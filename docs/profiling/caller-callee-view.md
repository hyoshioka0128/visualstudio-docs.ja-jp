---
title: 呼び出し元/呼び出し先ビュー | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.performance.view.callercallee
helpviewer_keywords:
- profiling tools, reports, Caller/Callee view
- profiling tools, Caller/Callee view
- performance reports, Caller/Callee view
- Caller/Callee view
ms.assetid: d3511bcf-cce0-4cbe-aecb-b94c7c80ad1b
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: bab816a0b71adef190a7d919b5ada7138a6a0e7c
ms.sourcegitcommit: 00b71889bd72b6a566586885bdb982cfe807cf54
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2019
ms.locfileid: "74779715"
---
# <a name="callercallee-view"></a>[呼び出し元/呼び出し先] ビュー
呼び出し元/呼び出し先ビューには、選択した関数およびその親関数と子関数のプロファイル データが表示されます。 [呼び出し元/呼び出し先] ビューは、3 つのグリッドで構成されます。

 **[現在の関数]** は中央のグリッドに表示されます。このグリッドには、選択した関数に関するプロファイル情報が表示されます。 値には、プロファイル実行で収集対象になった関数のすべての呼び出しが含まれます。

 **[現在の関数を呼び出した関数]** は最上部のグリッドに表示されます。このグリッドには、呼び出し元 (親) 関数からの呼び出しによって生成された、選択した (現在の) 関数の値の数が表示されます。

 **[現在の関数によって呼び出された関数]** は、下部のグリッドに表示されます。このグリッドには、子関数が現在の関数によって呼び出されたときに、選択した関数の呼び出し先 (子) 関数に関するプロファイル情報が表示されます。

 呼び出し元/呼び出し先ビューに表示される列は、データの収集に使用したプロファイル方式 (サンプリングまたはインストルメンテーション) と、プロファイル実行で .NET メモリ データを収集対象としたかどうかによって異なります。

 レポート ビューの中央部分にある [現在の関数] で別の関数を選択するには、ビューの他の 2 つの部分に一覧表示されている関数のどれか 1 つをダブルクリックします。 レポート ビューはこの変更を反映して自動的に更新されます。

 データを並べ替えるには、列名をクリックします。 呼び出し元/呼び出し先ビューには、列を追加できます。 詳細については、[レポート ビューの列をカスタマイズする](../profiling/how-to-customize-report-view-columns.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [呼び出し元/呼び出し先ビュー - サンプリング データ](../profiling/caller-callee-view-sampling-data.md)
- [呼び出し元/呼び出し先ビュー - インストルメンテーション データ](../profiling/caller-callee-view-instrumentation-data.md)
- [呼び出し元/呼び出し先ビュー - .NET メモリ インストルメンテーション データ](../profiling/caller-callee-view-net-memory-instrumentation-data.md)
- [呼び出し元/呼び出し先ビュー - .NET メモリ サンプリング データ](../profiling/caller-callee-view-dotnet-memory-sampling-data.md)
- [呼び出し元/呼び出し先ビュー - 競合データ](../profiling/caller-callee-view-contention-data.md)
