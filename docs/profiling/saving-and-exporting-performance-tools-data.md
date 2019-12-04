---
title: パフォーマンス ツール データの保存とエクスポート | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- performance tools, saving and exporting reports
ms.assetid: 2e9b28fe-3ed2-4e1d-b9cb-0a5e384380b0
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 729dc2e28446420dd2590e132b7ec8a5444fcb9c
ms.sourcegitcommit: 00b71889bd72b6a566586885bdb982cfe807cf54
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2019
ms.locfileid: "74773900"
---
# <a name="save-and-export-performance-tools-data"></a>パフォーマンス ツール データの保存とエクスポート
この記事では、パフォーマンス データ ファイルを保存およびエクスポートする方法について説明します。

## <a name="how-to-save-performance-data-files-as-analyzed-report-files"></a>方法: 分析されたレポート ファイルとしてパフォーマンス データ ファイルを保存する
 プロファイル データ (.*vsp*) ファイルのフィルター処理済みビューまたはフィルター処理なしビューは、分析されたレポート (.*vsps*) ファイルとして保存することができます。 分析されたレポート ファイルは、[レポート ビュー] ウィンドウで表示することができ、ファイルのサイズは、元の .*vsp* ファイルよりもかなり小さくなります。 ただし、.*vsps* ファイルのデータにフィルターを適用することはできません。 統合開発環境 (IDE) でファイルを開かなくても、パフォーマンス エクスプローラーで、分析されたレポート ファイルを作成することができます。あるいは、.*vsp* ファイルを開き、フィルター処理してから、その結果を保存することもできます。

#### <a name="to-save-an-analyzed-performance-report-from-the-performance-explorer"></a>分析されたパフォーマンス レポートをパフォーマンス エクスプ ローラーで保存するには

1. **[レポート]** で、分析するプロファイル データ ファイルを右クリックして、 **[分析されたものを保存]** をクリックします。

2. **[分析されたデータの保存]** ダイアログ ボックスで、ディレクトリを指定し、ファイル名を入力します。

3. **[保存]** をクリックします。

#### <a name="to-save-an-analyzed-performance-report-from-the-report-view-window"></a>[レポート ビュー] ウィンドウで、パフォーマンス レポートを保存して分析するには

1. [レポート ビュー] ウィンドウで、プロファイル データ (.*vsp*) ファイルを開きます。

2. (省略可能) データにフィルターを適用します。 詳細については、「[パフォーマンス レポート ビュー フィルター](../profiling/performance-report-view-filter.md)」を参照してください。

3. レポート ビュー ウィンドウのツールバーで、 **分析されたものを保存** をクリックします。

4. **[分析されたデータの保存]** ダイアログ ボックスで、ディレクトリを指定し、ファイル名を入力します。

5. **[保存]** をクリックします。

## <a name="how-to-export-profiling-tools-reports-to-an-xml-or-csv-file"></a>方法: プロファイリング ツールのレポートを .xml または .csv ファイルにエクスポートする
 1 つまたは複数のレポート ビューを、.*vsp* ファイルまたは .*vsps* プロファイル データ ファイルから、コンマ区切りファイルまたは XML ファイルとしてエクスポートすることができます。 レポート ビュー ウィンドウでエクスポートする前にデータをフィルター処理することも、 **パフォーマンス エクスプ ローラー** ウィンドウからデータ ファイル全体のレポート ビューをエクスポートすることもできます。

> [!NOTE]
> さらに、[レポート ビュー] ウィンドウで選択した行をタブ区切り値としてコピーして貼り付けることもできます。

#### <a name="to-export-performance-reports-from-the-performance-explorer-window"></a>[パフォーマンス エクスプ ローラー] ウィンドウから、パフォーマンス レポートをエクスポートするには

1. **[パフォーマンス エクスプローラー]** で、レポートを選択し、右クリックして **[エクスポート]** を選択します。

     **[レポートのエクスポート]** ダイアログ ボックスが表示されます。

2. エクスポートするレポート ビューを選択します。

3. **[レポートに付けるプレフィックス]** で、レポート名に追加するプレフィックスを指定します。

4. **[エクスポートされたレポートの場所]** で、ディレクトリを指定します。

5. **[エクスポートされたレポート形式]** で、[CSV (コンマ区切り) (\*.csv\)] または [XML データ (\*.xml\)] を選びます。

6. **[エクスポート]** をクリックします。

     各レポート ビューは、\<プレフィックス>_\<レポート ビュー名>.\<csv&#124;xml> という名前の別のファイルに保存されます

#### <a name="to-export-performance-reports-from-the-report-view-window"></a>[レポート ビュー] ウィンドウからパフォーマンス レポートをエクスポートするには

1. [レポート ビュー] ウィンドウで .*vsp* ファイルを開きます。

2. (省略可能) データにフィルターを適用します。 詳細については、「[パフォーマンス レポート ビュー フィルター](../profiling/performance-report-view-filter.md)」を参照してください。

3. レポート ビュー ウィンドウのツールバーで  **レポートのエクスポート** をクリックします。

4. エクスポートするレポート ビューを選択します。

5. **[レポートに付けるプレフィックス]** で、レポート名に追加するプレフィックスを指定します。

6. **[エクスポートされたレポートの場所]** で、ディレクトリを指定します。

7. **[エクスポートされたレポート形式]** で、[CSV (コンマ区切り) (\*.csv)] または [XML データ (\*.xml)] を選びます。

8. **[エクスポート]** をクリックします。

     各レポート ビューは、\<プレフィックス>_\<レポート ビュー名>.\<csv&#124;xml> という名前の別のファイルに保存されます

## <a name="see-also"></a>関連項目
- [パフォーマンス エクスプローラー](../profiling/performance-explorer.md)
- [パフォーマンス ツール データの分析](../profiling/analyzing-performance-tools-data.md)
- [パフォーマンス データ ファイルを比較する](../profiling/comparing-performance-data-files.md)
- [VSPerfReport](../profiling/vsperfreport.md)
