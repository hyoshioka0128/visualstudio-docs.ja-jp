---
title: パフォーマンス データ ファイルの比較 | Microsoft Docs
description: プロファイル ツールを使用して、2 つのレポート ファイル (.vsp または .vsps) を比較します。 この比較により、違い、パフォーマンスの低下、および改善が示されます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- profiling tools, comparing profiling tools report files
- profiling tools reports, comparing
ms.assetid: e6fda144-f21d-4912-9d16-1b8d3555a210
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 8d1c57c6c3dd8d7d01e37eae374c547e074d62e6
ms.sourcegitcommit: 7a5c4f60667b5792f876953d55192b49a73f5fe9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/16/2021
ms.locfileid: "98533499"
---
# <a name="compare-performance-data-files"></a>パフォーマンス データ ファイルを比較する

プロファイル ツールのデータ ファイルの比較機能を使用すると、2 つのレポート ファイル (.*vsp* または .*vsps*) を選択し、2 つのプロファイリング セッション間の違い、パフォーマンスの低下、および改善を示すレポートを生成できます。

[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] プロファイリング ツールのデータ ファイルの比較レポートでは、あるプロファイリング データ ファイルの分析結果と、他のデータ ファイルの基準の分析結果を比較します。 両方のデータ ファイルは、同じプロファイリング メソッドで生成されている必要があります。 分析された比較のレポートは .*vsps* ファイル形式で保存されます。

比較レポート ビューには、変化したデータのテーブル ビューが表示されます。 テーブルは、差分、またはベースラインからの変化を表示します。 差分は、古い値、基準値と、新しい分析による結果の値との違いを測定して計算されます。

プロファイラーのデータの比較は、コード内の関数、アプリケーション内のモジュール、行、命令ポインター (IP)、および種類に基づいて作成できます。

比較に使用できるプロファイリング データには、列に表示される情報が含まれています。 これらの列名の定義については、「[プロファイル ツールのレポート ビュー](../profiling/performance-report-views.md)」を参照してください。

しきい値を設定して、ノイズを減らし、指定した量によって変更のない行の比較テーブル ビュー内のデータをフィルター処理することができます。

## <a name="in-this-section"></a>このセクションの内容

[方法: パフォーマンス データ ファイルを比較する](../profiling/how-to-compare-performance-data-files.md)
