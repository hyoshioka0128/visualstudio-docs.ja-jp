---
title: モジュール ビュー | Microsoft Docs
description: モジュール ビューにプロファイル データのモジュールの一覧がどのように表示されるかについて学習します。 各モジュールが階層ツリーのルート ノードです。
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.performance.view.modules
helpviewer_keywords:
- Modules view
- profiling tools reports, Modules view
- profiling tools, Modules view
ms.assetid: 4314a404-2120-425b-be42-180cd4bac840
author: mikejo5000
ms.author: mikejo
manager: jmartens
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 412b40fdb38e4931bcefb05bde8d695955d6c05a
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99879736"
---
# <a name="modules-view"></a>モジュール ビュー
モジュール ビューには、プロファイリング データのモジュールが一覧表示されます。 各モジュールが階層ツリーのルート ノードです。 モジュールのプロファイリングされた関数が、モジュール ノードの下に一覧表示されます。 サンプリング メソッドを使用してプロファイリング データが収集された場合、関数ノードの下には行情報が一覧表示され、行ノードの下には命令ポインター データが一覧表示されます。

 モジュール名を展開してモジュールのパフォーマンス データのビューを表示したり、モジュール名を折りたたんでこれらのビューを閉じたりします。

 列を追加または削除するには、レポート ウィンドウ内を右クリックし、 **[列の追加と削除]** を選択します。 データを並べ替えるには、列名をクリックします。 詳細については、「[方法:レポート ビューの列をカスタマイズする](../profiling/how-to-customize-report-view-columns.md)」を参照してください。

 モジュール ビューに表示される列は、データの収集に使用したプロファイル方法 (サンプリングまたはインストルメンテーション)、およびプロファイル実行で .NET メモリ データを収集対象としたかどうかによって異なります。

## <a name="see-also"></a>関連項目
- [モジュール ビュー](../profiling/modules-view-sampling-data.md)
- [モジュール ビュー](../profiling/modules-view-instrumentation-data.md)
- [モジュール ビュー - インストルメンテーション](../profiling/modules-view-dotnet-memory-instrumentation-data.md)
- [モジュール ビュー - サンプリング](../profiling/modules-view-dotnet-memory-sampling-data.md)
- [モジュール ビュー](../profiling/modules-view-contention-data.md)
