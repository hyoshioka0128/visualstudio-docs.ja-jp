---
title: TensorFlow モデルをローカルにトレーニングする
description: AI Tools for Visual Studio でローカルに TensorFlow モデルを実行します
keywords: AI, Visual Studio, TensorFlow, ローカル
author: jillre
ms.author: jillfra
manager: jillfra
monikerRange: vs-2017
ms.date: 11/13/2017
ms.topic: quickstart
ms.devlang: python
ms.workload:
- multiple
ms.openlocfilehash: eca02b74154eab5468adeabdb84efdf2839fc92e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80638743"
---
# <a name="train-a-tensorflow-model-locally"></a>TensorFlow モデルをローカルにトレーニングする

このクイック スタートでは、Visual Studio Tools for AI でローカルに [MNIST](http://yann.lecun.com/exdb/mnist/) データセットを使って TensorFlow モデルをトレーニングします。

MNIST データベースには、60,000 例のトレーニング セットと、手書きの数字の 10,000 例のテスト セットが含まれます。

## <a name="prerequisites"></a>前提条件

始める前に、次のものがインストールされていることを確認します。

### <a name="google-tensorflow"></a>Google TensorFlow

端末で次のコマンドを実行します。

```cmd
C:\>pip.exe install tensorflow
```

### <a name="numpy-and-scipy"></a>NumPy と SciPy
[NumPy](https://www.lfd.uci.edu/~gohlke/pythonlibs/#numpy) と [SciPy](https://www.lfd.uci.edu/~gohlke/pythonlibs/#scipy) をインストールします。

### <a name="download-sample-code"></a>サンプル コードのダウンロード
TensorFlow、CNTK、Theano などでディープ ラーニングを始めるためのサンプルを含むこの [GitHub リポジトリ](https://github.com/Microsoft/samples-for-ai)をダウンロードします。

## <a name="open-solution-and-train-model"></a>ソリューションを開いてモデルをトレーニングする

- Visual Studio を起動し、**[ファイル] > [開く] > [プロジェクト/ソリューション]** の順に選びます。

- ダウンロードしたサンプル リポジトリで **Tensorflow Examples** フォルダーを選び、**TensorflowExamples.sln** ファイルを開きます。

   ![プロジェクトを開く](media/tensorflow-local/open-project.png)

   ![ソリューションを開く](media/tensorflow-local/open-solution.png)

- **ソリューション エクスプローラー**で MNIST プロジェクトを探して右クリックし、**[スタートアップ プロジェクトに設定]** を選びます。

- **[開始]** をクリックします。

- 出力がコンソールに表示されます。

   ![コンソールからの出力例](media/tensorflow-local/console-output.png)

> [!div class="nextstepaction"]
> [クラウドで TensorFlow モデルをトレーニングする](tensorflow-vm.md)
