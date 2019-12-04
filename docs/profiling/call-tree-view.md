---
title: コール ツリー ビュー | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.performance.view.calltree
helpviewer_keywords:
- Call Tree view
- profiling tools reports, Call Tree view
- performance reports, Call Tree view
- profiling tools, Call Tree view
ms.assetid: b2dbc033-bf95-4d10-8e51-f9462979133e
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 0b932d5f9e4a178c94f3e490c66cec64648ce4f6
ms.sourcegitcommit: 00b71889bd72b6a566586885bdb982cfe807cf54
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2019
ms.locfileid: "74773336"
---
# <a name="call-tree-view"></a>[コール ツリー] ビュー
[コール ツリー] ビューには、プロファイリングされるアプリケーションで走査された関数の実行パスが表示されます。 ツリーのルートは、アプリケーションまたはコンポーネントへのエントリ ポイントです。 各関数ノードは、呼び出したすべての関数と、その関数呼び出しに関するパフォーマンス データを表示します。

 [コール ツリー] ビューでは、最も時間を消費した関数や最も頻繁にサンプリングされた関数の実行パスを展開したり強調表示したりすることもできます。 最もパフォーマンス負荷の高いパスを表示するには、関数を右クリックし、 **[ホット パスの展開]** をクリックします。

 プロファイル実行の各プロセスは、ルート ノードとして表示されます。 コール ツリー ビューの開始ノードを設定するには、開始ノードとして設定するノードを右クリックし、 **[ルートの設定]** を選択します。

 ルート ノードを設定すると、選択したノードのサブツリーを除く他のすべてのエントリはビューから除外されます。 ルート ノードをリセットし、表示していたノードに戻すことができます。 コール ツリー ビュー ウィンドウで、右クリックし、 **[ルートのリセット]** を選択します。

 コール ツリー ビューをカスタマイズし、列を追加したり、削除したりできます。 **[Column Name Title Bar]\(列名タイトル バー\)** を右クリックし、 **[列の追加と削除]** を選択します。

 コール ツリー ビューは、表示されるデータの数を制限して、ノイズを除去するように構成できます。 ノイズ除去を行うことで、ビューでパフォーマンスの問題を発見しやすくなります。 パフォーマンスの問題が発見しやすくなれば、分析が簡単になります。 詳細については、[レポート ビューでノイズ除去を設定する](../profiling/how-to-configure-noise-reduction-in-report-views.md)」を参照してください。

> [!NOTE]
> 有効にしたときに警告を表示するようにノイズ除去が構成されている場合、レポートに情報バーが表示されます。

 コール ツリー ビューの列の定義については、以下をご覧ください。

- [コール ツリー ビュー](../profiling/call-tree-view-sampling-data.md)

- [コール ツリー ビュー](../profiling/call-tree-view-instrumentation-data.md)

- [コール ツリー ビュー - サンプリング](../profiling/call-tree-view-dotnet-memory-sampling-data.md)

- [コール ツリー ビュー](../profiling/call-tree-view-contention-data.md)

## <a name="see-also"></a>関連項目
- [パフォーマンス レポートのビュー](../profiling/performance-report-views.md)
- [インストルメンテーション データ値について](../profiling/understanding-instrumentation-data-values.md)
- [サンプリング データ値について](../profiling/understanding-sampling-data-values.md)
