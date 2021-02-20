---
title: リソース競合データ値について | Microsoft Docs
description: あるアプリケーションで競合するスレッドに対して、共有リソースにアクセスするときに待機を強制するとき、リソース競合プロファイルによって詳細情報が収集されるしくみについて学習します。
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- concurrency profiling method
- Profiling Tools, concurrency method
author: mikejo5000
ms.author: mikejo
manager: jmartens
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 5e050879fc9a1bd74f95ae5d24a92dc7a59a73c8
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99886068"
---
# <a name="understand-resource-contention-data-values"></a>リソース競合データ値について

リソース競合プロファイルでは、アプリケーションで競合するスレッドによる共有リソースへのアクセスで待機が発生するたびに、詳細な呼び出し履歴情報が収集されます。

リソース競合レポートには、発生した競合の合計数と、リソースに対する合計待機時間 (待機が発生したモジュール、関数、ソース コード行、命令についての合計待機時間) が表示されます。

- 包括値は、リソースの競合により関数を強制的に待機状態にした競合の合計数、および関数が待機した合計時間を示します。  包括値には、関数によって呼び出された子関数によって発生した競合が含まれています。

- 排他値は、関数を待機状態にした競合の数、および関数の本体のコードによって発生した競合の数のみを示します。 子関数によって発生した競合は含まれません。 関数の排他時間には、関数本体のステートメントによって発生した待機時間のみが含まれます。

リソース競合レポート ビューには、一定期間内の個々の競合イベントを表示するタイムライン グラフも含まれ、特定のイベントを発生させたコール スタックも表示します。 詳細については、次のトピックを参照してください。

- [スレッドの詳細ビュー](../profiling/thread-details-view-contention-data.md)

- [リソースの詳細ビュー](../profiling/resource-details-view-contention-data.md)

コンカレンシー プロファイルの 2 つ目のモードの詳細については、「[Concurrency Visualizer (コンカレンシー ビジュアライザー)](../profiling/concurrency-visualizer.md)」を参照してください。
