---
title: リソース競合データ値について | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- concurrency profiling method
- Profiling Tools, concurrency method
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 3f522d1854cae86d9dc6e757ef0c9a62f4511800
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "74779988"
---
# <a name="understand-resource-contention-data-values"></a>リソース競合データ値について

リソース競合プロファイルでは、アプリケーションで競合するスレッドによる共有リソースへのアクセスで待機が発生するたびに、詳細な呼び出し履歴情報が収集されます。

リソース競合レポートには、発生した競合の合計数と、リソースに対する合計待機時間 (待機が発生したモジュール、関数、ソース コード行、命令についての合計待機時間) が表示されます。

- 包括値は、リソースの競合により関数を強制的に待機状態にした競合の合計数、および関数が待機した合計時間を示します。  包括値には、関数によって呼び出された子関数によって発生した競合が含まれています。

- 排他値は、関数を待機状態にした競合の数、および関数の本体のコードによって発生した競合の数のみを示します。 子関数によって発生した競合は含まれません。 関数の排他時間には、関数本体のステートメントによって発生した待機時間のみが含まれます。

リソース競合レポート ビューには、一定期間内の個々の競合イベントを表示するタイムライン グラフも含まれ、特定のイベントを発生させたコール スタックも表示します。 詳細については、次のいずれかのトピックを参照してください。

- [スレッドの詳細ビュー](../profiling/thread-details-view-contention-data.md)

- [リソースの詳細ビュー](../profiling/resource-details-view-contention-data.md)

コンカレンシー プロファイルの 2 つ目のモードの詳細については、「[Concurrency Visualizer (コンカレンシー ビジュアライザー)](../profiling/concurrency-visualizer.md)」を参照してください。
