---
title: R のサンプル プロジェクト
description: Visual Studio で R を使い始めるときに役立つサンプルのコレクションの索引です。
ms.date: 01/24/2018
ms.topic: conceptual
author: kraigb
ms.author: kraigb
manager: jmartens
ms.workload:
- data-science
ms.openlocfilehash: 0ed322a03d056f72ac2246e96d3aaeefa8f557c7
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99967021"
---
# <a name="r-tools-for-visual-studio-sample-projects"></a>R Tools for Visual Studio のサンプル プロジェクト

次のサンプル コレクションを使用して、R、R Tools for Visual Studio (RTVS)、Microsoft Machine Learning Server の使用を開始できます。

1. [サンプルの ZIP ファイル](https://github.com/Microsoft/RTVS-docs/archive/master.zip)をダウンロードし、フォルダーを選択して展開します。
1. `examples/Examples.sln` を開くと、プロジェクトにフォルダーが 2 つ表示されます。

    - "*A First Look at R*" には、R を初めて使用するユーザーのために簡単な概要が含まれます。
    - "*MRS and Machine Learning*" には、機械学習に R と Microsoft Machine Learning Server を使用する方法の例が含まれます。

## <a name="a-first-look-at-r"></a>初めて R を検討する (A First Look at R)

このサンプルでは、2 つのソース ファイル内の詳細なコメントを使って、R を詳しく説明しています。 コードを 1 行ずつ **[R インタラクティブ]** ウィンドウに送るには、ファイルの一番上にカーソルを置き、Ctrl キーを押しながら Enter キーを押す方法が簡単です。 (パッケージをインストールする行は、完了までに 1、2 分かかる可能性があります)。

- `1-Getting Started with R.R` には、パッケージの使用、データの読み込みと分析、およびプロットなど、多くの R の基本が含まれています。

    !["1-Getting Started with R.R" サンプルの出力例](media/samples-getting-started-output.png)

- `2-Introduction to ggplot2.R` では、視覚に訴えるプロットとシンプルな構文で知られる ggplot2 グラフィック パッケージを紹介します。 この例では、フィジーの地震データを視覚化しています。

    !["2-Introduction to ggplot2.R" サンプルの出力例](media/samples-ggplot-output.png)

## <a name="microsoft-machine-learning-server-and-machine-learning"></a>Microsoft Machine Learning Server と Machine Learning

この例のコレクションでは、R を使用して Machine Learning モデルを作成する方法と [Microsoft Machine Learning Server](/machine-learning-server/what-is-machine-learning-server) を活用する方法を示します。

他の例と同様に、ファイルを開き、ファイルの先頭にカーソルを置いて、**Ctrl** キーを押しながら **Enter** キーを押して 1 行ずつコードをステップ実行します。 詳細については、各フォルダーのマークダウン ファイルも参照してください。

- `Benchmarks` では、多数の集中的な並列線形代数計算を実行し、Microsoft R Open と Intel 数値演算ライブラリ (MKL) を使用して向上するパフォーマンスを示します。 ベンチマークでは、シミュレートされたデータを使用して、2 つのスレッド間の行列計算を具体的に比較します。

    ![ベンチマーク プロットの例](media/samples-mro-benchmark-plot.png)

- `Bike_Rental_Estimation_with_MRS` では、Microsoft ML Server を使用して、履歴データセットに基づくレンタルサイクルの需要予測モデルを作成します。

- `Data_Exploration` には、次の 3 つのスクリプトが含まれます。

  - `Import Data from URL.R` では、URL によって特定されたデータ ファイルを R に読み込む方法を示します。
  - `Import Data from URL to xdf.R` では、URL によって特定されたデータ ファイルを xdf として Microsoft ML Server に読み込む方法を示します。
  - `Using ggplot2.R` は、`A First Look at R/2-Introduction to ggplot2.R` サンプルの拡張機能です。このスクリプトでは、対話型の 3D プロットなど、ggplot2 の機能の詳細なツアーを示します。

      ![ggplot2.R を使用した出力例](media/samples-3d-interactive.png)

- `Datasets` には、他のサンプルによって使用される *.csv* ファイルが 3 つ含まれています。
- `Flight_Delays_Prediction_with_R` と `Flight_Delays_Prediction_with_MRS` では、R、Machine Learning、過去の定時運行データおよび気象データを使用して、航空便の遅延を予測する方法を示します。
- `Machine learning` には、航空便の遅延、住宅価格、レンタルサイクルの予測方法を学習できる 3 つのサンプルが含まれています。 また、これらのサンプルは、R と Microsoft ML Server のアプリケーションから現実世界の問題へのデモンストレーションでもあります。 また、いくつかの一般的な Machine Learning モデルを使用し、[Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) ワークスペースを使用して、Azure Web サービスとして配置する方法も示します。

- `R_MRO_MRS_Comparison` は、6 パーツの比較で、構文、コンストラクト、パフォーマンスを含む、R、Microsoft R Open、Microsoft ML Server の類似点と相違点を示しています。

## <a name="whats-special-about-microsoft-r-open-and-microsoft-ml-server"></a>Microsoft R Open と Microsoft ML Server の特別な点

[Microsoft R Open](https://mran.revolutionanalytics.com/download/) (Microsoft が配布する R) は、次の 2 つの重要な点が [CRAN R](https://cran.r-project.org/) とは異なります。

1. [Intel 数値演算ライブラリ](https://software.intel.com/intel-mkl)と併用時の[優れた計算性能](https://mran.revolutionanalytics.com/rro/#intelmkl1)。 ライブラリは、Microsoft R Open と共に使用するために、Microsoft から無料でダウンロードして入手できます。

1. [再現可能な R ツールキット](https://mran.revolutionanalytics.com/rro/#reproducibility)。これは、R プログラムをビルドするために使用したライブラリを、作業を再現する必要がある他のユーザーが常に入手できるようにします。

[Microsoft ML Server (MLS)](/machine-learning-server/what-is-machine-learning-server) は、R の拡張機能であり、多くのデータを高速に処理することができます。 次の 2 つの利便性の高い機能を R に提供します。

1. RAM の制限がない大きなデータ セット。 ML Server では、Hadoop クラスター、データベース、データ ウェアハウスなど、さまざまなソースからメモリ不足になるデータを処理できます。

1. 並行、マルチコア処理。 MLS では、利用可能な演算リソース全体に計算を効率的に分散させることができます。 個人のワークステーションまたはリモート クラスターで、MLS は回答を高速に取得します。

次の比較では、MKL を使用する MLS と MRO が、MKL を使用しない R と MRO より特定のマトリックス計算に関連する計算性能で特に優れていることを示しています。 シミュレートされたデータは、この計算で使用されます。

![MKL を使用する MLS と MRO と MKL を使用しない R と MRO の比較](media/samples-speed-comparison.png)

MRO と MLS を使用した R の技術的な比較については、[Lixun Zhang の詳細なディスカッション](http://htmlpreview.github.io/?https://github.com/lixzhang/R-MRO-MRS/blob/master/Introduction_to_MRO_and_MRS.html) に関するページを参照してください。

次の図では、ロジスティック回帰モデルの構築時に使用される経過時間 (秒) を比較して、15 分を超える航空便の遅延を予測しています。  CRAN R で使われた経過時間は、行が少し増えると大幅に増加しますが、MLS では約 2 倍のみ増加しています。 このベンチマークの詳細については、*Benchmarks/rxGlm_benchmark.R* サンプルをご覧ください。

![rxGlm のベンチマーク](media/samples-rxGLM-benchmark.png)
